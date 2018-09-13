---
title: Getting Compliance Data in Azure Policy
description: Azure Policy evaluations and effects determine compliance. Learn how to get the compliance details.
services: azure-policy
author: DCtheGeek
ms.author: dacoulte
ms.date: 07/29/2018
ms.topic: conceptual
ms.service: azure-policy
manager: carmonm
ms.custom: mvc
ms.openlocfilehash: 6b310daec67f41ba589ce279e4a2dad427adb734
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858062"
---
# <a name="getting-compliance-data"></a>Getting Compliance Data

One of the largest benefits of Azure Policy is the insight and controls it provides over resources in a subscription or [management group](../azure-resource-manager/management-groups-overview.md) of subscriptions. This control can be exercised in many different ways, such as preventing resources being created in the wrong location, enforcing common and consistent tag usage, or auditing existing resources for appropriate configurations and settings. In all cases, data is generated by Policy to enable you to understand the compliance state of your environment.

There are several ways to access the compliance information generated by your policy and initiative assignments:

- Using the [Azure Portal](#portal)
- Through [command line](#command-line) scripting

Before looking at the methods to report on compliance, let's look at when compliance information is updated and the frequency and events that trigger an evaluation cycle.

> [!WARNING]
> If compliance status is being reported as **'N/A'**, verify that the **Microsoft.PolicyInsights** Resource Provider is registered and that the user has the appropriate role-based access control (RBAC) permissions as described [here](azure-policy-introduction.md#rbac-permissions-in-azure-policy).

## <a name="evaluation-triggers"></a>Evaluation triggers

The results of a completed evaluation cycle are reflected in the `Microsoft.PolicyInsights` Resource Provider through `PolicyStates` and `PolicyEvents` operations. For more information about the options and capabilities of the Policy Insights REST API, see [Policy Insights](/rest/api/policy-insights/).

Evaluations of assigned policies and initiatives happen as the result of various events:

- A policy or initiative is newly assigned to a scope. When this occurs, it takes around 30 minutes for the assignment to be applied to the defined scope. Once it is applied, the evaluation cycle begins for resources within that scope against the newly assigned policy or initiative and depending on the effects used by the policy or initiative, resources are marked as compliant or non-compliant. A large policy or initiative evaluated against a large scope of resources can take time, so there is no pre-defined expectation of when the evaluation cycle will complete. Once it completes, updated compliance results are available in the portal and SDKs.
- A policy or initiative already assigned to a scope is updated. The evaluation cycle and timing for this scenario is the same as for a new assignment to a scope.
- A resource is deployed to a scope with an assignment via Resource Manager, REST, Azure CLI, or Azure PowerShell. In this scenario, the effect event (append, audit, deny, deploy) and compliant status information for the individual resource becomes available in the portal and SDKs around 15 minutes later. This event does not cause an evaluation of other resources.
- Standard compliance evaluation cycle. Once every 24 hours, assignments are automatically re-evaluated. A large policy or initiative evaluated against a large scope of resources can take time, so there is no pre-defined expectation of when the evaluation cycle will complete. Once it completes, updated compliance results are available in the portal and SDKs.

## <a name="how-compliance-works"></a>How compliance works

In an assignment, a resource is non-compliant if it doesn't follow policy or initiative rules. The following table shows how different policy effects work with the condition evaluation for the resulting compliance state:

| Resource state | Effect | Policy evaluation | Compliance state |
| --- | --- | --- | --- |
| Exists | Deny, Audit, Append\*, DeployIfNotExist\*, AuditIfNotExist\* | True | Non-Compliant |
| Exists | Deny, Audit, Append\*, DeployIfNotExist\*, AuditIfNotExist\* | False | Compliant |
| New | Audit, AuditIfNotExist\* | True | Non-Compliant |
| New | Audit, AuditIfNotExist\* | False | Compliant |

\* The Append, DeployIfNotExist, and AuditIfNotExist effects require the IF statement to be TRUE.
The effects also require the existence condition to be FALSE to be non-compliant. When TRUE, the IF condition triggers evaluation of the existence condition for the related resources.

For example, assume that you have a resource group – ContsoRG, with some storage accounts (highlighted in red) that are exposed to public networks.

![Storage accounts exposed to public networks](media/policy-insights/resource-group01.png)

In this example, you need to be wary of security risks. Now that you've created a policy assignment, it is evaluated for all storage accounts in the ContosoRG resource group. It audits the three non-compliant storage accounts, consequently changing their states to **non-compliant.**

![Audited non-compliant storage accounts](media/policy-insights/resource-group03.png)

## <a name="portal"></a>Portal

The Azure portal showcases a graphical experience of visualizing and understanding the state of compliance in your environment. On the **Policy** page, the **Overview** option provides details for available scopes on the compliance of both policies and initiatives. In addition to the compliance state and count per assignment, it contains a chart showing compliance over the last seven days. The **Compliance** page contains much of this same information (except the chart), but provide additional filtering and sorting options.

![Policy Compliance Page](media/policy-compliance/compliance-page.png)

As a policy or initiative can be assigned to different scopes, note in the table the scope for each assignment and the type of definition that was assigned to that scope. The number of non-compliant policies and non-compliant resources for each assignment are also provided. Clicking on a policy or initiative in the table provides a deeper look at the compliance for that particular assignment.

![Policy Compliance Details](media/policy-compliance/compliance-details.png)

While the list of resources on the **Non-compliant resources** tab reflects the evaluation status of existing resources for the current assignment, events (append, audit, deny, deploy) triggered by the request to create a resource are shown under the **Events** tab.

![Policy Compliance Events](media/policy-compliance/compliance-events.png)

Right-click on the row of the event you would like to gather more details on and select **Show activity logs**. The activity log page opens and is pre-filtered to the search showing details for the assignment and the events. The activity log provides additional context and information about those events.

![Policy Compliance Activity Log](media/policy-compliance/compliance-activitylog.png)

## <a name="command-line"></a>Command Line

The same information that is available in the portal can be retrieved using the REST API directly (including with [ARMClient](https://github.com/projectkudu/ARMClient)) or Azure PowerShell with the REST API. For full details on the REST API, see the [Policy Insights](/rest/api/policy-insights/) reference. The REST API reference pages have a green 'Try It' button on each operation that allows you to try it right in the browser.

To use the following examples in Azure PowerShell, construct an authentication token with this example code. Then replace the $restUri with the desired string in the examples to retrieve a JSON object that can then be parsed.

```azurepowershell-interactive
# Login first with Connect-AzureRmAccount if not using Cloud Shell

$azContext = Get-AzureRmContext
$azProfile = [Microsoft.Azure.Commands.Common.Authentication.Abstractions.AzureRmProfileProvider]::Instance.Profile
$profileClient = New-Object -TypeName Microsoft.Azure.Commands.ResourceManager.Common.RMProfileClient -ArgumentList ($azProfile)
$token = $profileClient.AcquireAccessToken($azContext.Subscription.TenantId)
$authHeader = @{
    'Content-Type'='application/json'
    'Authorization'='Bearer ' + $token.AccessToken
}

# Define the REST API to communicate with
# Use double quotes for $restUri as some endpoints take strings passed in single quotes
$restUri = "https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.PolicyInsights/policyStates/latest/summarize?api-version=2018-04-04"

# Invoke the REST API
$response = Invoke-RestMethod -Uri $restUri -Method POST -Headers $authHeader

# View the response object (as JSON)
$response
```

### <a name="summarize-results"></a>Summarize results

Using the REST API, summarization can be performed by management group, subscription, resource group, resource, initiative, policy, subscription level assignment, or resource group level assignment. Here is an example of summarization at the subscription level using Policy Insight's [Summarize For Subscription](/rest/api/policy-insights/policystates/summarizeforsubscription):

```http
POST https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.PolicyInsights/policyStates/latest/summarize?api-version=2018-04-04
```

The output summarizes the subscription. In the example output below, the summarized compliance are under **value.results.nonCompliantResources** and **value.results.nonCompliantPolicies**. This request provides further details, including each assignment that made up the non-compliant numbers and the definition information for each assignment. Each policy object in the hierarchy provides a **queryResultsUri** that can be used to get additional detail at that level.

```json
{
    "@odata.context": "https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.PolicyInsights/policyStates/$metadata#summary",
    "@odata.count": 1,
    "value": [{
        "@odata.id": null,
        "@odata.context": "https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.PolicyInsights/policyStates/$metadata#summary/$entity",
        "results": {
            "queryResultsUri": "https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.PolicyInsights/policyStates/latest/queryResults?api-version=2018-04-04&$from=2018-05-18 04:28:22Z&$to=2018-05-19 04:28:22Z&$filter=IsCompliant eq false",
            "nonCompliantResources": 15,
            "nonCompliantPolicies": 1
        },
        "policyAssignments": [{
            "policyAssignmentId": "/subscriptions/{subscriptionId}/resourcegroups/rg-tags/providers/microsoft.authorization/policyassignments/37ce239ae4304622914f0c77",
            "policySetDefinitionId": "",
            "results": {
                "queryResultsUri": "https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.PolicyInsights/policyStates/latest/queryResults?api-version=2018-04-04&$from=2018-05-18 04:28:22Z&$to=2018-05-19 04:28:22Z&$filter=IsCompliant eq false and PolicyAssignmentId eq '/subscriptions/{subscriptionId}/resourcegroups/rg-tags/providers/microsoft.authorization/policyassignments/37ce239ae4304622914f0c77'",
                "nonCompliantResources": 15,
                "nonCompliantPolicies": 1
            },
            "policyDefinitions": [{
                "policyDefinitionReferenceId": "",
                "policyDefinitionId": "/providers/microsoft.authorization/policydefinitions/1e30110a-5ceb-460c-a204-c1c3969c6d62",
                "effect": "deny",
                "results": {
                    "queryResultsUri": "https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.PolicyInsights/policyStates/latest/queryResults?api-version=2018-04-04&$from=2018-05-18 04:28:22Z&$to=2018-05-19 04:28:22Z&$filter=IsCompliant eq false and PolicyAssignmentId eq '/subscriptions/{subscriptionId}/resourcegroups/rg-tags/providers/microsoft.authorization/policyassignments/37ce239ae4304622914f0c77' and PolicyDefinitionId eq '/providers/microsoft.authorization/policydefinitions/1e30110a-5ceb-460c-a204-c1c3969c6d62'",
                    "nonCompliantResources": 15
                }
            }]
        }]
    }]
}
```

### <a name="query-for-resources"></a>Query for resources

Using the example from above, **value.policyAssignments.policyDefinitions.results.queryResultsUri** provided us with a sample Uri for getting all non-compliant resources for a specific policy definition. Looking at the **$filter** value, IsCompliant is equal (eq) to false, PolicyAssignmentId is specified for the policy definition, and then the PolicyDefinitionId itself.
The reason for including the PolicyAssignmentId in the filter is because the PolicyDefinitionId could exist in several policy or initiative assignments with a variety of scopes. By specifying both the PolicyAssignmentId and the PolicyDefinitionId, we can be explicit in the results we are looking for. Previously, we used **latest** for the PolicyStates (the only allowed value for **policyStatesSummaryResource** on the Summarize For Subscription operator), which automatically sets a **from** and **to** time window of the last 24-hours.

```http
https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.PolicyInsights/policyStates/latest/queryResults?api-version=2018-04-04&$from=2018-05-18 04:28:22Z&$to=2018-05-19 04:28:22Z&$filter=IsCompliant eq false and PolicyAssignmentId eq '/subscriptions/{subscriptionId}/resourcegroups/rg-tags/providers/microsoft.authorization/policyassignments/37ce239ae4304622914f0c77' and PolicyDefinitionId eq '/providers/microsoft.authorization/policydefinitions/1e30110a-5ceb-460c-a204-c1c3969c6d62'
```

The example response below has been trimmed to just showing a single non-compliant resource for brevity (note that @odata.count is actually 15 and matches the count of non-compliant resources from the example above). The detailed response provides several pieces of data about the resource, the policy (or initiative), and the assignment. Notice that you can also see what assignment parameters were passed to the policy definition.

```json
{
    "@odata.context": "https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.PolicyInsights/policyStates/$metadata#latest",
    "@odata.count": 15,
    "value": [{
        "@odata.id": null,
        "@odata.context": "https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.PolicyInsights/policyStates/$metadata#latest/$entity",
        "timestamp": "2018-05-19T04:41:09Z",
        "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/rg-tags/providers/Microsoft.Compute/virtualMachines/linux",
        "policyAssignmentId": "/subscriptions/{subscriptionId}/resourceGroups/rg-tags/providers/Microsoft.Authorization/policyAssignments/37ce239ae4304622914f0c77",
        "policyDefinitionId": "/providers/Microsoft.Authorization/policyDefinitions/1e30110a-5ceb-460c-a204-c1c3969c6d62",
        "effectiveParameters": "",
        "isCompliant": false,
        "subscriptionId": "{subscriptionId}",
        "resourceType": "/Microsoft.Compute/virtualMachines",
        "resourceLocation": "westus2",
        "resourceGroup": "RG-Tags",
        "resourceTags": "tbd",
        "policyAssignmentName": "37ce239ae4304622914f0c77",
        "policyAssignmentOwner": "tbd",
        "policyAssignmentParameters": "{\"tagName\":{\"value\":\"costCenter\"},\"tagValue\":{\"value\":\"Contoso-Test\"}}",
        "policyAssignmentScope": "/subscriptions/{subscriptionId}/resourceGroups/RG-Tags",
        "policyDefinitionName": "1e30110a-5ceb-460c-a204-c1c3969c6d62",
        "policyDefinitionAction": "deny",
        "policyDefinitionCategory": "tbd",
        "policySetDefinitionId": "",
        "policySetDefinitionName": "",
        "policySetDefinitionOwner": "",
        "policySetDefinitionCategory": "",
        "policySetDefinitionParameters": "",
        "managementGroupIds": "",
        "policyDefinitionReferenceId": ""
    }]
}
```

### <a name="view-events"></a>View events

When a resource is created or updated, a policy evaluation result is generated. Results are called _policy events_. Use the following Uri to view recent policy events associated with the subscription.

```http
https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.PolicyInsights/policyEvents/default/queryResults?api-version=2018-04-04
```

Your results resemble the following example:

```json
{
    "@odata.context": "https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.PolicyInsights/policyEvents/$metadata#default",
    "@odata.count": 1,
    "value": [{
        "@odata.id": null,
        "@odata.context": "https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.PolicyInsights/policyEvents/$metadata#default/$entity",
        "NumAuditEvents": 16
    }]
}
```

For more information about querying policy events, see the [Policy Events](/rest/api/policy-insights/policyevents) reference article.

### <a name="azure-powershell"></a>Azure PowerShell

The Azure PowerShell module for Policy is available on the PowerShell Gallery as [AzureRM.PolicyInsights](https://www.powershellgallery.com/packages/AzureRM.PolicyInsights). Using PowerShellGet, you can install the module using `Install-Module -Name AzureRM.PolicyInsights` (make sure you have the latest [Azure PowerShell](/powershell/azure/install-azurerm-ps) installed):

```powershell
# Install from PowerShell Gallery via PowerShellGet
Install-Module -Name AzureRM.PolicyInsights

# Import the downloaded module
Import-Module AzureRM.PolicyInsights

# Login with Connect-AzureRmAccount if not using Cloud Shell
Connect-AzureRmAccount
```

The module has three cmdlets:

- `Get-AzureRmPolicyStateSummary`
- `Get-AzureRmPolicyState`
- `Get-AzureRmPolicyEvent`

Example: Getting the state summary for the topmost assigned policy with the highest number of non-compliant resources.

```powershell
PS > Get-AzureRmPolicyStateSummary -Top 1

NonCompliantResources : 15
NonCompliantPolicies  : 1
PolicyAssignments     : {/subscriptions/{subscriptionId}/resourcegroups/RG-Tags/providers/micros
                        oft.authorization/policyassignments/37ce239ae4304622914f0c77}
```

Example: Getting the state record for the most recently evaluated resource (default is by timestamp in descending order).

```powershell
PS > Get-AzureRmPolicyState -Top 1

Timestamp                  : 5/22/2018 3:47:34 PM
ResourceId                 : /subscriptions/{subscriptionId}/resourceGroups/RG-Tags/providers/Mi
                             crosoft.Network/networkInterfaces/linux316
PolicyAssignmentId         : /subscriptions/{subscriptionId}/resourceGroups/RG-Tags/providers/Mi
                             crosoft.Authorization/policyAssignments/37ce239ae4304622914f0c77
PolicyDefinitionId         : /providers/Microsoft.Authorization/policyDefinitions/1e30110a-5ceb-460c-a204-c1c3969c6d62
IsCompliant                : False
SubscriptionId             : {subscriptionId}
ResourceType               : /Microsoft.Network/networkInterfaces
ResourceLocation           : westus2
ResourceGroup              : RG-Tags
ResourceTags               : tbd
PolicyAssignmentName       : 37ce239ae4304622914f0c77
PolicyAssignmentOwner      : tbd
PolicyAssignmentParameters : {"tagName":{"value":"costCenter"},"tagValue":{"value":"Contoso-Test"}}
PolicyAssignmentScope      : /subscriptions/{subscriptionId}/resourceGroups/RG-Tags
PolicyDefinitionName       : 1e30110a-5ceb-460c-a204-c1c3969c6d62
PolicyDefinitionAction     : deny
PolicyDefinitionCategory   : tbd
```

Example: Getting the details for all non-compliant virtual network resources.

```powershell
PS > Get-AzureRmPolicyState -Filter "ResourceType eq '/Microsoft.Network/virtualNetworks'"

Timestamp                  : 5/22/2018 4:02:20 PM
ResourceId                 : /subscriptions/{subscriptionId}/resourceGroups/RG-Tags/providers/Mi
                             crosoft.Network/virtualNetworks/RG-Tags-vnet
PolicyAssignmentId         : /subscriptions/{subscriptionId}/resourceGroups/RG-Tags/providers/Mi
                             crosoft.Authorization/policyAssignments/37ce239ae4304622914f0c77
PolicyDefinitionId         : /providers/Microsoft.Authorization/policyDefinitions/1e30110a-5ceb-460c-a204-c1c3969c6d62
IsCompliant                : False
SubscriptionId             : {subscriptionId}
ResourceType               : /Microsoft.Network/virtualNetworks
ResourceLocation           : westus2
ResourceGroup              : RG-Tags
ResourceTags               : tbd
PolicyAssignmentName       : 37ce239ae4304622914f0c77
PolicyAssignmentOwner      : tbd
PolicyAssignmentParameters : {"tagName":{"value":"costCenter"},"tagValue":{"value":"Contoso-Test"}}
PolicyAssignmentScope      : /subscriptions/{subscriptionId}/resourceGroups/RG-Tags
PolicyDefinitionName       : 1e30110a-5ceb-460c-a204-c1c3969c6d62
PolicyDefinitionAction     : deny
PolicyDefinitionCategory   : tbd
```

Example: Getting events related to non-compliant virtual network resources that occurred after a specific date.

```powershell
PS > Get-AzureRmPolicyEvent -Filter "ResourceType eq '/Microsoft.Network/virtualNetworks'" -From '2018-05-19'

Timestamp                  : 5/19/2018 5:18:53 AM
ResourceId                 : /subscriptions/{subscriptionId}/resourceGroups/RG-Tags/providers/Mi
                             crosoft.Network/virtualNetworks/RG-Tags-vnet
PolicyAssignmentId         : /subscriptions/{subscriptionId}/resourceGroups/RG-Tags/providers/Mi
                             crosoft.Authorization/policyAssignments/37ce239ae4304622914f0c77
PolicyDefinitionId         : /providers/Microsoft.Authorization/policyDefinitions/1e30110a-5ceb-460c-a204-c1c3969c6d62
IsCompliant                : False
SubscriptionId             : {subscriptionId}
ResourceType               : /Microsoft.Network/virtualNetworks
ResourceLocation           : eastus
ResourceGroup              : RG-Tags
ResourceTags               : tbd
PolicyAssignmentName       : 37ce239ae4304622914f0c77
PolicyAssignmentOwner      : tbd
PolicyAssignmentParameters : {"tagName":{"value":"costCenter"},"tagValue":{"value":"Contoso-Test"}}
PolicyAssignmentScope      : /subscriptions/{subscriptionId}/resourceGroups/RG-Tags
PolicyDefinitionName       : 1e30110a-5ceb-460c-a204-c1c3969c6d62
PolicyDefinitionAction     : deny
PolicyDefinitionCategory   : tbd
TenantId                   : {tenantId}
PrincipalOid               : {principalOid}
```

The **PrincipalOid** field can be used to get a specific user with the Azure PowerShell cmdlet `Get-AzureRmADUser`. Replace **{principalOid}** with the response you get from the previous example.

```powershell
PS > (Get-AzureRmADUser -ObjectId {principalOid}).DisplayName
Trent Baker
```

## <a name="log-analytics"></a>Log Analytics

If you have a [Log Analytics](../log-analytics/log-analytics-overview.md) workspace with the `AzureActivity` solution tied to your subscription, then you can also view non-compliance results from the evaluation cycle using simple Kusto queries and the `AzureActivity` table. With non-compliance details in Log Analytics, this also means that alerts could be configured to watch for non-compliance on a specific resource, resource group, or even a threshold of non-compliant items, such as more than 10 in the last 24 hours.

![Policy Compliance using Log Analytics](media/policy-compliance/compliance-loganalytics.png)

## <a name="next-steps"></a>Next steps

- Review the [Policy definition structure](policy-definition.md).
- Review [Understanding policy effects](policy-effects.md).
- Review what a management group is with [Organize your resources with Azure management groups](../azure-resource-manager/management-groups-overview.md)