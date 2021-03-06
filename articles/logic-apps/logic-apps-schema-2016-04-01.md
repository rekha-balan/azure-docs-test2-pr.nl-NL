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
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a>Schema updates for Azure Logic Apps - June 1, 2016

The [updated schema](https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json) and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:

* [Scopes](#scopes) let you group or nest actions as a collection of actions.
* [Conditions and loops](#conditions-loops) are now first-class actions.
* More precise ordering for running actions with the `runAfter` property, replacing `dependsOn`

To upgrade your logic apps from the August 1, 2015 preview schema to the June 1, 2016 schema, [check out the upgrade section](#upgrade-your-schema).

<a name="scopes"></a>

## <a name="scopes"></a>Scopes

This schema includes scopes, which let you group actions together, or nest actions inside each other. For example, a condition can contain another condition. Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:

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

## <a name="conditions-and-loops-changes"></a>Conditions and loops changes

In previous schema versions, conditions and loops were parameters associated with a single action. This schema lifts this limitation, so conditions and loops now appear as action types. Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:

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

## <a name="runafter-property"></a>'runAfter' property

The `runAfter` property replaces `dependsOn`, providing more precision when you specify the run order for actions based on the status of previous actions.

The `dependsOn` property was synonymous with "the action ran and was successful", no matter how many times you wanted to execute an action, based on whether the previous action was successful, failed, or skipped. The `runAfter` property provides that flexibility as an object that specifies all the action names after which the object runs. This property also defines an array of statuses that are acceptable as triggers. For example, if you wanted to run after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a>Upgrade your schema

To upgrade to the [most recent schema](https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json), you need only take a few steps. The upgrade process includes running the upgrade script, saving as a new logic app, and if you want, possibly overwriting the previous logic app.

1. In the Azure portal, open your logic app.

2. Go to **Overview**. On the logic app toolbar, choose **Update Schema**.
   
    ![Choose Update Schema][1]
   
    The upgraded definition is returned, which you can copy and paste into a resource definition if necessary. 
    However, we **strongly recommend** you choose **Save As** to make sure that all connection references are valid in the upgraded logic app.

3. In the upgrade blade toolbar, choose **Save As**.

4. Enter the logic name and status. To deploy your upgraded logic app, choose **Create**.

5. Confirm that your upgraded logic app works as expected.
   
   > [!NOTE]
   > If you are using a manual or request trigger, the callback URL changes in your new logic app. Test the new URL to make sure the end-to-end experience works. To preserve previous URLs, you can clone over your existing logic app.

6. *Optional* To overwrite your previous logic app with the new schema version, on the toolbar, choose **Clone**, next to **Update Schema**. This step is necessary only if you want to keep the same resource ID or request trigger URL of your logic app.

### <a name="upgrade-tool-notes"></a>Upgrade tool notes

#### <a name="mapping-conditions"></a>Mapping conditions

In the upgraded definition, the tool makes a best effort at grouping true and false branch actions together as a scope. Specifically, the designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action. However, if the tool detects unrecognizable patterns, the tool might create separate conditions for both the true and the false branch. You can remap actions after upgrading, if necessary.

#### <a name="foreach-loop-with-condition"></a>'foreach' loop with condition

In the new schema, you can use the filter action to replicate the pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade. The condition becomes a filter action before the foreach loop for returning only an array of items that match the condition, and that array is passed into the foreach action. For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).

#### <a name="resource-tags"></a>Resource tags

After you upgrade, resource tags are removed, so you must reset them for the upgraded workflow.

## <a name="other-changes"></a>Other changes

### <a name="renamed-manual-trigger-to-request-trigger"></a>Renamed 'manual' trigger to 'request' trigger

The `manual` trigger type was deprecated and renamed to `request` with type `http`. This change creates more consistency for the kind of pattern that the trigger is used to build.

### <a name="new-filter-action"></a>New 'filter' action

To filter a large array down to a smaller set of items, the new `filter` type accepts an array and a condition, evaluates the condition for each item, and returns an array with items meeting the condition.

### <a name="restrictions-for-foreach-and-until-actions"></a>Restrictions for 'foreach' and 'until' actions

The `foreach` and `until` loop are restricted to a single action.

### <a name="new-trackedproperties-for-actions"></a>New 'trackedProperties' for actions

Actions can now have an additional property called `trackedProperties`, which is sibling to the `runAfter` and `type` properties. This object specifies certain action inputs or outputs that you want to include in the Azure Diagnostic telemetry, emitted as part of a workflow. For example:

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

## <a name="next-steps"></a>Next Steps
* [Create workflow definitions for logic apps](../logic-apps/logic-apps-author-definitions.md)
* [Create deployment templates for logic apps](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
