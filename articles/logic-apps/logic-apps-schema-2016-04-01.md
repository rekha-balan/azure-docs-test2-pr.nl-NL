---
title: Schema updates June-1-2016 - Azure Logic Apps | Microsoft Docs
description: Updated schema version 2016-06-01 for logic app definitions in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: kevinlam1
ms.author: klam
ms.reviewer: estfan, LADocs
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.topic: article
ms.date: 07/25/2016
ms.openlocfilehash: 43fd52dd04e679b9756c07e8c6e260323469026a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44826865"
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="f5664-103">Schema updates for Azure Logic Apps - June 1, 2016</span><span class="sxs-lookup"><span data-stu-id="f5664-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="f5664-104">The [updated schema](https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json) and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span><span class="sxs-lookup"><span data-stu-id="f5664-104">The [updated schema](https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json) and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

* <span data-ttu-id="f5664-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span><span class="sxs-lookup"><span data-stu-id="f5664-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="f5664-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span><span class="sxs-lookup"><span data-stu-id="f5664-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="f5664-107">More precise ordering for running actions with the `runAfter` property, replacing `dependsOn`</span><span class="sxs-lookup"><span data-stu-id="f5664-107">More precise ordering for running actions with the `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="f5664-108">To upgrade your logic apps from the August 1, 2015 preview schema to the June 1, 2016 schema, [check out the upgrade section](#upgrade-your-schema).</span><span class="sxs-lookup"><span data-stu-id="f5664-108">To upgrade your logic apps from the August 1, 2015 preview schema to the June 1, 2016 schema, [check out the upgrade section](#upgrade-your-schema).</span></span>

<a name="scopes"></a>

## <a name="scopes"></a><span data-ttu-id="f5664-109">Scopes</span><span class="sxs-lookup"><span data-stu-id="f5664-109">Scopes</span></span>

<span data-ttu-id="f5664-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span><span class="sxs-lookup"><span data-stu-id="f5664-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="f5664-111">For example, a condition can contain another condition.</span><span class="sxs-lookup"><span data-stu-id="f5664-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="f5664-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span><span class="sxs-lookup"><span data-stu-id="f5664-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>

## <a name="conditions-and-loops-changes"></a><span data-ttu-id="f5664-113">Conditions and loops changes</span><span class="sxs-lookup"><span data-stu-id="f5664-113">Conditions and loops changes</span></span>

<span data-ttu-id="f5664-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span><span class="sxs-lookup"><span data-stu-id="f5664-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="f5664-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span><span class="sxs-lookup"><span data-stu-id="f5664-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="f5664-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span><span class="sxs-lookup"><span data-stu-id="f5664-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>

## <a name="runafter-property"></a><span data-ttu-id="f5664-117">'runAfter' property</span><span class="sxs-lookup"><span data-stu-id="f5664-117">'runAfter' property</span></span>

<span data-ttu-id="f5664-118">The `runAfter` property replaces `dependsOn`, providing more precision when you specify the run order for actions based on the status of previous actions.</span><span class="sxs-lookup"><span data-stu-id="f5664-118">The `runAfter` property replaces `dependsOn`, providing more precision when you specify the run order for actions based on the status of previous actions.</span></span>

<span data-ttu-id="f5664-119">The `dependsOn` property was synonymous with "the action ran and was successful", no matter how many times you wanted to execute an action, based on whether the previous action was successful, failed, or skipped.</span><span class="sxs-lookup"><span data-stu-id="f5664-119">The `dependsOn` property was synonymous with "the action ran and was successful", no matter how many times you wanted to execute an action, based on whether the previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="f5664-120">The `runAfter` property provides that flexibility as an object that specifies all the action names after which the object runs.</span><span class="sxs-lookup"><span data-stu-id="f5664-120">The `runAfter` property provides that flexibility as an object that specifies all the action names after which the object runs.</span></span> <span data-ttu-id="f5664-121">This property also defines an array of statuses that are acceptable as triggers.</span><span class="sxs-lookup"><span data-stu-id="f5664-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="f5664-122">For example, if you wanted to run after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span><span class="sxs-lookup"><span data-stu-id="f5664-122">For example, if you wanted to run after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="f5664-123">Upgrade your schema</span><span class="sxs-lookup"><span data-stu-id="f5664-123">Upgrade your schema</span></span>

<span data-ttu-id="f5664-124">To upgrade to the [most recent schema](https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json), you need only take a few steps.</span><span class="sxs-lookup"><span data-stu-id="f5664-124">To upgrade to the [most recent schema](https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json), you need only take a few steps.</span></span> <span data-ttu-id="f5664-125">The upgrade process includes running the upgrade script, saving as a new logic app, and if you want, possibly overwriting the previous logic app.</span><span class="sxs-lookup"><span data-stu-id="f5664-125">The upgrade process includes running the upgrade script, saving as a new logic app, and if you want, possibly overwriting the previous logic app.</span></span>

1. <span data-ttu-id="f5664-126">In the Azure portal, open your logic app.</span><span class="sxs-lookup"><span data-stu-id="f5664-126">In the Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="f5664-127">Go to **Overview**.</span><span class="sxs-lookup"><span data-stu-id="f5664-127">Go to **Overview**.</span></span> <span data-ttu-id="f5664-128">On the logic app toolbar, choose **Update Schema**.</span><span class="sxs-lookup"><span data-stu-id="f5664-128">On the logic app toolbar, choose **Update Schema**.</span></span>
   
    ![Choose Update Schema][1]
   
    <span data-ttu-id="f5664-130">The upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span><span class="sxs-lookup"><span data-stu-id="f5664-130">The upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="f5664-131">However, we **strongly recommend** you choose **Save As** to make sure that all connection references are valid in the upgraded logic app.</span><span class="sxs-lookup"><span data-stu-id="f5664-131">However, we **strongly recommend** you choose **Save As** to make sure that all connection references are valid in the upgraded logic app.</span></span>

3. <span data-ttu-id="f5664-132">In the upgrade blade toolbar, choose **Save As**.</span><span class="sxs-lookup"><span data-stu-id="f5664-132">In the upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="f5664-133">Enter the logic name and status.</span><span class="sxs-lookup"><span data-stu-id="f5664-133">Enter the logic name and status.</span></span> <span data-ttu-id="f5664-134">To deploy your upgraded logic app, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="f5664-134">To deploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="f5664-135">Confirm that your upgraded logic app works as expected.</span><span class="sxs-lookup"><span data-stu-id="f5664-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f5664-136">If you are using a manual or request trigger, the callback URL changes in your new logic app.</span><span class="sxs-lookup"><span data-stu-id="f5664-136">If you are using a manual or request trigger, the callback URL changes in your new logic app.</span></span> <span data-ttu-id="f5664-137">Test the new URL to make sure the end-to-end experience works.</span><span class="sxs-lookup"><span data-stu-id="f5664-137">Test the new URL to make sure the end-to-end experience works.</span></span> <span data-ttu-id="f5664-138">To preserve previous URLs, you can clone over your existing logic app.</span><span class="sxs-lookup"><span data-stu-id="f5664-138">To preserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="f5664-139">*Optional* To overwrite your previous logic app with the new schema version, on the toolbar, choose **Clone**, next to **Update Schema**.</span><span class="sxs-lookup"><span data-stu-id="f5664-139">*Optional* To overwrite your previous logic app with the new schema version, on the toolbar, choose **Clone**, next to **Update Schema**.</span></span> <span data-ttu-id="f5664-140">This step is necessary only if you want to keep the same resource ID or request trigger URL of your logic app.</span><span class="sxs-lookup"><span data-stu-id="f5664-140">This step is necessary only if you want to keep the same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="f5664-141">Upgrade tool notes</span><span class="sxs-lookup"><span data-stu-id="f5664-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="f5664-142">Mapping conditions</span><span class="sxs-lookup"><span data-stu-id="f5664-142">Mapping conditions</span></span>

<span data-ttu-id="f5664-143">In the upgraded definition, the tool makes a best effort at grouping true and false branch actions together as a scope.</span><span class="sxs-lookup"><span data-stu-id="f5664-143">In the upgraded definition, the tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="f5664-144">Specifically, the designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span><span class="sxs-lookup"><span data-stu-id="f5664-144">Specifically, the designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="f5664-145">However, if the tool detects unrecognizable patterns, the tool might create separate conditions for both the true and the false branch.</span><span class="sxs-lookup"><span data-stu-id="f5664-145">However, if the tool detects unrecognizable patterns, the tool might create separate conditions for both the true and the false branch.</span></span> <span data-ttu-id="f5664-146">You can remap actions after upgrading, if necessary.</span><span class="sxs-lookup"><span data-stu-id="f5664-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="f5664-147">'foreach' loop with condition</span><span class="sxs-lookup"><span data-stu-id="f5664-147">'foreach' loop with condition</span></span>

<span data-ttu-id="f5664-148">In the new schema, you can use the filter action to replicate the pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span><span class="sxs-lookup"><span data-stu-id="f5664-148">In the new schema, you can use the filter action to replicate the pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="f5664-149">The condition becomes a filter action before the foreach loop for returning only an array of items that match the condition, and that array is passed into the foreach action.</span><span class="sxs-lookup"><span data-stu-id="f5664-149">The condition becomes a filter action before the foreach loop for returning only an array of items that match the condition, and that array is passed into the foreach action.</span></span> <span data-ttu-id="f5664-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="f5664-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="f5664-151">Resource tags</span><span class="sxs-lookup"><span data-stu-id="f5664-151">Resource tags</span></span>

<span data-ttu-id="f5664-152">After you upgrade, resource tags are removed, so you must reset them for the upgraded workflow.</span><span class="sxs-lookup"><span data-stu-id="f5664-152">After you upgrade, resource tags are removed, so you must reset them for the upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="f5664-153">Other changes</span><span class="sxs-lookup"><span data-stu-id="f5664-153">Other changes</span></span>

### <a name="renamed-manual-trigger-to-request-trigger"></a><span data-ttu-id="f5664-154">Renamed 'manual' trigger to 'request' trigger</span><span class="sxs-lookup"><span data-stu-id="f5664-154">Renamed 'manual' trigger to 'request' trigger</span></span>

<span data-ttu-id="f5664-155">The `manual` trigger type was deprecated and renamed to `request` with type `http`.</span><span class="sxs-lookup"><span data-stu-id="f5664-155">The `manual` trigger type was deprecated and renamed to `request` with type `http`.</span></span> <span data-ttu-id="f5664-156">This change creates more consistency for the kind of pattern that the trigger is used to build.</span><span class="sxs-lookup"><span data-stu-id="f5664-156">This change creates more consistency for the kind of pattern that the trigger is used to build.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="f5664-157">New 'filter' action</span><span class="sxs-lookup"><span data-stu-id="f5664-157">New 'filter' action</span></span>

<span data-ttu-id="f5664-158">To filter a large array down to a smaller set of items, the new `filter` type accepts an array and a condition, evaluates the condition for each item, and returns an array with items meeting the condition.</span><span class="sxs-lookup"><span data-stu-id="f5664-158">To filter a large array down to a smaller set of items, the new `filter` type accepts an array and a condition, evaluates the condition for each item, and returns an array with items meeting the condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="f5664-159">Restrictions for 'foreach' and 'until' actions</span><span class="sxs-lookup"><span data-stu-id="f5664-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="f5664-160">The `foreach` and `until` loop are restricted to a single action.</span><span class="sxs-lookup"><span data-stu-id="f5664-160">The `foreach` and `until` loop are restricted to a single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="f5664-161">New 'trackedProperties' for actions</span><span class="sxs-lookup"><span data-stu-id="f5664-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="f5664-162">Actions can now have an additional property called `trackedProperties`, which is sibling to the `runAfter` and `type` properties.</span><span class="sxs-lookup"><span data-stu-id="f5664-162">Actions can now have an additional property called `trackedProperties`, which is sibling to the `runAfter` and `type` properties.</span></span> <span data-ttu-id="f5664-163">This object specifies certain action inputs or outputs that you want to include in the Azure Diagnostic telemetry, emitted as part of a workflow.</span><span class="sxs-lookup"><span data-stu-id="f5664-163">This object specifies certain action inputs or outputs that you want to include in the Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="f5664-164">For example:</span><span class="sxs-lookup"><span data-stu-id="f5664-164">For example:</span></span>

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="f5664-165">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f5664-165">Next Steps</span></span>
* [<span data-ttu-id="f5664-166">Create workflow definitions for logic apps</span><span class="sxs-lookup"><span data-stu-id="f5664-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="f5664-167">Create deployment templates for logic apps</span><span class="sxs-lookup"><span data-stu-id="f5664-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
