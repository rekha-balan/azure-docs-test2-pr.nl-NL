---
title: Secure access to Azure Logic Apps | Microsoft Docs
description: Add security for protecting access to triggers, inputs and outputs, action parameters, and services used with workflows in Azure Logic Apps.
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: ''
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: jehollan
ms.openlocfilehash: 3f119409e031ca2b88694a011916f52aa9ef5d36
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660695"
---
# <a name="secure-access-to-your-logic-apps"></a>Secure access to your logic apps

There are many tools available to help you secure your logic app.

* Securing access to trigger a logic app (HTTP Request Trigger)
* Securing access to manage, edit, or read a logic app
* Securing access to contents of inputs and outputs for a run
* Securing parameters or inputs within actions in a workflow
* Securing access to services that receive requests from a workflow

## <a name="secure-access-to-trigger"></a>Secure access to trigger

When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire the logic app. All requests into a logic app are encrypted and secured via SSL.

### <a name="shared-access-signature"></a>Shared Access Signature

Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/storage-dotnet-shared-access-signature-part-1.md) as part of the URL. Each URL contains a `sp`, `sv`, and `sig` query parameter. Permissions are specified by `sp`, and correspond to HTTP methods allowed, `sv` is the version used to generate, and `sig` is used to authenticate access to trigger. The signature is generated using the SHA256 algorithm with a secret key on all the URL paths and properties. The secret key is never exposed and published, and is kept encrypted and stored as part of the logic app. Your logic app only authorizes triggers that contain a valid signature created with the secret key.

#### <a name="regenerate-access-keys"></a>Regenerate access keys

You can regenerate a new secure key at anytime through the REST API or Azure portal. All current URLs that were generated previously using the old key are invalidated and no longer authorized to fire the logic app.

1. In the Azure portal, open the logic app you want to regenerate a key
1. Click the **Access Keys** menu item under **Settings**
1. Choose the key to regenerate and complete the process

URLs you retrieve after regeneration are signed with the new access key.

#### <a name="creating-callback-urls-with-an-expiration-date"></a>Creating callback URLs with an expiration date

If you are sharing the URL with other parties, you can generate URLs with specific keys and expiration dates as needed. You can then seamlessly roll keys, or ensure access to fire an app is restricted to a certain timespan. You can specify an expiration date for a URL through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

In the body, include the property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until the `NotAfter` date and time.

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a>Creating URLs with primary or secondary secret key

When you generate or list callback URLs for request-based triggers, you can also specify which key to use to sign the URL.  You can generate a URL signed by a specific key through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

In the body, include the property `KeyType` as either `Primary` or `Secondary`.  This returns a URL signed by the secure key specified.

### <a name="restrict-incoming-ip-addresses"></a>Restrict incoming IP addresses

In addition to the Shared Access Signature, you may wish to restrict calling a logic app only from specific clients.  For example, if you manage your endpoint through Azure API Management, you can restrict the logic app to only accept the request when the request comes from the API Management instance IP address.

This setting can be configured within the logic app settings:

1. In the Azure portal, open the logic app you want to add IP address restrictions
1. Click the **Access control configuration** menu item under **Settings**
1. Specify the list of IP address ranges to be accepted by the trigger

A valid IP range takes the format `192.168.1.1/255`. If you want the logic app to only fire as a nested logic app, select the **Only other logic apps** option. This option writes an empty array to the resource, meaning only calls from the service itself (parent logic apps) fire successfully.

> [!NOTE]
> You can still run a logic app with a request trigger through the REST API / Management `/triggers/{triggerName}/run` regardless of IP. This scenario requires authentication against the Azure REST API, and all events would appear in the Azure Audit Log. Set access control policies accordingly.

#### <a name="setting-ip-ranges-on-the-resource-definition"></a>Setting IP ranges on the resource definition

If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a>Adding Azure Active Directory, OAuth, or other security

To add more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with the capability to expose a logic app as an API. Azure API Management can expose a public or private endpoint for the logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards. When a request is received, Azure API Management forwards the request to the logic app (performing any needed transformations or restrictions in-flight). You can use the incoming IP range settings on the logic app to only allow the logic app to be triggered from API Management.

## <a name="secure-access-to-manage-or-edit-logic-apps"></a>Secure access to manage or edit logic apps

You can restrict access to management operations on a logic app so that only specific users or groups are able to perform operations on the resource. Logic apps use the Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with the same tools.  There are a few built-in roles you can assign members of your subscription to as well:

* **Logic App Contributor** - Provides access to view, edit, and update a logic app.  Cannot remove the resource or perform admin operations.
* **Logic App Operator** - Can view the logic app and run history, and enable/disable.  Cannot edit or update the definition.

You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) to prevent changing or deleting logic apps. This capability is valuable to prevent production resources from changes or deletions.

## <a name="secure-access-to-contents-of-the-run-history"></a>Secure access to contents of the run history

You can restrict access to contents of inputs or outputs from previous runs to specific IP address ranges.  

All data within a workflow run is encrypted in transit and at rest. When a call to run history is made, the service authenticates the request and provides links to the request and response inputs and outputs. This link can be protected so only requests to view content from a designated IP address range return the contents. You can use this capability for additional access control. You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs. Only someone with admin permissions could remove this restriction, providing the possibility for 'just-in-time' access to workflow contents.

This setting can be configured within the resource settings of the Azure portal:

1. In the Azure portal, open the logic app you want to add IP address restrictions
1. Click the **Access control configuration** menu item under **Settings**
1. Specify the list of IP address ranges for access to content

#### <a name="setting-ip-ranges-on-the-resource-definition"></a>Setting IP ranges on the resource definition

If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a>Secure parameters and inputs within a workflow

You might want to parameterize some aspects of a workflow definition for deployment across environments. Also, some parameters might be secure parameters you don't want to appear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.

### <a name="using-parameters-and-secure-parameters"></a>Using parameters and secure parameters

To access the value of a resource parameter at runtime, the [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation. Also, you can [specify parameters in the resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters). But if you specify the parameter type as `securestring`, the parameter won't be returned with the rest of the resource definition, and won't be accessible by viewing the resource after deployment.

> [!NOTE]
> If your parameter is used in the headers or body of a request, the parameter might be visible by accessing the run history and outgoing HTTP request. Make sure to set your content access policies accordingly.
> Authorization headers are never visible through inputs or outputs. So if the secret is being used there, the secret is not retrievable.

#### <a name="resource-deployment-template-with-secrets"></a>Resource deployment template with secrets

The following example shows a deployment that references a secure parameter of `secret` at runtime. In a separate parameters file, you could specify the environment value for the `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) to retrieve secrets at deploy time.

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is the request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-to-services-receiving-requests-from-a-workflow"></a>Secure access to services receiving requests from a workflow

There are many ways to help secure any endpoint the logic app needs to access.

### <a name="using-authentication-on-outbound-requests"></a>Using authentication on outbound requests

When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication to the request being sent. You could include basic authentication, certificate authentication, or Azure Active Directory authentication. Details on how to configure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).

### <a name="restricting-access-to-logic-app-ip-addresses"></a>Restricting access to logic app IP addresses

All calls from logic apps come from a specific set of IP addresses per region. You can add additional filtering to only accept requests from those designated IP addresses. For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).

### <a name="on-premises-connectivity"></a>On-premises connectivity

Logic apps provide integration with several services to provide secure and reliable on-premises communication.

#### <a name="on-premises-data-gateway"></a>On-premises data gateway

Many of the managed connectors from logic apps provide secure connectivity to on-premises systems, including File System, SQL, SharePoint, DB2, and more.  The gateway uses encrypted channels via Azure Service Bus to relay data on-premises, and all traffic originates from secure outbound traffic from the gateway agent.  More details on how the gateway works [in this article](logic-apps-gateway-install.md#how-the-gateway-works).

#### <a name="azure-api-management"></a>Azure API Management

[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication to on-premises systems. In the Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access to on-premises systems.

#### <a name="hybrid-connections-from-azure-app-service"></a>Hybrid connections from Azure App Service

You can use the on-premises hybrid connection feature for Azure API and Web apps to communicate on-premises.  Details on hybrid connections and how to configure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="next-steps"></a>Next steps
[Create a deployment template](logic-apps-create-deploy-template.md)  
[Exception handling](logic-apps-exception-handling.md)  
[Monitor your logic apps](logic-apps-monitor-your-logic-apps.md)  
[Diagnosing logic app failures and issues](logic-apps-diagnosing-failures.md)  
