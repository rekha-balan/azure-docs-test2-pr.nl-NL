---
title: Create an Azure function app with Java and IntelliJ| Microsoft Docs
description: How-to guide to create and publish a simple HTTP triggered serverless app using Java and IntelliJ to Azure Functions.
services: functions
documentationcenter: na
author: jeffhollan
manager: jpconnock
keywords: azure functions, functions, event processing, compute, serverless architecture, java
ms.service: azure-functions
ms.devlang: java
ms.topic: conceptual
ms.date: 07/01/2018
ms.author: jehollan
ms.custom: mvc, devcenter
ms.openlocfilehash: b28e7b158af939defd37734c3ff9fe2309e3ab85
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869955"
---
# <a name="create-your-first-function-with-java-and-intellij-preview"></a><span data-ttu-id="a5237-104">Create your first function with Java and IntelliJ (Preview)</span><span class="sxs-lookup"><span data-stu-id="a5237-104">Create your first function with Java and IntelliJ (Preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="a5237-105">Java for Azure Functions is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="a5237-105">Java for Azure Functions is currently in preview.</span></span>

<span data-ttu-id="a5237-106">This article shows you how to create a [serverless](https://azure.microsoft.com/overview/serverless-computing/) function project with IntelliJ IDEA and Apache Maven, test and debug it on your own computer from the IDE, and deploy it to Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a5237-106">This article shows you how to create a [serverless](https://azure.microsoft.com/overview/serverless-computing/) function project with IntelliJ IDEA and Apache Maven, test and debug it on your own computer from the IDE, and deploy it to Azure Functions.</span></span> 

<!-- TODO ![Access a Hello World function from the command line with cURL](media/functions-create-java-maven/hello-azure.png) -->

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="set-up-your-development-environment"></a><span data-ttu-id="a5237-107">Set up your development environment</span><span class="sxs-lookup"><span data-stu-id="a5237-107">Set up your development environment</span></span>

<span data-ttu-id="a5237-108">To develop a functions app with Java and IntelliJ, you must have the following installed:</span><span class="sxs-lookup"><span data-stu-id="a5237-108">To develop a functions app with Java and IntelliJ, you must have the following installed:</span></span>

-  <span data-ttu-id="a5237-109">[Java Developer Kit](https://www.azul.com/downloads/zulu/), version 8.</span><span class="sxs-lookup"><span data-stu-id="a5237-109">[Java Developer Kit](https://www.azul.com/downloads/zulu/), version 8.</span></span>
-  <span data-ttu-id="a5237-110">[Apache Maven](https://maven.apache.org), version 3.0 or above.</span><span class="sxs-lookup"><span data-stu-id="a5237-110">[Apache Maven](https://maven.apache.org), version 3.0 or above.</span></span>
-  <span data-ttu-id="a5237-111">[IntelliJ IDEA](https://www.jetbrains.com/idea/download), Community or Ultimate with Maven tooling.</span><span class="sxs-lookup"><span data-stu-id="a5237-111">[IntelliJ IDEA](https://www.jetbrains.com/idea/download), Community or Ultimate with Maven tooling.</span></span>
-  [<span data-ttu-id="a5237-112">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a5237-112">Azure CLI</span></span>](https://docs.microsoft.com/cli/azure)

> [!IMPORTANT] 
> <span data-ttu-id="a5237-113">The JAVA_HOME environment variable must be set to the install location of the JDK to complete this quickstart.</span><span class="sxs-lookup"><span data-stu-id="a5237-113">The JAVA_HOME environment variable must be set to the install location of the JDK to complete this quickstart.</span></span>

<span data-ttu-id="a5237-114">It is highly reccommended to also install [Azure Functions Core Tools, version 2](functions-run-local.md#v2), which provide a local development environment for writing, running, and debugging Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a5237-114">It is highly reccommended to also install [Azure Functions Core Tools, version 2](functions-run-local.md#v2), which provide a local development environment for writing, running, and debugging Azure Functions.</span></span> 


## <a name="create-a-functions-project"></a><span data-ttu-id="a5237-115">Create a Functions project</span><span class="sxs-lookup"><span data-stu-id="a5237-115">Create a Functions project</span></span>

1. <span data-ttu-id="a5237-116">In IntelliJ IDEA, click to **Create New Project**.</span><span class="sxs-lookup"><span data-stu-id="a5237-116">In IntelliJ IDEA, click to **Create New Project**.</span></span>  
1. <span data-ttu-id="a5237-117">Select to create from **Maven**</span><span class="sxs-lookup"><span data-stu-id="a5237-117">Select to create from **Maven**</span></span>
1. <span data-ttu-id="a5237-118">Select the checkbox to **Create from archetype** and **Add Archetype** for the [azure-functions-archetype](https://mvnrepository.com/artifact/com.microsoft.azure/azure-functions-archetype).</span><span class="sxs-lookup"><span data-stu-id="a5237-118">Select the checkbox to **Create from archetype** and **Add Archetype** for the [azure-functions-archetype](https://mvnrepository.com/artifact/com.microsoft.azure/azure-functions-archetype).</span></span>
    - <span data-ttu-id="a5237-119">GroupId: com.microsoft.azure</span><span class="sxs-lookup"><span data-stu-id="a5237-119">GroupId: com.microsoft.azure</span></span>
    - <span data-ttu-id="a5237-120">ArtifactId: azure-functions-archetype</span><span class="sxs-lookup"><span data-stu-id="a5237-120">ArtifactId: azure-functions-archetype</span></span>
    - <span data-ttu-id="a5237-121">Version: Use latest version from [the central repository](https://mvnrepository.com/artifact/com.microsoft.azure/azure-functions-archetype)
    ![IntelliJ Maven create](media/functions-create-first-java-intellij/functions-create-intellij.png)</span><span class="sxs-lookup"><span data-stu-id="a5237-121">Version: Use latest version from [the central repository](https://mvnrepository.com/artifact/com.microsoft.azure/azure-functions-archetype)
![IntelliJ Maven create](media/functions-create-first-java-intellij/functions-create-intellij.png)</span></span>  
1. <span data-ttu-id="a5237-122">Click **Next** and enter details for current project, and eventually **Finish**.</span><span class="sxs-lookup"><span data-stu-id="a5237-122">Click **Next** and enter details for current project, and eventually **Finish**.</span></span>

<span data-ttu-id="a5237-123">Maven creates the project files in a new folder with a name of _artifactId_.</span><span class="sxs-lookup"><span data-stu-id="a5237-123">Maven creates the project files in a new folder with a name of _artifactId_.</span></span> <span data-ttu-id="a5237-124">The generated code in the project is a simple [HTTP triggered](/azure/azure-functions/functions-bindings-http-webhook) function that echoes the body of the triggering HTTP request.</span><span class="sxs-lookup"><span data-stu-id="a5237-124">The generated code in the project is a simple [HTTP triggered](/azure/azure-functions/functions-bindings-http-webhook) function that echoes the body of the triggering HTTP request.</span></span>

## <a name="run-functions-locally-in-the-ide"></a><span data-ttu-id="a5237-125">Run functions locally in the IDE</span><span class="sxs-lookup"><span data-stu-id="a5237-125">Run functions locally in the IDE</span></span>

> [!NOTE]
> <span data-ttu-id="a5237-126">[Azure Functions Core Tools, version 2](functions-run-local.md#v2) must be installed to run and debug functions locally.</span><span class="sxs-lookup"><span data-stu-id="a5237-126">[Azure Functions Core Tools, version 2](functions-run-local.md#v2) must be installed to run and debug functions locally.</span></span>

1. <span data-ttu-id="a5237-127">Select to import changes or make sure that [auto import](https://www.jetbrains.com/help/idea/creating-and-optimizing-imports.html) is enables.</span><span class="sxs-lookup"><span data-stu-id="a5237-127">Select to import changes or make sure that [auto import](https://www.jetbrains.com/help/idea/creating-and-optimizing-imports.html) is enables.</span></span>
1. <span data-ttu-id="a5237-128">Open the **Maven Projects** toolbar</span><span class="sxs-lookup"><span data-stu-id="a5237-128">Open the **Maven Projects** toolbar</span></span>
1. <span data-ttu-id="a5237-129">Under Lifecycle, double-click **package** to package and build the solution and create a target directory.</span><span class="sxs-lookup"><span data-stu-id="a5237-129">Under Lifecycle, double-click **package** to package and build the solution and create a target directory.</span></span>
1. <span data-ttu-id="a5237-130">Under Plugins -> azure-functions double-click **azure-functions:run** to start the azure functions local runtime.</span><span class="sxs-lookup"><span data-stu-id="a5237-130">Under Plugins -> azure-functions double-click **azure-functions:run** to start the azure functions local runtime.</span></span>  
  <span data-ttu-id="a5237-131">![Maven toolbar for Azure Functions](media/functions-create-first-java-intellij/functions-intellij-java-maven-toolbar.png)</span><span class="sxs-lookup"><span data-stu-id="a5237-131">![Maven toolbar for Azure Functions](media/functions-create-first-java-intellij/functions-intellij-java-maven-toolbar.png)</span></span>  

<span data-ttu-id="a5237-132">Close the run dialog when you're done testing your function.</span><span class="sxs-lookup"><span data-stu-id="a5237-132">Close the run dialog when you're done testing your function.</span></span> <span data-ttu-id="a5237-133">Only one function host can be active and running locally at a time.</span><span class="sxs-lookup"><span data-stu-id="a5237-133">Only one function host can be active and running locally at a time.</span></span>

### <a name="debug-the-function-in-intellij"></a><span data-ttu-id="a5237-134">Debug the function in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="a5237-134">Debug the function in IntelliJ</span></span>
<span data-ttu-id="a5237-135">To start the function host in debug mode, add **-DenableDebug** as the argument when you run your function.</span><span class="sxs-lookup"><span data-stu-id="a5237-135">To start the function host in debug mode, add **-DenableDebug** as the argument when you run your function.</span></span> <span data-ttu-id="a5237-136">You could run below command line in terminal or configure it in [maven goals](https://www.jetbrains.com/help/idea/maven-support.html#run_goal).</span><span class="sxs-lookup"><span data-stu-id="a5237-136">You could run below command line in terminal or configure it in [maven goals](https://www.jetbrains.com/help/idea/maven-support.html#run_goal).</span></span> <span data-ttu-id="a5237-137">Then the function host will open a debug port at 5005.</span><span class="sxs-lookup"><span data-stu-id="a5237-137">Then the function host will open a debug port at 5005.</span></span> 

```
mvn azure-functions:run -DenableDebug
```

<span data-ttu-id="a5237-138">To debug in IntelliJ, In the **Run** menu select **Edit Configurations**.</span><span class="sxs-lookup"><span data-stu-id="a5237-138">To debug in IntelliJ, In the **Run** menu select **Edit Configurations**.</span></span> <span data-ttu-id="a5237-139">Click **+** to add a **Remote**.</span><span class="sxs-lookup"><span data-stu-id="a5237-139">Click **+** to add a **Remote**.</span></span> <span data-ttu-id="a5237-140">Fill in **Name** and **Settings**, and then click **OK** to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="a5237-140">Fill in **Name** and **Settings**, and then click **OK** to save the configuration.</span></span> <span data-ttu-id="a5237-141">After setup, click **Debug** 'Your Remote Configuration Name' or hit **Shift+F9** to start debugging.</span><span class="sxs-lookup"><span data-stu-id="a5237-141">After setup, click **Debug** 'Your Remote Configuration Name' or hit **Shift+F9** to start debugging.</span></span>

![Debug functions in IntelliJ](media/functions-create-first-java-intellij/debug-configuration-intellij.PNG)

<span data-ttu-id="a5237-143">When finished stop the debugger and the running process.</span><span class="sxs-lookup"><span data-stu-id="a5237-143">When finished stop the debugger and the running process.</span></span> <span data-ttu-id="a5237-144">Only one function host can be active and running locally at a time.</span><span class="sxs-lookup"><span data-stu-id="a5237-144">Only one function host can be active and running locally at a time.</span></span>

## <a name="deploy-the-function-to-azure"></a><span data-ttu-id="a5237-145">Deploy the function to Azure</span><span class="sxs-lookup"><span data-stu-id="a5237-145">Deploy the function to Azure</span></span>

<span data-ttu-id="a5237-146">The deploy process to Azure Functions uses account credentials from the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a5237-146">The deploy process to Azure Functions uses account credentials from the Azure CLI.</span></span> <span data-ttu-id="a5237-147">[Log in with the Azure CLI](/cli/azure/authenticate-azure-cli?view=azure-cli-latest) before continuing using your computer's command prompt.</span><span class="sxs-lookup"><span data-stu-id="a5237-147">[Log in with the Azure CLI](/cli/azure/authenticate-azure-cli?view=azure-cli-latest) before continuing using your computer's command prompt.</span></span>

```azurecli
az login
```

<span data-ttu-id="a5237-148">Deploy your code into a new Function app using the `azure-functions:deploy` Maven target, or select the azure-functions:deploy option in the Maven Projects window.</span><span class="sxs-lookup"><span data-stu-id="a5237-148">Deploy your code into a new Function app using the `azure-functions:deploy` Maven target, or select the azure-functions:deploy option in the Maven Projects window.</span></span>

```
mvn azure-functions:deploy
```

<span data-ttu-id="a5237-149">When the deploy is complete, you see the URL you can use to access your Azure function app:</span><span class="sxs-lookup"><span data-stu-id="a5237-149">When the deploy is complete, you see the URL you can use to access your Azure function app:</span></span>

```output
[INFO] Successfully deployed Function App with package.
[INFO] Deleting deployment package from Azure Storage...
[INFO] Successfully deleted deployment package fabrikam-function-20170920120101928.20170920143621915.zip
[INFO] Successfully deployed Function App at https://fabrikam-function-20170920120101928.azurewebsites.net
[INFO] ------------------------------------------------------------------------
```

## <a name="next-steps"></a><span data-ttu-id="a5237-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="a5237-150">Next steps</span></span>

- <span data-ttu-id="a5237-151">Review the  [Java Functions developer guide](functions-reference-java.md) for more information on developing Java functions.</span><span class="sxs-lookup"><span data-stu-id="a5237-151">Review the  [Java Functions developer guide](functions-reference-java.md) for more information on developing Java functions.</span></span>
- <span data-ttu-id="a5237-152">Add additional functions with different triggers to your project using the `azure-functions:add` Maven target.</span><span class="sxs-lookup"><span data-stu-id="a5237-152">Add additional functions with different triggers to your project using the `azure-functions:add` Maven target.</span></span>
