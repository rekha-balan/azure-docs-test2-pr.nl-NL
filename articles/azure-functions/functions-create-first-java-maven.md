---
title: Create your first function in Azure with Java and Maven| Microsoft Docs
description: Create and publish a simple HTTP triggered function to Azure with Java and Maven.
services: functions
documentationcenter: na
author: rloutlaw
manager: justhe
keywords: azure functions, functions, event processing, compute, serverless architecture
ms.service: azure-functions
ms.devlang: java
ms.topic: quickstart
ms.date: 08/10/2018
ms.author: routlaw, glenga
ms.custom: mvc, devcenter
ms.openlocfilehash: 16d6dd6a589256ad98a37465e64e847778d0cc7e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870394"
---
# <a name="create-your-first-function-with-java-and-maven-preview"></a><span data-ttu-id="35a07-104">Create your first function with Java and Maven (Preview)</span><span class="sxs-lookup"><span data-stu-id="35a07-104">Create your first function with Java and Maven (Preview)</span></span>

[!INCLUDE [functions-java-preview-note](../../includes/functions-java-preview-note.md)]

<span data-ttu-id="35a07-105">This quickstart guides through creating a [serverless](https://azure.microsoft.com/overview/serverless-computing/) function project with Maven, testing it locally, and deploying it to Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="35a07-105">This quickstart guides through creating a [serverless](https://azure.microsoft.com/overview/serverless-computing/) function project with Maven, testing it locally, and deploying it to Azure Functions.</span></span> <span data-ttu-id="35a07-106">When you're done, you have a HTTP-triggered function app running in Azure.</span><span class="sxs-lookup"><span data-stu-id="35a07-106">When you're done, you have a HTTP-triggered function app running in Azure.</span></span>

![Access a Hello World function from the command line with cURL](media/functions-create-java-maven/hello-azure.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="35a07-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="35a07-108">Prerequisites</span></span>
<span data-ttu-id="35a07-109">To develop functions app with Java, you must have the following installed:</span><span class="sxs-lookup"><span data-stu-id="35a07-109">To develop functions app with Java, you must have the following installed:</span></span>

-  <span data-ttu-id="35a07-110">[Java Developer Kit](https://www.azul.com/downloads/zulu/), version 8.</span><span class="sxs-lookup"><span data-stu-id="35a07-110">[Java Developer Kit](https://www.azul.com/downloads/zulu/), version 8.</span></span>
-  <span data-ttu-id="35a07-111">[Apache Maven](https://maven.apache.org), version 3.0 or above.</span><span class="sxs-lookup"><span data-stu-id="35a07-111">[Apache Maven](https://maven.apache.org), version 3.0 or above.</span></span>
-  [<span data-ttu-id="35a07-112">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="35a07-112">Azure CLI</span></span>](https://docs.microsoft.com/cli/azure)

> [!IMPORTANT] 
> <span data-ttu-id="35a07-113">The JAVA_HOME environment variable must be set to the install location of the JDK to complete this quickstart.</span><span class="sxs-lookup"><span data-stu-id="35a07-113">The JAVA_HOME environment variable must be set to the install location of the JDK to complete this quickstart.</span></span>

## <a name="install-the-azure-functions-core-tools"></a><span data-ttu-id="35a07-114">Install the Azure Functions Core Tools</span><span class="sxs-lookup"><span data-stu-id="35a07-114">Install the Azure Functions Core Tools</span></span>

<span data-ttu-id="35a07-115">The Azure Functions Core Tools provide a local development environment for writing, running, and debugging Azure Functions from the terminal or command prompt.</span><span class="sxs-lookup"><span data-stu-id="35a07-115">The Azure Functions Core Tools provide a local development environment for writing, running, and debugging Azure Functions from the terminal or command prompt.</span></span> 

<span data-ttu-id="35a07-116">Install [version 2 of the Core Tools](functions-run-local.md#v2) on your local computer before continuing.</span><span class="sxs-lookup"><span data-stu-id="35a07-116">Install [version 2 of the Core Tools](functions-run-local.md#v2) on your local computer before continuing.</span></span>

## <a name="generate-a-new-functions-project"></a><span data-ttu-id="35a07-117">Generate a new Functions project</span><span class="sxs-lookup"><span data-stu-id="35a07-117">Generate a new Functions project</span></span>

<span data-ttu-id="35a07-118">In an empty folder, run the following command to generate the Functions project from a [Maven archetype](https://maven.apache.org/guides/introduction/introduction-to-archetypes.html).</span><span class="sxs-lookup"><span data-stu-id="35a07-118">In an empty folder, run the following command to generate the Functions project from a [Maven archetype](https://maven.apache.org/guides/introduction/introduction-to-archetypes.html).</span></span>

### <a name="linuxmacos"></a><span data-ttu-id="35a07-119">Linux/MacOS</span><span class="sxs-lookup"><span data-stu-id="35a07-119">Linux/MacOS</span></span>

```bash
mvn archetype:generate \
    -DarchetypeGroupId=com.microsoft.azure \
    -DarchetypeArtifactId=azure-functions-archetype 
```

### <a name="windows-cmd"></a><span data-ttu-id="35a07-120">Windows (CMD)</span><span class="sxs-lookup"><span data-stu-id="35a07-120">Windows (CMD)</span></span>
```cmd
mvn archetype:generate ^
    -DarchetypeGroupId=com.microsoft.azure ^
    -DarchetypeArtifactId=azure-functions-archetype
```

<span data-ttu-id="35a07-121">Maven will ask you for values needed to finish generating the project.</span><span class="sxs-lookup"><span data-stu-id="35a07-121">Maven will ask you for values needed to finish generating the project.</span></span> <span data-ttu-id="35a07-122">For _groupId_, _artifactId_, and _version_ values, see the [Maven naming conventions](https://maven.apache.org/guides/mini/guide-naming-conventions.html) reference.</span><span class="sxs-lookup"><span data-stu-id="35a07-122">For _groupId_, _artifactId_, and _version_ values, see the [Maven naming conventions](https://maven.apache.org/guides/mini/guide-naming-conventions.html) reference.</span></span> <span data-ttu-id="35a07-123">The _appName_ value must be unique across Azure, so Maven generates an app name based on the previously entered _artifactId_  as a default.</span><span class="sxs-lookup"><span data-stu-id="35a07-123">The _appName_ value must be unique across Azure, so Maven generates an app name based on the previously entered _artifactId_  as a default.</span></span> <span data-ttu-id="35a07-124">The _packageName_ value determines the Java package for the generated function code.</span><span class="sxs-lookup"><span data-stu-id="35a07-124">The _packageName_ value determines the Java package for the generated function code.</span></span>

<span data-ttu-id="35a07-125">The `appRegion` value specifies which [Azure region](https://azure.microsoft.com/global-infrastructure/regions/) you want to run the deployed Function app in.</span><span class="sxs-lookup"><span data-stu-id="35a07-125">The `appRegion` value specifies which [Azure region](https://azure.microsoft.com/global-infrastructure/regions/) you want to run the deployed Function app in.</span></span> <span data-ttu-id="35a07-126">You can get a list of region name values through the `az account list-locations` command in the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="35a07-126">You can get a list of region name values through the `az account list-locations` command in the Azure CLI.</span></span> <span data-ttu-id="35a07-127">The `resourceGroup` value specifies which Azure resource group the function app will be created in.</span><span class="sxs-lookup"><span data-stu-id="35a07-127">The `resourceGroup` value specifies which Azure resource group the function app will be created in.</span></span>

<span data-ttu-id="35a07-128">The `com.fabrikam.functions` and `fabrikam-functions` identifiers below are used as an example and to make later steps in this quickstart easier to read.</span><span class="sxs-lookup"><span data-stu-id="35a07-128">The `com.fabrikam.functions` and `fabrikam-functions` identifiers below are used as an example and to make later steps in this quickstart easier to read.</span></span> <span data-ttu-id="35a07-129">You are encouraged to supply your own values to Maven in this step.</span><span class="sxs-lookup"><span data-stu-id="35a07-129">You are encouraged to supply your own values to Maven in this step.</span></span>

```Output
Define value for property 'groupId': com.fabrikam.functions
Define value for property 'artifactId' : fabrikam-functions
Define value for property 'version' 1.0-SNAPSHOT : 
Define value for property 'package': com.fabrikam.functions
Define value for property 'appName' fabrikam-functions-20170927220323382:
Define value for property 'appRegion' westus : 
Define value for property 'resourceGroup' java-functions-group: 
Confirm properties configuration: Y
```

<span data-ttu-id="35a07-130">Maven creates the project files in a new folder with a name of _artifactId_, in this example `fabrikam-functions`.</span><span class="sxs-lookup"><span data-stu-id="35a07-130">Maven creates the project files in a new folder with a name of _artifactId_, in this example `fabrikam-functions`.</span></span> <span data-ttu-id="35a07-131">The ready to run generated code in the project is a simple [HTTP triggered](/azure/azure-functions/functions-bindings-http-webhook) function that echoes the body of the request after a "Hello, " string.</span><span class="sxs-lookup"><span data-stu-id="35a07-131">The ready to run generated code in the project is a simple [HTTP triggered](/azure/azure-functions/functions-bindings-http-webhook) function that echoes the body of the request after a "Hello, " string.</span></span>

```java
public class Function {
    @FunctionName("HttpTrigger-Java")
    public HttpResponseMessage HttpTriggerJava(
    @HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,final ExecutionContext context) {
        context.getLogger().info("Java HTTP trigger processed a request.");

        // Parse query parameter
        String query = request.getQueryParameters().get("name");
        String name = request.getBody().orElse(query);

        if (name == null) {
            return request.createResponseBuilder(HttpStatus.BAD_REQUEST).body("Please pass a name on the query string or in the request body").build();
        } else {
            return request.createResponseBuilder(HttpStatus.OK).body("Hello, " + name).build();
        }
    }
}
```

## <a name="run-the-function-locally"></a><span data-ttu-id="35a07-132">Run the function locally</span><span class="sxs-lookup"><span data-stu-id="35a07-132">Run the function locally</span></span>

<span data-ttu-id="35a07-133">Change directory to the newly created project folder and build and run the function with Maven:</span><span class="sxs-lookup"><span data-stu-id="35a07-133">Change directory to the newly created project folder and build and run the function with Maven:</span></span>

```
cd fabrikam-functions
mvn clean package 
mvn azure-functions:run
```

> [!NOTE]
> <span data-ttu-id="35a07-134">If you're experiencing this exception: `javax.xml.bind.JAXBException` with Java 9, see the workaround on [GitHub](https://github.com/jOOQ/jOOQ/issues/6477).</span><span class="sxs-lookup"><span data-stu-id="35a07-134">If you're experiencing this exception: `javax.xml.bind.JAXBException` with Java 9, see the workaround on [GitHub](https://github.com/jOOQ/jOOQ/issues/6477).</span></span>

<span data-ttu-id="35a07-135">You see this output when the function is running locally on your system and ready to respond to HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="35a07-135">You see this output when the function is running locally on your system and ready to respond to HTTP requests:</span></span>

```Output
Listening on http://0.0.0.0:7071/
Hit CTRL-C to exit...

Http Functions:

        HttpTrigger-Java: http://localhost:7071/api/HttpTrigger-Java
```

<span data-ttu-id="35a07-136">Trigger the function from the command line using curl in a new terminal window:</span><span class="sxs-lookup"><span data-stu-id="35a07-136">Trigger the function from the command line using curl in a new terminal window:</span></span>

```
curl -w '\n' -d LocalFunctionTest http://localhost:7071/api/HttpTrigger-Java
```

```Output
Hello, LocalFunctionTest
```

<span data-ttu-id="35a07-137">Use `Ctrl-C` in the terminal to stop the function code.</span><span class="sxs-lookup"><span data-stu-id="35a07-137">Use `Ctrl-C` in the terminal to stop the function code.</span></span>

## <a name="deploy-the-function-to-azure"></a><span data-ttu-id="35a07-138">Deploy the function to Azure</span><span class="sxs-lookup"><span data-stu-id="35a07-138">Deploy the function to Azure</span></span>

<span data-ttu-id="35a07-139">The deploy process to Azure Functions uses account credentials from the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="35a07-139">The deploy process to Azure Functions uses account credentials from the Azure CLI.</span></span> <span data-ttu-id="35a07-140">[Log in with the Azure CLI](/cli/azure/authenticate-azure-cli?view=azure-cli-latest) before continuing.</span><span class="sxs-lookup"><span data-stu-id="35a07-140">[Log in with the Azure CLI](/cli/azure/authenticate-azure-cli?view=azure-cli-latest) before continuing.</span></span>

```azurecli
az login
```

<span data-ttu-id="35a07-141">Deploy your code into a new Function app using the `azure-functions:deploy` Maven target.</span><span class="sxs-lookup"><span data-stu-id="35a07-141">Deploy your code into a new Function app using the `azure-functions:deploy` Maven target.</span></span>

```
mvn azure-functions:deploy
```

<span data-ttu-id="35a07-142">When the deploy is complete, you see the URL you can use to access your Azure function app:</span><span class="sxs-lookup"><span data-stu-id="35a07-142">When the deploy is complete, you see the URL you can use to access your Azure function app:</span></span>

```output
[INFO] Successfully deployed Function App with package.
[INFO] Deleting deployment package from Azure Storage...
[INFO] Successfully deleted deployment package fabrikam-function-20170920120101928.20170920143621915.zip
[INFO] Successfully deployed Function App at https://fabrikam-function-20170920120101928.azurewebsites.net
[INFO] ------------------------------------------------------------------------
```

<span data-ttu-id="35a07-143">Test the function app running on Azure using `cURL`.</span><span class="sxs-lookup"><span data-stu-id="35a07-143">Test the function app running on Azure using `cURL`.</span></span> <span data-ttu-id="35a07-144">You'll need to change the URL from the sample below to match the deployed URL for your own function app from the previous step.</span><span class="sxs-lookup"><span data-stu-id="35a07-144">You'll need to change the URL from the sample below to match the deployed URL for your own function app from the previous step.</span></span>

```
curl -w '\n' -d AzureFunctionsTest https://fabrikam-functions-20170920120101928.azurewebsites.net/api/HttpTrigger-Java
```

```Output
Hello, AzureFunctionsTest
```

## <a name="make-changes-and-redeploy"></a><span data-ttu-id="35a07-145">Make changes and redeploy</span><span class="sxs-lookup"><span data-stu-id="35a07-145">Make changes and redeploy</span></span>

<span data-ttu-id="35a07-146">Edit the `src/main.../Function.java` source file in the generated project to alter the text returned by your Function app.</span><span class="sxs-lookup"><span data-stu-id="35a07-146">Edit the `src/main.../Function.java` source file in the generated project to alter the text returned by your Function app.</span></span> <span data-ttu-id="35a07-147">Change this line:</span><span class="sxs-lookup"><span data-stu-id="35a07-147">Change this line:</span></span>

```java
return request.createResponse(200, "Hello, " + name);
```

<span data-ttu-id="35a07-148">To the following:</span><span class="sxs-lookup"><span data-stu-id="35a07-148">To the following:</span></span>

```java
return request.createResponse(200, "Hi, " + name);
```

<span data-ttu-id="35a07-149">Save the changes and redeploy by running `azure-functions:deploy` from the terminal as before.</span><span class="sxs-lookup"><span data-stu-id="35a07-149">Save the changes and redeploy by running `azure-functions:deploy` from the terminal as before.</span></span> <span data-ttu-id="35a07-150">The function app will be updated and this request:</span><span class="sxs-lookup"><span data-stu-id="35a07-150">The function app will be updated and this request:</span></span>

```bash
curl -w '\n' -d AzureFunctionsTest https://fabrikam-functions-20170920120101928.azurewebsites.net/api/HttpTrigger-Java
```

<span data-ttu-id="35a07-151">Will have updated output:</span><span class="sxs-lookup"><span data-stu-id="35a07-151">Will have updated output:</span></span>

```Output
Hi, AzureFunctionsTest
```

## <a name="next-steps"></a><span data-ttu-id="35a07-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="35a07-152">Next steps</span></span>

<span data-ttu-id="35a07-153">You've created a Java function app with a simple HTTP trigger and deployed it to Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="35a07-153">You've created a Java function app with a simple HTTP trigger and deployed it to Azure Functions.</span></span>

- <span data-ttu-id="35a07-154">Review the  [Java Functions developer guide](functions-reference-java.md) for more information on developing Java functions.</span><span class="sxs-lookup"><span data-stu-id="35a07-154">Review the  [Java Functions developer guide](functions-reference-java.md) for more information on developing Java functions.</span></span>
- <span data-ttu-id="35a07-155">Add additional functions with different triggers to your project using the `azure-functions:add` Maven target.</span><span class="sxs-lookup"><span data-stu-id="35a07-155">Add additional functions with different triggers to your project using the `azure-functions:add` Maven target.</span></span>
- <span data-ttu-id="35a07-156">Write and debug functions locally with [Visual Studio Code](https://code.visualstudio.com/docs/java/java-azurefunctions), [IntelliJ](functions-create-maven-intellij.md), and [Eclipse](functions-create-maven-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="35a07-156">Write and debug functions locally with [Visual Studio Code](https://code.visualstudio.com/docs/java/java-azurefunctions), [IntelliJ](functions-create-maven-intellij.md), and [Eclipse](functions-create-maven-eclipse.md).</span></span> 
- <span data-ttu-id="35a07-157">Debug functions deployed in Azure with Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="35a07-157">Debug functions deployed in Azure with Visual Studio Code.</span></span> <span data-ttu-id="35a07-158">See the Visual Studio Code [serverless Java applications](https://code.visualstudio.com/docs/java/java-serverless#_remote-debug-functions-running-in-the-cloud) documentation for instructions.</span><span class="sxs-lookup"><span data-stu-id="35a07-158">See the Visual Studio Code [serverless Java applications](https://code.visualstudio.com/docs/java/java-serverless#_remote-debug-functions-running-in-the-cloud) documentation for instructions.</span></span>
