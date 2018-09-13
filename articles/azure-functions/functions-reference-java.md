---
title: Java developer reference for Azure Functions | Microsoft Docs
description: Understand how to develop functions with Java.
services: functions
documentationcenter: na
author: rloutlaw
manager: justhe
keywords: azure functions, functions, event processing, webhooks, dynamic compute, serverless architecture, java
ms.service: azure-functions
ms.devlang: java
ms.topic: conceptual
ms.date: 08/10/2018
ms.author: routlaw
ms.openlocfilehash: f0dc471e8875ad0d738fce10421c3586752148b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864517"
---
# <a name="azure-functions-java-developer-guide"></a><span data-ttu-id="791d0-104">Azure Functions Java developer guide</span><span class="sxs-lookup"><span data-stu-id="791d0-104">Azure Functions Java developer guide</span></span>

[!INCLUDE [functions-java-preview-note](../../includes/functions-java-preview-note.md)]

## <a name="programming-model"></a><span data-ttu-id="791d0-105">Programming model</span><span class="sxs-lookup"><span data-stu-id="791d0-105">Programming model</span></span> 

<span data-ttu-id="791d0-106">Your Azure function should be a stateless class method that processes input and produces output.</span><span class="sxs-lookup"><span data-stu-id="791d0-106">Your Azure function should be a stateless class method that processes input and produces output.</span></span> <span data-ttu-id="791d0-107">Although you can write instance methods, your function must not depend on any instance fields of the class.</span><span class="sxs-lookup"><span data-stu-id="791d0-107">Although you can write instance methods, your function must not depend on any instance fields of the class.</span></span> <span data-ttu-id="791d0-108">All function methods must have a `public` access modifier.</span><span class="sxs-lookup"><span data-stu-id="791d0-108">All function methods must have a `public` access modifier.</span></span>

<span data-ttu-id="791d0-109">You can put more than one function in a project.</span><span class="sxs-lookup"><span data-stu-id="791d0-109">You can put more than one function in a project.</span></span> <span data-ttu-id="791d0-110">Avoid putting your functions into separate jars.</span><span class="sxs-lookup"><span data-stu-id="791d0-110">Avoid putting your functions into separate jars.</span></span>

## <a name="triggers-and-annotations"></a><span data-ttu-id="791d0-111">Triggers and annotations</span><span class="sxs-lookup"><span data-stu-id="791d0-111">Triggers and annotations</span></span>

 <span data-ttu-id="791d0-112">Azure functions are invoked by a trigger, such as an HTTP request, a timer, or an update to data.</span><span class="sxs-lookup"><span data-stu-id="791d0-112">Azure functions are invoked by a trigger, such as an HTTP request, a timer, or an update to data.</span></span> <span data-ttu-id="791d0-113">Your function needs to process that trigger and any other inputs to produce one or more outputs.</span><span class="sxs-lookup"><span data-stu-id="791d0-113">Your function needs to process that trigger and any other inputs to produce one or more outputs.</span></span>

<span data-ttu-id="791d0-114">Use the Java annotations included in the [com.microsoft.azure.functions.annotation.\*](/java/api/com.microsoft.azure.functions.annotation) package to bind input and outputs to your methods.</span><span class="sxs-lookup"><span data-stu-id="791d0-114">Use the Java annotations included in the [com.microsoft.azure.functions.annotation.\*](/java/api/com.microsoft.azure.functions.annotation) package to bind input and outputs to your methods.</span></span> <span data-ttu-id="791d0-115">Sample code using the annotations is available in the [Java reference docs](/java/api/com.microsoft.azure.functions.annotation) for each annotation and in the Azure Functions binding reference documentation, such as the one for [HTTP triggers](/azure/azure-functions/functions-bindings-http-webhook).</span><span class="sxs-lookup"><span data-stu-id="791d0-115">Sample code using the annotations is available in the [Java reference docs](/java/api/com.microsoft.azure.functions.annotation) for each annotation and in the Azure Functions binding reference documentation, such as the one for [HTTP triggers](/azure/azure-functions/functions-bindings-http-webhook).</span></span>

<span data-ttu-id="791d0-116">Trigger inputs and outputs can also be defined in the [function.json](/azure/azure-functions/functions-reference#function-code) for your function instead of through annotations.</span><span class="sxs-lookup"><span data-stu-id="791d0-116">Trigger inputs and outputs can also be defined in the [function.json](/azure/azure-functions/functions-reference#function-code) for your function instead of through annotations.</span></span> <span data-ttu-id="791d0-117">Using `function.json` instead of annotations in this way is not recommended.</span><span class="sxs-lookup"><span data-stu-id="791d0-117">Using `function.json` instead of annotations in this way is not recommended.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="791d0-118">You must configure an Azure Storage account in your [local.settings.json](/azure/azure-functions/functions-run-local#local-settings-file) to run Azure Storage Blob, Queue, or Table triggers locally.</span><span class="sxs-lookup"><span data-stu-id="791d0-118">You must configure an Azure Storage account in your [local.settings.json](/azure/azure-functions/functions-run-local#local-settings-file) to run Azure Storage Blob, Queue, or Table triggers locally.</span></span>

<span data-ttu-id="791d0-119">Example using annotations:</span><span class="sxs-lookup"><span data-stu-id="791d0-119">Example using annotations:</span></span>

```java
public class Function {
    public String echo(@HttpTrigger(name = "req", 
      methods = {"post"},  authLevel = AuthorizationLevel.ANONYMOUS) 
        String req, ExecutionContext context) {
        return String.format(req);
    }
}
```

<span data-ttu-id="791d0-120">The same function written without annotations:</span><span class="sxs-lookup"><span data-stu-id="791d0-120">The same function written without annotations:</span></span>

```java
package com.example;

public class MyClass {
    public static String echo(String in) {
        return in;
    }
}
```

<span data-ttu-id="791d0-121">with the corresponding `function.json`:</span><span class="sxs-lookup"><span data-stu-id="791d0-121">with the corresponding `function.json`:</span></span>

```json
{
  "scriptFile": "azure-functions-example.jar",
  "entryPoint": "com.example.MyClass.echo",
  "bindings": [
    {
      "type": "httpTrigger",
      "name": "req",
      "direction": "in",
      "authLevel": "anonymous",
      "methods": [ "post" ]
    },
    {
      "type": "http",
      "name": "$return",
      "direction": "out"
    }
  ]
}

```

## <a name="third-party-libraries"></a><span data-ttu-id="791d0-122">Third-party libraries</span><span class="sxs-lookup"><span data-stu-id="791d0-122">Third-party libraries</span></span> 

<span data-ttu-id="791d0-123">Azure Functions supports the use of third-party libraries.</span><span class="sxs-lookup"><span data-stu-id="791d0-123">Azure Functions supports the use of third-party libraries.</span></span> <span data-ttu-id="791d0-124">By default, all dependencies specified in your project `pom.xml` file will be automatically bundled during the `mvn package` goal.</span><span class="sxs-lookup"><span data-stu-id="791d0-124">By default, all dependencies specified in your project `pom.xml` file will be automatically bundled during the `mvn package` goal.</span></span> <span data-ttu-id="791d0-125">For libraries not specified as dependencies in the `pom.xml` file, place them in a `lib` directory in the function's root directory.</span><span class="sxs-lookup"><span data-stu-id="791d0-125">For libraries not specified as dependencies in the `pom.xml` file, place them in a `lib` directory in the function's root directory.</span></span> <span data-ttu-id="791d0-126">Dependencies placed in the `lib` directory will be added to the system class loader at runtime.</span><span class="sxs-lookup"><span data-stu-id="791d0-126">Dependencies placed in the `lib` directory will be added to the system class loader at runtime.</span></span>

## <a name="data-type-support"></a><span data-ttu-id="791d0-127">Data type support</span><span class="sxs-lookup"><span data-stu-id="791d0-127">Data type support</span></span>

<span data-ttu-id="791d0-128">You can use any data types in Java for the input and output data, including native types; customized Java types and specialized Azure types defined in `azure-functions-java-library` package.</span><span class="sxs-lookup"><span data-stu-id="791d0-128">You can use any data types in Java for the input and output data, including native types; customized Java types and specialized Azure types defined in `azure-functions-java-library` package.</span></span> <span data-ttu-id="791d0-129">The Azure Functions runtime attempts convert the input received into the type requested by your code.</span><span class="sxs-lookup"><span data-stu-id="791d0-129">The Azure Functions runtime attempts convert the input received into the type requested by your code.</span></span>

### <a name="strings"></a><span data-ttu-id="791d0-130">Strings</span><span class="sxs-lookup"><span data-stu-id="791d0-130">Strings</span></span>

<span data-ttu-id="791d0-131">Values passed into function methods will be cast to Strings if the corresponding input parameter type for the function is of type `String`.</span><span class="sxs-lookup"><span data-stu-id="791d0-131">Values passed into function methods will be cast to Strings if the corresponding input parameter type for the function is of type `String`.</span></span> 

### <a name="plain-old-java-objects-pojos"></a><span data-ttu-id="791d0-132">Plain old Java objects (POJOs)</span><span class="sxs-lookup"><span data-stu-id="791d0-132">Plain old Java objects (POJOs)</span></span>

<span data-ttu-id="791d0-133">Strings formatted with JSON will be cast to Java types if the input signature of the function expects that Java type.</span><span class="sxs-lookup"><span data-stu-id="791d0-133">Strings formatted with JSON will be cast to Java types if the input signature of the function expects that Java type.</span></span> <span data-ttu-id="791d0-134">This conversion allows you to pass in JSON and work with Java types.</span><span class="sxs-lookup"><span data-stu-id="791d0-134">This conversion allows you to pass in JSON and work with Java types.</span></span>

<span data-ttu-id="791d0-135">POJO types used as inputs to functions must the same `public` access modifier as the function methods they are being used in.</span><span class="sxs-lookup"><span data-stu-id="791d0-135">POJO types used as inputs to functions must the same `public` access modifier as the function methods they are being used in.</span></span> <span data-ttu-id="791d0-136">You don't have to declare POJO class fields `public`.</span><span class="sxs-lookup"><span data-stu-id="791d0-136">You don't have to declare POJO class fields `public`.</span></span> <span data-ttu-id="791d0-137">For example, a JSON string `{ "x": 3 }` is able to be converted to the following POJO type:</span><span class="sxs-lookup"><span data-stu-id="791d0-137">For example, a JSON string `{ "x": 3 }` is able to be converted to the following POJO type:</span></span>

```Java
public class MyData {
    private int x;
}
```

### <a name="binary-data"></a><span data-ttu-id="791d0-138">Binary data</span><span class="sxs-lookup"><span data-stu-id="791d0-138">Binary data</span></span>

<span data-ttu-id="791d0-139">Binary data is represented as a `byte[]` in your Azure functions code.</span><span class="sxs-lookup"><span data-stu-id="791d0-139">Binary data is represented as a `byte[]` in your Azure functions code.</span></span> <span data-ttu-id="791d0-140">Bind binary inputs or outputs to your functions by setting the `dataType` field in your function.json to `binary`:</span><span class="sxs-lookup"><span data-stu-id="791d0-140">Bind binary inputs or outputs to your functions by setting the `dataType` field in your function.json to `binary`:</span></span>

```json
 {
  "scriptFile": "azure-functions-example.jar",
  "entryPoint": "com.example.MyClass.echo",
  "bindings": [
    {
      "type": "blob",
      "name": "content",
      "direction": "in",
      "dataType": "binary",
      "path": "container/myfile.bin",
      "connection": "ExampleStorageAccount"
    },
  ]
}
```

<span data-ttu-id="791d0-141">Then use it in your function code:</span><span class="sxs-lookup"><span data-stu-id="791d0-141">Then use it in your function code:</span></span>

```java
// Class definition and imports are omitted here
public static String echoLength(byte[] content) {
}
```

<span data-ttu-id="791d0-142">Empty input values could be `null` as your functions argument, but a recommended way to deal with potential empty values is to use `Optional<T>`.</span><span class="sxs-lookup"><span data-stu-id="791d0-142">Empty input values could be `null` as your functions argument, but a recommended way to deal with potential empty values is to use `Optional<T>`.</span></span>


## <a name="function-method-overloading"></a><span data-ttu-id="791d0-143">Function method overloading</span><span class="sxs-lookup"><span data-stu-id="791d0-143">Function method overloading</span></span>

<span data-ttu-id="791d0-144">You are allowed to overload function methods with the same name but with different types.</span><span class="sxs-lookup"><span data-stu-id="791d0-144">You are allowed to overload function methods with the same name but with different types.</span></span> <span data-ttu-id="791d0-145">For example, you can have both `String echo(String s)` and `String echo(MyType s)` in a class.</span><span class="sxs-lookup"><span data-stu-id="791d0-145">For example, you can have both `String echo(String s)` and `String echo(MyType s)` in a class.</span></span> <span data-ttu-id="791d0-146">Azure Functions decides which method to invoke based on the input type (for HTTP input, MIME type `text/plain` leads to `String` while `application/json` represents `MyType`).</span><span class="sxs-lookup"><span data-stu-id="791d0-146">Azure Functions decides which method to invoke based on the input type (for HTTP input, MIME type `text/plain` leads to `String` while `application/json` represents `MyType`).</span></span>

## <a name="inputs"></a><span data-ttu-id="791d0-147">Inputs</span><span class="sxs-lookup"><span data-stu-id="791d0-147">Inputs</span></span>

<span data-ttu-id="791d0-148">Input are divided into two categories in Azure Functions: one is the trigger input and the other is the additional input.</span><span class="sxs-lookup"><span data-stu-id="791d0-148">Input are divided into two categories in Azure Functions: one is the trigger input and the other is the additional input.</span></span> <span data-ttu-id="791d0-149">Although they are different in `function.json`, the usage is identical in Java code.</span><span class="sxs-lookup"><span data-stu-id="791d0-149">Although they are different in `function.json`, the usage is identical in Java code.</span></span> <span data-ttu-id="791d0-150">Let's take the following code snippet as an example:</span><span class="sxs-lookup"><span data-stu-id="791d0-150">Let's take the following code snippet as an example:</span></span>

```java
package com.example;

import com.microsoft.azure.functions.annotation.*;

public class MyClass {
    @FunctionName("echo")
    public static String echo(
        @HttpTrigger(name = "req", methods = { "put" }, authLevel = AuthorizationLevel.ANONYMOUS, route = "items/{id}") String in,
        @TableInput(name = "item", tableName = "items", partitionKey = "Example", rowKey = "{id}", connection = "AzureWebJobsStorage") MyObject obj
    ) {
        return "Hello, " + in + " and " + obj.getKey() + ".";
    }

    public static class MyObject {
        public String getKey() { return this.RowKey; }
        private String RowKey;
    }
}
```

<span data-ttu-id="791d0-151">When this function is triggered, the HTTP request is passed to the function by `String in`.</span><span class="sxs-lookup"><span data-stu-id="791d0-151">When this function is triggered, the HTTP request is passed to the function by `String in`.</span></span> <span data-ttu-id="791d0-152">An entry will be retrieved from the Azure Table Storage based on the ID in the route URL and made avaialble as `obj` in the function body.</span><span class="sxs-lookup"><span data-stu-id="791d0-152">An entry will be retrieved from the Azure Table Storage based on the ID in the route URL and made avaialble as `obj` in the function body.</span></span>

## <a name="outputs"></a><span data-ttu-id="791d0-153">Outputs</span><span class="sxs-lookup"><span data-stu-id="791d0-153">Outputs</span></span>

<span data-ttu-id="791d0-154">Outputs can be expressed both in return value or output parameters.</span><span class="sxs-lookup"><span data-stu-id="791d0-154">Outputs can be expressed both in return value or output parameters.</span></span> <span data-ttu-id="791d0-155">If there is only one output, you are recommended to use the return value.</span><span class="sxs-lookup"><span data-stu-id="791d0-155">If there is only one output, you are recommended to use the return value.</span></span> <span data-ttu-id="791d0-156">For multiple outputs, you have to use output parameters.</span><span class="sxs-lookup"><span data-stu-id="791d0-156">For multiple outputs, you have to use output parameters.</span></span>

<span data-ttu-id="791d0-157">Return value is the simplest form of output, you just return the value of any type, and Azure Functions runtime will try to marshal it back to the actual type (such as an HTTP response).</span><span class="sxs-lookup"><span data-stu-id="791d0-157">Return value is the simplest form of output, you just return the value of any type, and Azure Functions runtime will try to marshal it back to the actual type (such as an HTTP response).</span></span>  <span data-ttu-id="791d0-158">You could apply any output annotations to the function method (the name property of the annotation has to be $return) to define the return value output.</span><span class="sxs-lookup"><span data-stu-id="791d0-158">You could apply any output annotations to the function method (the name property of the annotation has to be $return) to define the return value output.</span></span>

<span data-ttu-id="791d0-159">To produce multiple output values, use `OutputBinding<T>` type defined in the `azure-functions-java-library` package.</span><span class="sxs-lookup"><span data-stu-id="791d0-159">To produce multiple output values, use `OutputBinding<T>` type defined in the `azure-functions-java-library` package.</span></span> <span data-ttu-id="791d0-160">If you need to make an HTTP response and push a message to a queue as well, you can write something like:</span><span class="sxs-lookup"><span data-stu-id="791d0-160">If you need to make an HTTP response and push a message to a queue as well, you can write something like:</span></span>

<span data-ttu-id="791d0-161">For example, a blob content copying function could be defined as the following code.</span><span class="sxs-lookup"><span data-stu-id="791d0-161">For example, a blob content copying function could be defined as the following code.</span></span> <span data-ttu-id="791d0-162">`@StorageAccount` annotation is used here to prevent the duplicating of the connection property for both `@BlobTrigger` and `@BlobOutput`.</span><span class="sxs-lookup"><span data-stu-id="791d0-162">`@StorageAccount` annotation is used here to prevent the duplicating of the connection property for both `@BlobTrigger` and `@BlobOutput`.</span></span>

```java
package com.example;

import com.microsoft.azure.functions.annotation.*;

public class MyClass {
    @FunctionName("copy")
    @StorageAccount("AzureWebJobsStorage")
    @BlobOutput(name = "$return", path = "samples-output-java/{name}")
    public static String copy(@BlobTrigger(name = "blob", path = "samples-input-java/{name}") String content) {
        return content;
    }
}
```

<span data-ttu-id="791d0-163">Use `OutputBinding<byte[]`>  to make a binary output value (for parameters); for return values, just use `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="791d0-163">Use `OutputBinding<byte[]`>  to make a binary output value (for parameters); for return values, just use `byte[]`.</span></span>

## <a name="specialized-types"></a><span data-ttu-id="791d0-164">Specialized Types</span><span class="sxs-lookup"><span data-stu-id="791d0-164">Specialized Types</span></span>

<span data-ttu-id="791d0-165">Sometimes a function must have detailed control over inputs and outputs.</span><span class="sxs-lookup"><span data-stu-id="791d0-165">Sometimes a function must have detailed control over inputs and outputs.</span></span> <span data-ttu-id="791d0-166">Specialized types in the `azure-functions-java-core` package are provided for you to manipulate request information and tailor the return status of an HTTP trigger:</span><span class="sxs-lookup"><span data-stu-id="791d0-166">Specialized types in the `azure-functions-java-core` package are provided for you to manipulate request information and tailor the return status of an HTTP trigger:</span></span>

| <span data-ttu-id="791d0-167">Specialized Type</span><span class="sxs-lookup"><span data-stu-id="791d0-167">Specialized Type</span></span>      |       <span data-ttu-id="791d0-168">Target</span><span class="sxs-lookup"><span data-stu-id="791d0-168">Target</span></span>        | <span data-ttu-id="791d0-169">Typical Usage</span><span class="sxs-lookup"><span data-stu-id="791d0-169">Typical Usage</span></span>                  |
| --------------------- | :-----------------: | ------------------------------ |
| `HttpRequestMessage<T>`  |    <span data-ttu-id="791d0-170">HTTP Trigger</span><span class="sxs-lookup"><span data-stu-id="791d0-170">HTTP Trigger</span></span>     | <span data-ttu-id="791d0-171">Get method, headers, or queries</span><span class="sxs-lookup"><span data-stu-id="791d0-171">Get method, headers, or queries</span></span> |
| `HttpResponseMessage<T>` | <span data-ttu-id="791d0-172">HTTP Output Binding</span><span class="sxs-lookup"><span data-stu-id="791d0-172">HTTP Output Binding</span></span> | <span data-ttu-id="791d0-173">Return status other than 200</span><span class="sxs-lookup"><span data-stu-id="791d0-173">Return status other than 200</span></span>   |

> [!NOTE] 
> <span data-ttu-id="791d0-174">You can also use `@BindingName` annotation to get HTTP headers and queries.</span><span class="sxs-lookup"><span data-stu-id="791d0-174">You can also use `@BindingName` annotation to get HTTP headers and queries.</span></span> <span data-ttu-id="791d0-175">For example, `@BindingName("name") String query` iterates the HTTP request headers and queries and pass that value to the method.</span><span class="sxs-lookup"><span data-stu-id="791d0-175">For example, `@BindingName("name") String query` iterates the HTTP request headers and queries and pass that value to the method.</span></span> <span data-ttu-id="791d0-176">For example,  `query` will be `"test"` if the request URL is `http://example.org/api/echo?name=test`.</span><span class="sxs-lookup"><span data-stu-id="791d0-176">For example,  `query` will be `"test"` if the request URL is `http://example.org/api/echo?name=test`.</span></span>

### <a name="metadata"></a><span data-ttu-id="791d0-177">Metadata</span><span class="sxs-lookup"><span data-stu-id="791d0-177">Metadata</span></span>

<span data-ttu-id="791d0-178">Metadata comes from different sources, like HTTP headers, HTTP queries, and [trigger metadata](/azure/azure-functions/functions-triggers-bindings#trigger-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="791d0-178">Metadata comes from different sources, like HTTP headers, HTTP queries, and [trigger metadata](/azure/azure-functions/functions-triggers-bindings#trigger-metadata-properties).</span></span> <span data-ttu-id="791d0-179">Use the `@BindingName` annotation together with the metadata name to get the value.</span><span class="sxs-lookup"><span data-stu-id="791d0-179">Use the `@BindingName` annotation together with the metadata name to get the value.</span></span>

<span data-ttu-id="791d0-180">For example, the `queryValue` in the following code snippet will be `"test"` if the requested URL is `http://{example.host}/api/metadata?name=test`.</span><span class="sxs-lookup"><span data-stu-id="791d0-180">For example, the `queryValue` in the following code snippet will be `"test"` if the requested URL is `http://{example.host}/api/metadata?name=test`.</span></span>

```Java
package com.example;

import java.util.Optional;
import com.microsoft.azure.functions.annotation.*;


public class MyClass {
    @FunctionName("metadata")
    public static String metadata(
        @HttpTrigger(name = "req", methods = { "get", "post" }, authLevel = AuthorizationLevel.ANONYMOUS) Optional<String> body,
        @BindingName("name") String queryValue
    ) {
        return body.orElse(queryValue);
    }
}
```

## <a name="execution-context"></a><span data-ttu-id="791d0-181">Execution context</span><span class="sxs-lookup"><span data-stu-id="791d0-181">Execution context</span></span>

<span data-ttu-id="791d0-182">Interact with Azure Functions execution environment via the `ExecutionContext` object defined in the `azure-functions-java-library` package.</span><span class="sxs-lookup"><span data-stu-id="791d0-182">Interact with Azure Functions execution environment via the `ExecutionContext` object defined in the `azure-functions-java-library` package.</span></span> <span data-ttu-id="791d0-183">Use the `ExecutionContext` object to use invocation information and functions runtime information in your code.</span><span class="sxs-lookup"><span data-stu-id="791d0-183">Use the `ExecutionContext` object to use invocation information and functions runtime information in your code.</span></span>

### <a name="custom-logging"></a><span data-ttu-id="791d0-184">Custom logging</span><span class="sxs-lookup"><span data-stu-id="791d0-184">Custom logging</span></span>

<span data-ttu-id="791d0-185">Access to the Functions runtime logger is available through the `ExecutionContext` object.</span><span class="sxs-lookup"><span data-stu-id="791d0-185">Access to the Functions runtime logger is available through the `ExecutionContext` object.</span></span> <span data-ttu-id="791d0-186">This logger is tied to the Azure monitor and allows you to flag warnings and errors encountered during function execution.</span><span class="sxs-lookup"><span data-stu-id="791d0-186">This logger is tied to the Azure monitor and allows you to flag warnings and errors encountered during function execution.</span></span>

<span data-ttu-id="791d0-187">The following example code logs a warning message when the request body received is empty.</span><span class="sxs-lookup"><span data-stu-id="791d0-187">The following example code logs a warning message when the request body received is empty.</span></span>

```java

import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;

public class Function {
    public String echo(@HttpTrigger(name = "req", methods = {"post"}, authLevel = AuthorizationLevel.ANONYMOUS) String req, ExecutionContext context) {
        if (req.isEmpty()) {
            context.getLogger().warning("Empty request body received by function " + context.getFunctionName() + " with invocation " + context.getInvocationId());
        }
        return String.format(req);
    }
}
```

## <a name="view-logs-and-trace"></a><span data-ttu-id="791d0-188">View logs and trace</span><span class="sxs-lookup"><span data-stu-id="791d0-188">View logs and trace</span></span>

<span data-ttu-id="791d0-189">You can use the Azure CLI to stream Java standard out and error logging as well as other application logging.</span><span class="sxs-lookup"><span data-stu-id="791d0-189">You can use the Azure CLI to stream Java standard out and error logging as well as other application logging.</span></span> <span data-ttu-id="791d0-190">First, Configure your Function application to write application logging using the Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="791d0-190">First, Configure your Function application to write application logging using the Azure CLI:</span></span>

```azurecli-interactive
az webapp log config --name functionname --resource-group myResourceGroup --application-logging true
```

<span data-ttu-id="791d0-191">To stream logging output for your Function app using the Azure CLI, open a new command prompt, Bash, or Terminal session and enter the following command:</span><span class="sxs-lookup"><span data-stu-id="791d0-191">To stream logging output for your Function app using the Azure CLI, open a new command prompt, Bash, or Terminal session and enter the following command:</span></span>

```azurecli-interactive
az webapp log tail --name webappname --resource-group myResourceGroup
```
<span data-ttu-id="791d0-192">The [az webapp log tail](/cli/azure/webapp/log) command has options to filter output using the `--provider` option.</span><span class="sxs-lookup"><span data-stu-id="791d0-192">The [az webapp log tail](/cli/azure/webapp/log) command has options to filter output using the `--provider` option.</span></span> 

<span data-ttu-id="791d0-193">To download the log files as a single ZIP file using the Azure CLI, open a new command prompt, Bash, or Terminal session and enter the following command:</span><span class="sxs-lookup"><span data-stu-id="791d0-193">To download the log files as a single ZIP file using the Azure CLI, open a new command prompt, Bash, or Terminal session and enter the following command:</span></span>

```azurecli-interactive
az webapp log download --resource-group resourcegroupname --name functionappname
```

<span data-ttu-id="791d0-194">You must have enabled file system logging in the Azure Portal or Azure CLI before running this command.</span><span class="sxs-lookup"><span data-stu-id="791d0-194">You must have enabled file system logging in the Azure Portal or Azure CLI before running this command.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="791d0-195">Environment variables</span><span class="sxs-lookup"><span data-stu-id="791d0-195">Environment variables</span></span>

<span data-ttu-id="791d0-196">Keep secret information such as keys or tokens out of your source code for security reasons.</span><span class="sxs-lookup"><span data-stu-id="791d0-196">Keep secret information such as keys or tokens out of your source code for security reasons.</span></span> <span data-ttu-id="791d0-197">Use keys and tokens in your function code by reading them from environment variables.</span><span class="sxs-lookup"><span data-stu-id="791d0-197">Use keys and tokens in your function code by reading them from environment variables.</span></span>

<span data-ttu-id="791d0-198">To set environment variables when running Azure Functions locally, you may choose to add these variables to the local.settings.json file.</span><span class="sxs-lookup"><span data-stu-id="791d0-198">To set environment variables when running Azure Functions locally, you may choose to add these variables to the local.settings.json file.</span></span> <span data-ttu-id="791d0-199">If one is not present in the root directory of your function project, you can create one.</span><span class="sxs-lookup"><span data-stu-id="791d0-199">If one is not present in the root directory of your function project, you can create one.</span></span> <span data-ttu-id="791d0-200">Here is what the file should look like:</span><span class="sxs-lookup"><span data-stu-id="791d0-200">Here is what the file should look like:</span></span>

```xml
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "",
    "AzureWebJobsDashboard": ""
  }
}
```

<span data-ttu-id="791d0-201">Each key / value mapping in the `values` map will be made available at runtime as an environment variable, accessible by calling `System.getenv("<keyname>")`, for example, `System.getenv("AzureWebJobsStorage")`.</span><span class="sxs-lookup"><span data-stu-id="791d0-201">Each key / value mapping in the `values` map will be made available at runtime as an environment variable, accessible by calling `System.getenv("<keyname>")`, for example, `System.getenv("AzureWebJobsStorage")`.</span></span> <span data-ttu-id="791d0-202">Adding additional key / value pairs is accepted and recommended practice.</span><span class="sxs-lookup"><span data-stu-id="791d0-202">Adding additional key / value pairs is accepted and recommended practice.</span></span>

> [!NOTE]
> <span data-ttu-id="791d0-203">If this approach is taken, be sure to add the local.settings.json file to your repository ignore file, so that it is not committed.</span><span class="sxs-lookup"><span data-stu-id="791d0-203">If this approach is taken, be sure to add the local.settings.json file to your repository ignore file, so that it is not committed.</span></span>

<span data-ttu-id="791d0-204">With your code now depending on these environment variables, you can sign in to the Azure portal to set the same key / value pairs in your function app settings, so that your code functions equivalently when testing locally and when deployed to Azure.</span><span class="sxs-lookup"><span data-stu-id="791d0-204">With your code now depending on these environment variables, you can sign in to the Azure portal to set the same key / value pairs in your function app settings, so that your code functions equivalently when testing locally and when deployed to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="791d0-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="791d0-205">Next steps</span></span>

<span data-ttu-id="791d0-206">For more information about Azure Function Java development, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="791d0-206">For more information about Azure Function Java development, see the following resources:</span></span>

* [<span data-ttu-id="791d0-207">Best practices for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="791d0-207">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="791d0-208">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="791d0-208">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="791d0-209">Azure Functions triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="791d0-209">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
- <span data-ttu-id="791d0-210">Local development and debug with [Visual Studio Code](https://code.visualstudio.com/docs/java/java-azurefunctions), [IntelliJ](functions-create-maven-intellij.md), and [Eclipse](functions-create-maven-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="791d0-210">Local development and debug with [Visual Studio Code](https://code.visualstudio.com/docs/java/java-azurefunctions), [IntelliJ](functions-create-maven-intellij.md), and [Eclipse](functions-create-maven-eclipse.md).</span></span> 
* [<span data-ttu-id="791d0-211">Remote Debug Java Azure Functions with Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="791d0-211">Remote Debug Java Azure Functions with Visual Studio Code</span></span>](https://code.visualstudio.com/docs/java/java-serverless#_remote-debug-functions-running-in-the-cloud)
* <span data-ttu-id="791d0-212">[Maven plugin for Azure Functions](https://github.com/Microsoft/azure-maven-plugins/blob/develop/azure-functions-maven-plugin/README.md) - Streamline function creation through the `azure-functions:add` goal and prepare a staging directory for [ZIP file deployment](deployment-zip-push.md).</span><span class="sxs-lookup"><span data-stu-id="791d0-212">[Maven plugin for Azure Functions](https://github.com/Microsoft/azure-maven-plugins/blob/develop/azure-functions-maven-plugin/README.md) - Streamline function creation through the `azure-functions:add` goal and prepare a staging directory for [ZIP file deployment](deployment-zip-push.md).</span></span>
