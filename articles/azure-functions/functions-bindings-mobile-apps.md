---
title: Mobile Apps bindings for Azure Functions
description: Understand how to use Azure Mobile Apps bindings in Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
keywords: azure functions, functions, event processing, dynamic compute, serverless architecture
ms.service: azure-functions
ms.devlang: multiple
ms.topic: reference
ms.date: 11/21/2017
ms.author: glenga
ms.openlocfilehash: d43032f854aa37f150945c25515c03ec97277b41
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44810302"
---
# <a name="mobile-apps-bindings-for-azure-functions"></a>Mobile Apps bindings for Azure Functions 

This article explains how to work with [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions. Azure Functions supports input and output bindings for Mobile Apps.

The Mobile Apps bindings let you read and update data tables in mobile apps.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="packages---functions-1x"></a>Packages - Functions 1.x

Mobile Apps bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.MobileApps](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps) NuGet package, version 1.x. Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.MobileApps/) GitHub repository.

[!INCLUDE [functions-package](../../includes/functions-package.md)]

## <a name="packages---functions-2x"></a>Packages - Functions 2.x

Mobile Apps bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.MobileApps](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps) NuGet package, version 3.x. Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/) GitHub repository.

[!INCLUDE [functions-package-v2](../../includes/functions-package-v2.md)]

## <a name="input"></a>Input

The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function. In C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.

## <a name="input---example"></a>Input - example

See the language-specific example:

* [C# script (.csx)](#input---c-script-example)
* [JavaScript](#input---javascript-example)

### <a name="input---c-script-example"></a>Input - C# script example

The following example shows a Mobile Apps input binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding. The function is triggered by a queue message that has a record identifier. The function reads the specified record and modifies its `Text` property.

Here's the binding data in the *function.json* file:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```
The [configuration](#input---configuration) section explains these properties.

Here's the C# script code:

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

### <a name="input---javascript"></a>Input - JavaScript

The following example shows a Mobile Apps input binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding. The function is triggered by a queue message that has a record identifier. The function reads the specified record and modifies its `Text` property.

Here's the binding data in the *function.json* file:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```
The [configuration](#input---configuration) section explains these properties.

Here's the JavaScript code:

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

## <a name="input---attributes"></a>Input - attributes

In [C# class libraries](functions-dotnet-class-library.md), use the [MobileTable](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) attribute.

For information about attribute properties that you can configure, see [the following configuration section](#input---configuration).

## <a name="input---configuration"></a>Input - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `MobileTable` attribute.

|function.json property | Attribute property |Description|
|---------|---------|----------------------|
| **type**|| Must be set to "mobileTable"|
| **direction**||Must be set to "in"|
| **name**|| Name of input parameter in function signature.|
|**tableName** |**TableName**|Name of the mobile app's data table|
| **id**| **Id** | The identifier of the record to retrieve. Can be static or based on the trigger that invokes the function. For example, if you use a queue trigger for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve.|
|**connection**|**Connection**|The name of an app setting that has the mobile app's URL. The function uses this URL to construct the required REST operations against your mobile app. Create an app setting in your function app that contains the mobile app's URL, then specify the name of the app setting in the `connection` property in your input binding. The URL looks like `http://<appname>.azurewebsites.net`.
|**apiKey**|**ApiKey**|The name of an app setting that has your mobile app's API key. Provide the API key if you [implement an API key in your Node.js mobile app](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). To provide the key, create an app setting in your function app that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting. |

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

> [!IMPORTANT]
> Don't share the API key with your mobile app clients. It should only be distributed securely to service-side clients, like Azure Functions. Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository. This safeguards your sensitive information.

## <a name="input---usage"></a>Input - usage

In C# functions, when the record with the specified ID is found, it is passed into the named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter. When the record is not found, the parameter value is `null`. 

In JavaScript functions, the record is passed into the `context.bindings.<name>` object. When the record is not found, the parameter value is `null`. 

In C# and F# functions, any changes you make to the input record (input parameter) are automatically sent back to the table when the function exits successfully. You can't modify a record in JavaScript functions.

## <a name="output"></a>Output

Use the Mobile Apps output binding to write a new record to a Mobile Apps table.  

## <a name="output---example"></a>Output - example

See the language-specific example:

* [C#](#output---c-example)
* [C# script (.csx)](#output---c-script-example)
* [JavaScript](#output---javascript-example)

### <a name="output---c-example"></a>Output - C# example

The following example shows a [C# function](functions-dotnet-class-library.md) that is triggered by a queue message and creates a record in a mobile app table.

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
    TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

### <a name="output---c-script-example"></a>Output - C# script example

The following example shows a Mobile Apps output binding in a *function.json* file and a [C# script function](functions-reference-csharp.md) that uses the binding. The function is triggered by a queue message and creates a new record with hard-coded value for the `Text` property.

Here's the binding data in the *function.json* file:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

The [configuration](#output---configuration) section explains these properties.

Here's the C# script code:

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

### <a name="output---javascript-example"></a>Output - JavaScript example

The following example shows a Mobile Apps output binding in a *function.json* file and a [JavaScript function](functions-reference-node.md) that uses the binding. The function is triggered by a queue message and creates a new record with hard-coded value for the `Text` property.

Here's the binding data in the *function.json* file:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

The [configuration](#output---configuration) section explains these properties.

Here's the JavaScript code:

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="output---attributes"></a>Output - attributes

In [C# class libraries](functions-dotnet-class-library.md), use the [MobileTable](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) attribute.

For information about attribute properties that you can configure, see [Output - configuration](#output---configuration). Here's a `MobileTable` attribute example in a method signature:

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
    TraceWriter log)
{
    ...
}
```

For a complete example, see [Output - C# example](#output---c-example).

## <a name="output---configuration"></a>Output - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `MobileTable` attribute.

|function.json property | Attribute property |Description|
|---------|---------|----------------------|
| **type**|| Must be set to "mobileTable"|
| **direction**||Must be set to "out"|
| **name**|| Name of output parameter in function signature.|
|**tableName** |**TableName**|Name of the mobile app's data table|
|**connection**|**MobileAppUriSetting**|The name of an app setting that has the mobile app's URL. The function uses this URL to construct the required REST operations against your mobile app. Create an app setting in your function app that contains the mobile app's URL, then specify the name of the app setting in the `connection` property in your input binding. The URL looks like `http://<appname>.azurewebsites.net`.
|**apiKey**|**ApiKeySetting**|The name of an app setting that has your mobile app's API key. Provide the API key if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). To provide the key, create an app setting in your function app that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting. |

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

> [!IMPORTANT]
> Don't share the API key with your mobile app clients. It should only be distributed securely to service-side clients, like Azure Functions. Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository. This safeguards your sensitive information.

## <a name="output---usage"></a>Output - usage

In C# script functions, use a named output parameter of type `out object` to access the output record. In C# class libraries, the `MobileTable` attribute can be used with any of the following types:

* `ICollector<T>` or `IAsyncCollector<T>`, where `T` is either `JObject` or any type with a `public string Id` property.
* `out JObject`
* `out T` or `out T[]`, where `T` is any Type with a `public string Id` property.

In Node.js functions, use `context.bindings.<name>` to access the output record.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Learn more about Azure functions triggers and bindings](functions-triggers-bindings.md)
