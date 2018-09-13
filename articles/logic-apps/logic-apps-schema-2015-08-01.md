---
title: Schema updates for August-1-2015 preview - Azure Logic Apps | Microsoft Docs
description: Updated schema version 2015-08-01-preview for logic app definitions in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: stepsic-microsoft-com
ms.author: stepsic
ms.reviewer: klam, estfan, LADocs
ms.assetid: 0d03a4d4-e8a8-4c81-aed5-bfd2a28c7f0c
ms.topic: article
ms.date: 05/31/2016
ms.openlocfilehash: dd05543c2a727f010432ecb54c2dc3e77a245de4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783450"
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="ce930-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span><span class="sxs-lookup"><span data-stu-id="ce930-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="ce930-104">This schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span><span class="sxs-lookup"><span data-stu-id="ce930-104">This schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

* <span data-ttu-id="ce930-105">The **APIApp** action type is now named [**APIConnection**](#api-connections).</span><span class="sxs-lookup"><span data-stu-id="ce930-105">The **APIApp** action type is now named [**APIConnection**](#api-connections).</span></span>
* <span data-ttu-id="ce930-106">The **Repeat** action is now named [**Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="ce930-106">The **Repeat** action is now named [**Foreach**](#foreach).</span></span>
* <span data-ttu-id="ce930-107">The [**HTTP Listener** API App](#http-listener) is no longer required.</span><span class="sxs-lookup"><span data-stu-id="ce930-107">The [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
* <span data-ttu-id="ce930-108">Calling child workflows uses a [new schema](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="ce930-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>

## <a name="move-to-api-connections"></a><span data-ttu-id="ce930-109">Move to API connections</span><span class="sxs-lookup"><span data-stu-id="ce930-109">Move to API connections</span></span>

<span data-ttu-id="ce930-110">The biggest change is that you no longer have to deploy API Apps into your Azure subscription so that you can use APIs.</span><span class="sxs-lookup"><span data-stu-id="ce930-110">The biggest change is that you no longer have to deploy API Apps into your Azure subscription so that you can use APIs.</span></span> <span data-ttu-id="ce930-111">Here are the ways that you can use APIs:</span><span class="sxs-lookup"><span data-stu-id="ce930-111">Here are the ways that you can use APIs:</span></span>

* <span data-ttu-id="ce930-112">Managed APIs</span><span class="sxs-lookup"><span data-stu-id="ce930-112">Managed APIs</span></span>
* <span data-ttu-id="ce930-113">Your custom Web APIs</span><span class="sxs-lookup"><span data-stu-id="ce930-113">Your custom Web APIs</span></span>

<span data-ttu-id="ce930-114">Each way is handled slightly differently because their management and hosting models are different.</span><span class="sxs-lookup"><span data-stu-id="ce930-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="ce930-115">One advantage of this model is you're no longer constrained to resources that are deployed in your Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="ce930-115">One advantage of this model is you're no longer constrained to resources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="ce930-116">Managed APIs</span><span class="sxs-lookup"><span data-stu-id="ce930-116">Managed APIs</span></span>

<span data-ttu-id="ce930-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span><span class="sxs-lookup"><span data-stu-id="ce930-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="ce930-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration, also called a *connection*.</span><span class="sxs-lookup"><span data-stu-id="ce930-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration, also called a *connection*.</span></span>

<span data-ttu-id="ce930-119">For example, when you use Office 365, you must create a connection that includes your Office 365 sign-in token.</span><span class="sxs-lookup"><span data-stu-id="ce930-119">For example, when you use Office 365, you must create a connection that includes your Office 365 sign-in token.</span></span> <span data-ttu-id="ce930-120">Your token is securely stored and refreshed so that your logic app can always call the Office 365 API.</span><span class="sxs-lookup"><span data-stu-id="ce930-120">Your token is securely stored and refreshed so that your logic app can always call the Office 365 API.</span></span> <span data-ttu-id="ce930-121">If you want to connect to your SQL or FTP server, you must create a connection that has the connection string.</span><span class="sxs-lookup"><span data-stu-id="ce930-121">If you want to connect to your SQL or FTP server, you must create a connection that has the connection string.</span></span> 

<span data-ttu-id="ce930-122">In this definition, these actions are called `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="ce930-122">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="ce930-123">Here is an example of a connection that calls Office 365 to send an email:</span><span class="sxs-lookup"><span data-stu-id="ce930-123">Here is an example of a connection that calls Office 365 to send an email:</span></span>

``` json
{
   "actions": {
      "Send_an_email": {
         "type": "ApiConnection",
         "inputs": {
            "host": {
               "api": {
                  "runtimeUrl": "https://msmanaged-na.azure-apim.net/apim/office365"
               },
               "connection": {
                  "name": "@parameters('$connections')['shared_office365']['connectionId']"
               }
            },
            "method": "POST",
            "body": {
               "Subject": "Reminder",
               "Body": "Don't forget!",
               "To": "me@contoso.com"
            },
            "path": "/Mail"
         }
      }
   }
}
```

<span data-ttu-id="ce930-124">The `host` object is a part of the inputs that is unique to API connections, and contains these parts: `api` and `connection`.</span><span class="sxs-lookup"><span data-stu-id="ce930-124">The `host` object is a part of the inputs that is unique to API connections, and contains these parts: `api` and `connection`.</span></span> <span data-ttu-id="ce930-125">The `api` object specifies the runtime URL for where that managed API is hosted.</span><span class="sxs-lookup"><span data-stu-id="ce930-125">The `api` object specifies the runtime URL for where that managed API is hosted.</span></span> <span data-ttu-id="ce930-126">You can see all the available managed APIs by calling `GET https://management.azure.com/subscriptions/<Azure-subscription-ID>/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="ce930-126">You can see all the available managed APIs by calling `GET https://management.azure.com/subscriptions/<Azure-subscription-ID>/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="ce930-127">When you use an API, that API might or might not have defined any *connection parameters*.</span><span class="sxs-lookup"><span data-stu-id="ce930-127">When you use an API, that API might or might not have defined any *connection parameters*.</span></span> <span data-ttu-id="ce930-128">So, if the API doesn't define these parameters, no connection is required.</span><span class="sxs-lookup"><span data-stu-id="ce930-128">So, if the API doesn't define these parameters, no connection is required.</span></span> <span data-ttu-id="ce930-129">If the API does define these parameters, you must create a connection with a specified name.</span><span class="sxs-lookup"><span data-stu-id="ce930-129">If the API does define these parameters, you must create a connection with a specified name.</span></span>  
<span data-ttu-id="ce930-130">You then reference that name in the `connection` object inside the `host` object.</span><span class="sxs-lookup"><span data-stu-id="ce930-130">You then reference that name in the `connection` object inside the `host` object.</span></span> <span data-ttu-id="ce930-131">To create a connection in a resource group, call this method:</span><span class="sxs-lookup"><span data-stu-id="ce930-131">To create a connection in a resource group, call this method:</span></span>

```
PUT https://management.azure.com/subscriptions/<Azure-subscription-ID>/resourceGroups/<Azure-resource-group-name>/providers/Microsoft.Web/connections/<name>?api-version=2015-08-01-preview
```

<span data-ttu-id="ce930-132">With the following body:</span><span class="sxs-lookup"><span data-stu-id="ce930-132">With the following body:</span></span>

``` json
{
   "properties": {
      "api": {
         "id": "/subscriptions/<Azure-subscription-ID>/providers/Microsoft.Web/managedApis/azureblob"
      },
      "parameterValues": {
         "accountName": "<Azure-storage-account-name-with-different-parameters-for-each-API>"
      }
   },
   "location": "<logic-app-location>"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="ce930-133">Deploy managed APIs in an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="ce930-133">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="ce930-134">You can create a full app in an Azure Resource Manager template as long as interactive sign-in isn't required.</span><span class="sxs-lookup"><span data-stu-id="ce930-134">You can create a full app in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="ce930-135">If sign-in is required, you can set up everything with the Azure Resource Manager template, but you still have to visit the Azure portal to authorize the connections.</span><span class="sxs-lookup"><span data-stu-id="ce930-135">If sign-in is required, you can set up everything with the Azure Resource Manager template, but you still have to visit the Azure portal to authorize the connections.</span></span> 

``` json
"resources": [ {
   "apiVersion": "2015-08-01-preview",
   "name": "azureblob",
   "type": "Microsoft.Web/connections",
   "location": "[resourceGroup().location]",
   "properties": {
      "api": {
         "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
      },
      "parameterValues": {
         "accountName": "[parameters('storageAccountName')]",
         "accessKey": "[parameters('storageAccountKey')]"
      }
    },
},
{
   "type": "Microsoft.Logic/workflows",
   "apiVersion": "2015-08-01-preview",
   "name": "[parameters('logicAppName')]",
   "location": "[resourceGroup().location]",
   "dependsOn": ["[resourceId('Microsoft.Web/connections', 'azureblob')]"],
   "properties": {
      "sku": {
         "name": "[parameters('sku')]",
         "plan": {
            "id": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('svcPlanName'))]"
         }
      },
      "parameters": {
         "$connections": {
             "value": {
                  "azureblob": {
                     "connectionId": "[concat(resourceGroup().id,'/providers/Microsoft.Web/connections/azureblob')]",
                     "connectionName": "azureblob",
                     "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
                  }
             }
         }
      },
      "definition": {
         "$schema": "https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
            "type": "Object",
            "$connections": {
               "defaultValue": {},
 
            }
         },
         "triggers": {
            "Recurrence": {
               "type": "Recurrence",
               "recurrence": {
                  "frequency": "Day",
                  "interval": 1
               }
            }
         },
         "actions": {
            "Create_file": {
               "type": "ApiConnection",
               "inputs": {
                  "host": {
                     "api": {
                        "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                     },
                     "connection": {
                       "name": "@parameters('$connections')['azureblob']['connectionId']"
                     }
                  },
                  "method": "POST",
                  "queries": {
                     "folderPath": "[concat('/', parameters('containerName'))]",
                     "name": "helloworld.txt"
                  },
                  "body": "@decodeDataUri('data:, Hello+world!')",
                  "path": "/datasets/default/files"
               },
               "conditions": []
            }
         },
         "outputs": {}
      }
   }
} ]
```

<span data-ttu-id="ce930-136">You can see in this example that the connections are just resources that live in your resource group.</span><span class="sxs-lookup"><span data-stu-id="ce930-136">You can see in this example that the connections are just resources that live in your resource group.</span></span> <span data-ttu-id="ce930-137">They reference the managed APIs available to you in your subscription.</span><span class="sxs-lookup"><span data-stu-id="ce930-137">They reference the managed APIs available to you in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="ce930-138">Your custom Web APIs</span><span class="sxs-lookup"><span data-stu-id="ce930-138">Your custom Web APIs</span></span>

<span data-ttu-id="ce930-139">If you use your own APIs, not Microsoft-managed ones, use the built-in **HTTP** action to call them.</span><span class="sxs-lookup"><span data-stu-id="ce930-139">If you use your own APIs, not Microsoft-managed ones, use the built-in **HTTP** action to call them.</span></span> <span data-ttu-id="ce930-140">For an ideal experience, you should expose a Swagger endpoint for your API.</span><span class="sxs-lookup"><span data-stu-id="ce930-140">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="ce930-141">This endpoint enables the Logic App Designer to render the inputs and outputs for your API.</span><span class="sxs-lookup"><span data-stu-id="ce930-141">This endpoint enables the Logic App Designer to render the inputs and outputs for your API.</span></span> <span data-ttu-id="ce930-142">Without Swagger, the designer can only show the inputs and outputs as opaque JSON objects.</span><span class="sxs-lookup"><span data-stu-id="ce930-142">Without Swagger, the designer can only show the inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="ce930-143">Here is an example showing the new `metadata.apiDefinitionUrl` property:</span><span class="sxs-lookup"><span data-stu-id="ce930-143">Here is an example showing the new `metadata.apiDefinitionUrl` property:</span></span>

``` json
"actions": {
   "mycustomAPI": {
      "type": "Http",
      "metadata": {
         "apiDefinitionUrl": "https://mysite.azurewebsites.net/api/apidef/"  
      },
      "inputs": {
         "uri": "https://mysite.azurewebsites.net/api/getsomedata",
         "method": "GET"
      }
   }
}
```

<span data-ttu-id="ce930-144">If you host your Web API on Azure App Service, your Web API automatically appears in the list of actions available in the designer.</span><span class="sxs-lookup"><span data-stu-id="ce930-144">If you host your Web API on Azure App Service, your Web API automatically appears in the list of actions available in the designer.</span></span> <span data-ttu-id="ce930-145">If not, you have to paste in the URL directly.</span><span class="sxs-lookup"><span data-stu-id="ce930-145">If not, you have to paste in the URL directly.</span></span> <span data-ttu-id="ce930-146">The Swagger endpoint must be unauthenticated to be usable in the Logic App Designer, although you can secure the API itself with whatever methods that Swagger supports.</span><span class="sxs-lookup"><span data-stu-id="ce930-146">The Swagger endpoint must be unauthenticated to be usable in the Logic App Designer, although you can secure the API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="ce930-147">Call deployed API apps with 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="ce930-147">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="ce930-148">If you previously deployed an API App, you can call that app with the **HTTP** action.</span><span class="sxs-lookup"><span data-stu-id="ce930-148">If you previously deployed an API App, you can call that app with the **HTTP** action.</span></span>
<span data-ttu-id="ce930-149">For example, if you use Dropbox to list files, your **2014-12-01-preview** schema version definition might have something like:</span><span class="sxs-lookup"><span data-stu-id="ce930-149">For example, if you use Dropbox to list files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

``` json
"definition": {
   "$schema": "https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json",
   "contentVersion": "1.0.0.0",
   "parameters": {
      "/subscriptions/<Azure-subscription-ID>/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token": {
         "defaultValue": "eyJ0eX...wCn90",
         "type": "String",
         "metadata": {
            "token": {
               "name": "/subscriptions/<Azure-subscription-ID>/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token"
            }
         }
      }
    },
    "actions": {
       "dropboxconnector": {
          "type": "ApiApp",
          "inputs": {
             "apiVersion": "2015-01-14",
             "host": {
                "id": "/subscriptions/<Azure-subscription-ID>/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector",
                "gateway": "https://avdemo.azurewebsites.net"
             },
             "operation": "ListFiles",
             "parameters": {
                "FolderPath": "/myfolder"
             },
             "authentication": {
                "type": "Raw",
                "scheme": "Zumo",
                "parameter": "@parameters('/subscriptions/<Azure-subscription-ID>/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
             }
          }
       }
    }
}
```

<span data-ttu-id="ce930-150">Now, you can now construct the equivalent HTTP action like the following example, while leaving the parameters section for the logic app definition unchanged:</span><span class="sxs-lookup"><span data-stu-id="ce930-150">Now, you can now construct the equivalent HTTP action like the following example, while leaving the parameters section for the logic app definition unchanged:</span></span>

``` json
"actions": {
   "dropboxconnector": {
      "type": "Http",
      "metadata": {
         "apiDefinitionUrl": "https://avdemo.azurewebsites.net/api/service/apidef/dropboxconnector/?api-version=2015-01-14&format=swagger-2.0-standard"  
      },
      "inputs": {
         "uri": "https://avdemo.azurewebsites.net/api/service/invoke/dropboxconnector/ListFiles?api-version=2015-01-14",
         "method": "POST",
         "body": {
            "FolderPath": "/myfolder"
         },
         "authentication": {
            "type": "Raw",
            "scheme": "Zumo",
            "parameter": "@parameters('/subscriptions/<Azure-subscription-ID>/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
         }
      }
   }
}
```

<span data-ttu-id="ce930-151">Walking through these properties one-by-one:</span><span class="sxs-lookup"><span data-stu-id="ce930-151">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="ce930-152">Action property</span><span class="sxs-lookup"><span data-stu-id="ce930-152">Action property</span></span> | <span data-ttu-id="ce930-153">Description</span><span class="sxs-lookup"><span data-stu-id="ce930-153">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="ce930-154">`Http` instead of `APIapp`</span><span class="sxs-lookup"><span data-stu-id="ce930-154">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` | <span data-ttu-id="ce930-155">To use this action in the Logic App Designer, include the metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="ce930-155">To use this action in the Logic App Designer, include the metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` | <span data-ttu-id="ce930-156">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="ce930-156">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` | <span data-ttu-id="ce930-157">Always `POST`</span><span class="sxs-lookup"><span data-stu-id="ce930-157">Always `POST`</span></span> |
| `inputs.body` | <span data-ttu-id="ce930-158">Identical to the API App parameters</span><span class="sxs-lookup"><span data-stu-id="ce930-158">Identical to the API App parameters</span></span> |
| `inputs.authentication` | <span data-ttu-id="ce930-159">Identical to the API App authentication</span><span class="sxs-lookup"><span data-stu-id="ce930-159">Identical to the API App authentication</span></span> |

<span data-ttu-id="ce930-160">This approach should work for all API App actions.</span><span class="sxs-lookup"><span data-stu-id="ce930-160">This approach should work for all API App actions.</span></span> <span data-ttu-id="ce930-161">However, remember that these previous API Apps are no longer supported.</span><span class="sxs-lookup"><span data-stu-id="ce930-161">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="ce930-162">So you should move to one of the two other previous options, a managed API or hosting your custom Web API.</span><span class="sxs-lookup"><span data-stu-id="ce930-162">So you should move to one of the two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>

## <a name="renamed-repeat-to-foreach"></a><span data-ttu-id="ce930-163">Renamed 'repeat' to 'foreach'</span><span class="sxs-lookup"><span data-stu-id="ce930-163">Renamed 'repeat' to 'foreach'</span></span>

<span data-ttu-id="ce930-164">For the previous schema version, we received much customer feedback that the **Repeat** action name was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span><span class="sxs-lookup"><span data-stu-id="ce930-164">For the previous schema version, we received much customer feedback that the **Repeat** action name was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="ce930-165">So, we renamed `repeat` to `foreach`.</span><span class="sxs-lookup"><span data-stu-id="ce930-165">So, we renamed `repeat` to `foreach`.</span></span> <span data-ttu-id="ce930-166">Previously you'd write this action like this example:</span><span class="sxs-lookup"><span data-stu-id="ce930-166">Previously you'd write this action like this example:</span></span>

``` json
"actions": {
   "pingBing": {
      "type": "Http",
      "repeat": "@range(0,2)",
      "inputs": {
         "method": "GET",
         "uri": "https://www.bing.com/search?q=@{repeatItem()}"
      }
   }
}
```

<span data-ttu-id="ce930-167">Now you'd write this version instead:</span><span class="sxs-lookup"><span data-stu-id="ce930-167">Now you'd write this version instead:</span></span>

``` json
"actions": {
   "pingBing": {
      "type": "Http",
      "foreach": "@range(0,2)",
      "inputs": {
         "method": "GET",
         "uri": "https://www.bing.com/search?q=@{item()}"
      }
   }
}
```

<span data-ttu-id="ce930-168">Also, the `repeatItem()` function, which referenced the item that the loop is processing during the current iteration, is now renamed `item()`.</span><span class="sxs-lookup"><span data-stu-id="ce930-168">Also, the `repeatItem()` function, which referenced the item that the loop is processing during the current iteration, is now renamed `item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="ce930-169">Reference outputs from 'foreach'</span><span class="sxs-lookup"><span data-stu-id="ce930-169">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="ce930-170">For simplification, the outputs from `foreach` actions are no longer wrapped in an object named `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="ce930-170">For simplification, the outputs from `foreach` actions are no longer wrapped in an object named `repeatItems`.</span></span> <span data-ttu-id="ce930-171">Also, with these changes, the `repeatItem()`, `repeatBody()`, and `repeatOutputs()` functions are removed.</span><span class="sxs-lookup"><span data-stu-id="ce930-171">Also, with these changes, the `repeatItem()`, `repeatBody()`, and `repeatOutputs()` functions are removed.</span></span>

<span data-ttu-id="ce930-172">So, using the previous `repeat` example, you get these outputs:</span><span class="sxs-lookup"><span data-stu-id="ce930-172">So, using the previous `repeat` example, you get these outputs:</span></span>

``` json
"repeatItems": [ {
   "name": "pingBing",
   "inputs": {
      "uri": "https://www.bing.com/search?q=0",
      "method": "GET"
   },
   "outputs": {
      "headers": { },
      "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
   },
   "status": "Succeeded"
} ]
```

<span data-ttu-id="ce930-173">Now you get these outputs instead:</span><span class="sxs-lookup"><span data-stu-id="ce930-173">Now you get these outputs instead:</span></span>

``` json
[ {
   "name": "pingBing",
      "inputs": {
         "uri": "https://www.bing.com/search?q=0",
         "method": "GET"
      },
      "outputs": {
         "headers": { },
         "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
      },
      "status": "Succeeded"
} ]
```

<span data-ttu-id="ce930-174">Previously, to get the `body` from the action when referencing these outputs:</span><span class="sxs-lookup"><span data-stu-id="ce930-174">Previously, to get the `body` from the action when referencing these outputs:</span></span>

``` json
"actions": {
   "secondAction": {
      "type": "Http",
      "repeat": "@outputs('pingBing').repeatItems",
      "inputs": {
         "method": "POST",
         "uri": "http://www.example.com",
         "body": "@repeatItem().outputs.body"
      }
   }
}
```

<span data-ttu-id="ce930-175">Now you can use this version instead:</span><span class="sxs-lookup"><span data-stu-id="ce930-175">Now you can use this version instead:</span></span>

``` json
"actions": {
   "secondAction": {
      "type": "Http",
      "foreach": "@outputs('pingBing')",
      "inputs": {
         "method": "POST",
         "uri": "http://www.example.com",
         "body": "@item().outputs.body"
      }
   }
}
```

<a name="http-listener"></a>

## <a name="native-http-listener"></a><span data-ttu-id="ce930-176">Native HTTP listener</span><span class="sxs-lookup"><span data-stu-id="ce930-176">Native HTTP listener</span></span>

<span data-ttu-id="ce930-177">The HTTP Listener capabilities are now built in.</span><span class="sxs-lookup"><span data-stu-id="ce930-177">The HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="ce930-178">So you no longer need to deploy an HTTP Listener API App.</span><span class="sxs-lookup"><span data-stu-id="ce930-178">So you no longer need to deploy an HTTP Listener API App.</span></span> <span data-ttu-id="ce930-179">See [the full details for how to make your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="ce930-179">See [the full details for how to make your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="ce930-180">With these changes, we removed the `@accessKeys()` function, which we replaced with the `@listCallbackURL()` function for getting the endpoint when necessary.</span><span class="sxs-lookup"><span data-stu-id="ce930-180">With these changes, we removed the `@accessKeys()` function, which we replaced with the `@listCallbackURL()` function for getting the endpoint when necessary.</span></span> <span data-ttu-id="ce930-181">Also, you must now define at least one trigger in your logic app.</span><span class="sxs-lookup"><span data-stu-id="ce930-181">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="ce930-182">If you want to `/run` the workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="ce930-182">If you want to `/run` the workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>

## <a name="call-child-workflows"></a><span data-ttu-id="ce930-183">Call child workflows</span><span class="sxs-lookup"><span data-stu-id="ce930-183">Call child workflows</span></span>

<span data-ttu-id="ce930-184">Previously, calling child workflows required going to the workflow, getting the access token, and pasting the token in the logic app definition where you want to call that child workflow.</span><span class="sxs-lookup"><span data-stu-id="ce930-184">Previously, calling child workflows required going to the workflow, getting the access token, and pasting the token in the logic app definition where you want to call that child workflow.</span></span> <span data-ttu-id="ce930-185">With the new schema, the Logic Apps engine automatically generates a SAS at runtime for the child workflow so you don't have to paste any secrets into the definition.</span><span class="sxs-lookup"><span data-stu-id="ce930-185">With the new schema, the Logic Apps engine automatically generates a SAS at runtime for the child workflow so you don't have to paste any secrets into the definition.</span></span> <span data-ttu-id="ce930-186">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="ce930-186">Here is an example:</span></span>

``` json
"myNestedWorkflow": {
   "type": "Workflow",
   "inputs": {
      "host": {
         "id": "/subscriptions/<Azure-subscription-ID>/resourceGroups/<Azure-resource-group-name>/providers/Microsoft.Logic/myWorkflow001",
         "triggerName": "myEndpointTrigger"
      },
      "queries": {
         "extrafield": "specialValue"
      },
      "headers": {
         "x-ms-date": "@utcnow()",
         "Content-type": "application/json"
      },
      "body": {
         "contentFieldOne": "value100",
         "anotherField": 10.001
      }
   },
   "conditions": []
}
```

<span data-ttu-id="ce930-187">A second improvement is we are giving the child workflows full access to the incoming request.</span><span class="sxs-lookup"><span data-stu-id="ce930-187">A second improvement is we are giving the child workflows full access to the incoming request.</span></span> <span data-ttu-id="ce930-188">That means that you can pass parameters in the *queries* section and in the *headers* object and that you can fully define the entire body.</span><span class="sxs-lookup"><span data-stu-id="ce930-188">That means that you can pass parameters in the *queries* section and in the *headers* object and that you can fully define the entire body.</span></span>

<span data-ttu-id="ce930-189">Finally, there are required changes to the child workflow.</span><span class="sxs-lookup"><span data-stu-id="ce930-189">Finally, there are required changes to the child workflow.</span></span> <span data-ttu-id="ce930-190">While you could previously call a child workflow directly, now you must define a trigger endpoint in the workflow for the parent to call.</span><span class="sxs-lookup"><span data-stu-id="ce930-190">While you could previously call a child workflow directly, now you must define a trigger endpoint in the workflow for the parent to call.</span></span> <span data-ttu-id="ce930-191">Generally, you would add a trigger that has `manual` type, and then use that trigger in the parent definition.</span><span class="sxs-lookup"><span data-stu-id="ce930-191">Generally, you would add a trigger that has `manual` type, and then use that trigger in the parent definition.</span></span> <span data-ttu-id="ce930-192">Note the `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span><span class="sxs-lookup"><span data-stu-id="ce930-192">Note the `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="ce930-193">Other changes</span><span class="sxs-lookup"><span data-stu-id="ce930-193">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="ce930-194">New 'queries' property</span><span class="sxs-lookup"><span data-stu-id="ce930-194">New 'queries' property</span></span>

<span data-ttu-id="ce930-195">All action types now support a new input called `queries`.</span><span class="sxs-lookup"><span data-stu-id="ce930-195">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="ce930-196">This input can be a structured object, rather than you having to assemble the string by hand.</span><span class="sxs-lookup"><span data-stu-id="ce930-196">This input can be a structured object, rather than you having to assemble the string by hand.</span></span>

### <a name="renamed-parse-function-to-json"></a><span data-ttu-id="ce930-197">Renamed 'parse()' function to 'json()'</span><span class="sxs-lookup"><span data-stu-id="ce930-197">Renamed 'parse()' function to 'json()'</span></span>

<span data-ttu-id="ce930-198">We are adding more content types soon, so we renamed the `parse()` function to `json()`.</span><span class="sxs-lookup"><span data-stu-id="ce930-198">We are adding more content types soon, so we renamed the `parse()` function to `json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="ce930-199">Coming soon: Enterprise Integration APIs</span><span class="sxs-lookup"><span data-stu-id="ce930-199">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="ce930-200">We don't have managed versions yet of the Enterprise Integration APIs, like AS2.</span><span class="sxs-lookup"><span data-stu-id="ce930-200">We don't have managed versions yet of the Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="ce930-201">Meanwhile, you can use your existing deployed BizTalk APIs through the HTTP action.</span><span class="sxs-lookup"><span data-stu-id="ce930-201">Meanwhile, you can use your existing deployed BizTalk APIs through the HTTP action.</span></span> <span data-ttu-id="ce930-202">For details, see "Using your already deployed API apps" in the [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="ce930-202">For details, see "Using your already deployed API apps" in the [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
