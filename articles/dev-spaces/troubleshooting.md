---
title: Troubleshooting | Microsoft Docs
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: ghogen
ms.author: ghogen
ms.date: 05/11/2018
ms.topic: article
description: Rapid Kubernetes development with containers and microservices on Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Kubernetes Service, containers
manager: douge
ms.openlocfilehash: b66e43c0f40f184bfb2c62327f5742346ff8b187
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868898"
---
# <a name="troubleshooting-guide"></a><span data-ttu-id="ecd5a-104">Troubleshooting guide</span><span class="sxs-lookup"><span data-stu-id="ecd5a-104">Troubleshooting guide</span></span>

<span data-ttu-id="ecd5a-105">This guide contains information about common problems you may have when using Azure Dev Spaces.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-105">This guide contains information about common problems you may have when using Azure Dev Spaces.</span></span>

## <a name="enabling-detailed-logging"></a><span data-ttu-id="ecd5a-106">Enabling detailed logging</span><span class="sxs-lookup"><span data-stu-id="ecd5a-106">Enabling detailed logging</span></span>

<span data-ttu-id="ecd5a-107">In order to troubleshoot problems more effectively, it may help to create more detailed logs for review.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-107">In order to troubleshoot problems more effectively, it may help to create more detailed logs for review.</span></span>

<span data-ttu-id="ecd5a-108">For the Visual Studio extension, you can do this by setting the `MS_VS_AZUREDEVSPACES_TOOLS_LOGGING_ENABLED` environment variable to 1.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-108">For the Visual Studio extension, you can do this by setting the `MS_VS_AZUREDEVSPACES_TOOLS_LOGGING_ENABLED` environment variable to 1.</span></span> <span data-ttu-id="ecd5a-109">Be sure to restart Visual Studio for the environment variable to take effect.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-109">Be sure to restart Visual Studio for the environment variable to take effect.</span></span> <span data-ttu-id="ecd5a-110">Once enabled, detailed logs will be written to your `%TEMP%\Microsoft.VisualStudio.Azure.DevSpaces.Tools` directory.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-110">Once enabled, detailed logs will be written to your `%TEMP%\Microsoft.VisualStudio.Azure.DevSpaces.Tools` directory.</span></span>

<span data-ttu-id="ecd5a-111">In the CLI, you can output more information during command execution by using the `--verbose` switch.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-111">In the CLI, you can output more information during command execution by using the `--verbose` switch.</span></span>

## <a name="error-failed-to-create-azure-dev-spaces-controller"></a><span data-ttu-id="ecd5a-112">Error 'Failed to create Azure Dev Spaces controller'</span><span class="sxs-lookup"><span data-stu-id="ecd5a-112">Error 'Failed to create Azure Dev Spaces controller'</span></span>

<span data-ttu-id="ecd5a-113">You might see this error when something goes wrong with the creation of the controller.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-113">You might see this error when something goes wrong with the creation of the controller.</span></span> <span data-ttu-id="ecd5a-114">If it's a transient error, deleting and recreating the controller will fix it.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-114">If it's a transient error, deleting and recreating the controller will fix it.</span></span>

### <a name="try"></a><span data-ttu-id="ecd5a-115">Try:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-115">Try:</span></span>

<span data-ttu-id="ecd5a-116">To delete the controller, use the Azure Dev Spaces CLI.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-116">To delete the controller, use the Azure Dev Spaces CLI.</span></span> <span data-ttu-id="ecd5a-117">It’s not possible to do it in Visual Studio or Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-117">It’s not possible to do it in Visual Studio or Cloud Shell.</span></span> <span data-ttu-id="ecd5a-118">To install the AZDS CLI, first install the Azure CLI, and then run this command:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-118">To install the AZDS CLI, first install the Azure CLI, and then run this command:</span></span>

```cmd
az aks use-dev-spaces -g <resource group name> -n <cluster name>
```

<span data-ttu-id="ecd5a-119">And then run this command to delete the controller:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-119">And then run this command to delete the controller:</span></span>

```cmd
azds remove -g <resource group name> -n <cluster name>
```

<span data-ttu-id="ecd5a-120">Recreating the controller can be done from the CLI or Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-120">Recreating the controller can be done from the CLI or Visual Studio.</span></span> <span data-ttu-id="ecd5a-121">Follow the instructions in the tutorials as if starting for the first time.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-121">Follow the instructions in the tutorials as if starting for the first time.</span></span>


## <a name="error-service-cannot-be-started"></a><span data-ttu-id="ecd5a-122">Error 'Service cannot be started.'</span><span class="sxs-lookup"><span data-stu-id="ecd5a-122">Error 'Service cannot be started.'</span></span>

<span data-ttu-id="ecd5a-123">You might see this error when your service code fails to start.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-123">You might see this error when your service code fails to start.</span></span> <span data-ttu-id="ecd5a-124">The cause is often in user code.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-124">The cause is often in user code.</span></span> <span data-ttu-id="ecd5a-125">To get more diagnostic information, make the following changes to your commands and settings:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-125">To get more diagnostic information, make the following changes to your commands and settings:</span></span>

### <a name="try"></a><span data-ttu-id="ecd5a-126">Try:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-126">Try:</span></span>

<span data-ttu-id="ecd5a-127">On the command line:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-127">On the command line:</span></span>

<span data-ttu-id="ecd5a-128">When using _azds.exe_, use the --verbose command-line option, and use the --output command-line option to specify the output format.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-128">When using _azds.exe_, use the --verbose command-line option, and use the --output command-line option to specify the output format.</span></span>
 
    ```cmd
    azds up --verbose --output json
    ```

<span data-ttu-id="ecd5a-129">In Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-129">In Visual Studio:</span></span>

1. <span data-ttu-id="ecd5a-130">Open **Tools > Options** and under **Projects and Solutions**, choose and **Build and Run**.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-130">Open **Tools > Options** and under **Projects and Solutions**, choose and **Build and Run**.</span></span>
2. <span data-ttu-id="ecd5a-131">Change the settings for **MSBuild project build output verbosity** to **Detailed** or **Diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-131">Change the settings for **MSBuild project build output verbosity** to **Detailed** or **Diagnostic**.</span></span>

    ![Screenshot of Tools Options dialog](media/common/VerbositySetting.PNG)
    
## <a name="dns-name-resolution-fails-for-a-public-url-associated-with-a-dev-spaces-service"></a><span data-ttu-id="ecd5a-133">DNS name resolution fails for a public URL associated with a Dev Spaces service</span><span class="sxs-lookup"><span data-stu-id="ecd5a-133">DNS name resolution fails for a public URL associated with a Dev Spaces service</span></span>

<span data-ttu-id="ecd5a-134">When this happens, you might see a "Page cannot be displayed" or "This site cannot be reached" error in your web browser when attempting to connect to the public URL associated with a Dev Spaces service.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-134">When this happens, you might see a "Page cannot be displayed" or "This site cannot be reached" error in your web browser when attempting to connect to the public URL associated with a Dev Spaces service.</span></span>

### <a name="try"></a><span data-ttu-id="ecd5a-135">Try:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-135">Try:</span></span>

<span data-ttu-id="ecd5a-136">You can use the following command to list out all URLs associated with your Dev Spaces services:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-136">You can use the following command to list out all URLs associated with your Dev Spaces services:</span></span>

```cmd
azds list-uris
```

<span data-ttu-id="ecd5a-137">If a URL is in the *Pending* state, that means that Dev Spaces is still waiting for DNS registration to complete.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-137">If a URL is in the *Pending* state, that means that Dev Spaces is still waiting for DNS registration to complete.</span></span> <span data-ttu-id="ecd5a-138">Sometimes, it takes a few minutes for this to happen.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-138">Sometimes, it takes a few minutes for this to happen.</span></span> <span data-ttu-id="ecd5a-139">Dev Spaces also opens a localhost tunnel for each service, which you can use while waiting on DNS registration.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-139">Dev Spaces also opens a localhost tunnel for each service, which you can use while waiting on DNS registration.</span></span>

<span data-ttu-id="ecd5a-140">If a URL remains in the *Pending* state for more than 5 minutes, it may indicate a problem with the external DNS pod that creates the public endpoint and/or the nginx ingress controller pod that acquires the public endpoint.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-140">If a URL remains in the *Pending* state for more than 5 minutes, it may indicate a problem with the external DNS pod that creates the public endpoint and/or the nginx ingress controller pod that acquires the public endpoint.</span></span> <span data-ttu-id="ecd5a-141">You can use the following commands to delete these pods.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-141">You can use the following commands to delete these pods.</span></span> <span data-ttu-id="ecd5a-142">They will be recreated automatically.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-142">They will be recreated automatically.</span></span>

```cmd
kubectl delete pod -n kube-system -l app=addon-http-application-routing-external-dns
kubectl delete pod -n kube-system -l app=addon-http-application-routing-nginx-ingress
```

## <a name="error-required-tools-and-configurations-are-missing"></a><span data-ttu-id="ecd5a-143">Error 'Required tools and configurations are missing'</span><span class="sxs-lookup"><span data-stu-id="ecd5a-143">Error 'Required tools and configurations are missing'</span></span>

<span data-ttu-id="ecd5a-144">This error might occur when launching VS Code: "[Azure Dev Spaces] Required tools and configurations to build and debug '[project name]' are missing."</span><span class="sxs-lookup"><span data-stu-id="ecd5a-144">This error might occur when launching VS Code: "[Azure Dev Spaces] Required tools and configurations to build and debug '[project name]' are missing."</span></span>
<span data-ttu-id="ecd5a-145">The error means that azds.exe is not in the PATH environment variable, as seen in VS Code.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-145">The error means that azds.exe is not in the PATH environment variable, as seen in VS Code.</span></span>

### <a name="try"></a><span data-ttu-id="ecd5a-146">Try:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-146">Try:</span></span>

<span data-ttu-id="ecd5a-147">Launch VS Code from a command prompt where the PATH environment variable is set properly.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-147">Launch VS Code from a command prompt where the PATH environment variable is set properly.</span></span>

## <a name="error-azds-is-not-recognized-as-an-internal-or-external-command-operable-program-or-batch-file"></a><span data-ttu-id="ecd5a-148">Error 'azds' is not recognized as an internal or external command, operable program, or batch file</span><span class="sxs-lookup"><span data-stu-id="ecd5a-148">Error 'azds' is not recognized as an internal or external command, operable program, or batch file</span></span>
 
<span data-ttu-id="ecd5a-149">You might see this error if azds.exe is not installed or configured correctly.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-149">You might see this error if azds.exe is not installed or configured correctly.</span></span>

### <a name="try"></a><span data-ttu-id="ecd5a-150">Try:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-150">Try:</span></span>

1. <span data-ttu-id="ecd5a-151">Check the location %ProgramFiles%/Microsoft SDKs\Azure\Azure Dev Spaces CLI (Preview) for azds.exe.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-151">Check the location %ProgramFiles%/Microsoft SDKs\Azure\Azure Dev Spaces CLI (Preview) for azds.exe.</span></span> <span data-ttu-id="ecd5a-152">If it's there, add that location to the PATH environment variable.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-152">If it's there, add that location to the PATH environment variable.</span></span>
2. <span data-ttu-id="ecd5a-153">If azds.exe is not installed, run the following command:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-153">If azds.exe is not installed, run the following command:</span></span>

    ```cmd
    az aks use-dev-spaces -n <cluster-name> -g <resource-group>
    ```

## <a name="warning-dockerfile-could-not-be-generated-due-to-unsupported-language"></a><span data-ttu-id="ecd5a-154">Warning 'Dockerfile could not be generated due to unsupported language'</span><span class="sxs-lookup"><span data-stu-id="ecd5a-154">Warning 'Dockerfile could not be generated due to unsupported language'</span></span>
<span data-ttu-id="ecd5a-155">Azure Dev Spaces provides native support for C# and Node.js.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-155">Azure Dev Spaces provides native support for C# and Node.js.</span></span> <span data-ttu-id="ecd5a-156">When you run *azds prep* in a directory containing code written in one of these languages, Azure Dev Spaces will automatically create an appropriate Dockerfile for you.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-156">When you run *azds prep* in a directory containing code written in one of these languages, Azure Dev Spaces will automatically create an appropriate Dockerfile for you.</span></span>

<span data-ttu-id="ecd5a-157">You can still use Azure Dev Spaces with code written in other languages, but you will need to create the Dockerfile yourself prior to running *azds up* for the first time.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-157">You can still use Azure Dev Spaces with code written in other languages, but you will need to create the Dockerfile yourself prior to running *azds up* for the first time.</span></span>

### <a name="try"></a><span data-ttu-id="ecd5a-158">Try:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-158">Try:</span></span>
<span data-ttu-id="ecd5a-159">If your application is written in a language that Azure Dev Spaces does not natively support, you'll need to provide an appropriate Dockerfile to build a container image running your code.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-159">If your application is written in a language that Azure Dev Spaces does not natively support, you'll need to provide an appropriate Dockerfile to build a container image running your code.</span></span> <span data-ttu-id="ecd5a-160">Docker provides a [list of best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) as well as a [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) that can help you do this.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-160">Docker provides a [list of best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) as well as a [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) that can help you do this.</span></span>

<span data-ttu-id="ecd5a-161">Once you have an appropriate Dockerfile in place, you can proceed with running *azds up* to run your application in Azure Dev Spaces.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-161">Once you have an appropriate Dockerfile in place, you can proceed with running *azds up* to run your application in Azure Dev Spaces.</span></span>

## <a name="error-upstream-connect-error-or-disconnectreset-before-headers"></a><span data-ttu-id="ecd5a-162">Error 'upstream connect error or disconnect/reset before headers'</span><span class="sxs-lookup"><span data-stu-id="ecd5a-162">Error 'upstream connect error or disconnect/reset before headers'</span></span>
<span data-ttu-id="ecd5a-163">You may see this error when trying to access your service.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-163">You may see this error when trying to access your service.</span></span> <span data-ttu-id="ecd5a-164">For example, when you go to the service's URL in a browser.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-164">For example, when you go to the service's URL in a browser.</span></span> 

### <a name="reason"></a><span data-ttu-id="ecd5a-165">Reason</span><span class="sxs-lookup"><span data-stu-id="ecd5a-165">Reason</span></span> 
<span data-ttu-id="ecd5a-166">The container port isn't available.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-166">The container port isn't available.</span></span> <span data-ttu-id="ecd5a-167">This problem could occur because:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-167">This problem could occur because:</span></span> 
* <span data-ttu-id="ecd5a-168">The container is still in the process of being built and deployed.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-168">The container is still in the process of being built and deployed.</span></span> <span data-ttu-id="ecd5a-169">This issue can arise if you run `azds up` or start the debugger, and then try to access the container before it has successfully deployed.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-169">This issue can arise if you run `azds up` or start the debugger, and then try to access the container before it has successfully deployed.</span></span>
* <span data-ttu-id="ecd5a-170">Port configuration is not consistent across your _Dockerfile_, Helm Chart, and any server code that opens up a port.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-170">Port configuration is not consistent across your _Dockerfile_, Helm Chart, and any server code that opens up a port.</span></span>

### <a name="try"></a><span data-ttu-id="ecd5a-171">Try:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-171">Try:</span></span>
1. <span data-ttu-id="ecd5a-172">If the container is in the process of being built/deployed, you can wait 2-3 seconds and try accessing the service again.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-172">If the container is in the process of being built/deployed, you can wait 2-3 seconds and try accessing the service again.</span></span> 
1. <span data-ttu-id="ecd5a-173">Check your port configuration.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-173">Check your port configuration.</span></span> <span data-ttu-id="ecd5a-174">The specified port numbers should be **identical** in all the assets below:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-174">The specified port numbers should be **identical** in all the assets below:</span></span>
    * <span data-ttu-id="ecd5a-175">**Dockerfile:** Specified by the `EXPOSE` instruction.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-175">**Dockerfile:** Specified by the `EXPOSE` instruction.</span></span>
    * <span data-ttu-id="ecd5a-176">**[Helm chart](https://docs.helm.sh):** Specified by the `externalPort` and `internalPort` values for a service (often located in a `values.yml` file),</span><span class="sxs-lookup"><span data-stu-id="ecd5a-176">**[Helm chart](https://docs.helm.sh):** Specified by the `externalPort` and `internalPort` values for a service (often located in a `values.yml` file),</span></span>
    * <span data-ttu-id="ecd5a-177">Any ports being opened up in application code, for example in Node.js: `var server = app.listen(80, function () {...}`</span><span class="sxs-lookup"><span data-stu-id="ecd5a-177">Any ports being opened up in application code, for example in Node.js: `var server = app.listen(80, function () {...}`</span></span>


## <a name="config-file-not-found"></a><span data-ttu-id="ecd5a-178">Config file not found</span><span class="sxs-lookup"><span data-stu-id="ecd5a-178">Config file not found</span></span>
<span data-ttu-id="ecd5a-179">You run `azds up` and get the following error: `Config file not found: .../azds.yaml`</span><span class="sxs-lookup"><span data-stu-id="ecd5a-179">You run `azds up` and get the following error: `Config file not found: .../azds.yaml`</span></span>

### <a name="reason"></a><span data-ttu-id="ecd5a-180">Reason</span><span class="sxs-lookup"><span data-stu-id="ecd5a-180">Reason</span></span>
<span data-ttu-id="ecd5a-181">You must run `azds up` from the root directory of the code you want to run, and you must initialize the code folder to run with Azure Dev Spaces.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-181">You must run `azds up` from the root directory of the code you want to run, and you must initialize the code folder to run with Azure Dev Spaces.</span></span>

### <a name="try"></a><span data-ttu-id="ecd5a-182">Try:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-182">Try:</span></span>
1. <span data-ttu-id="ecd5a-183">Change your current directory to the root folder containing your service code.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-183">Change your current directory to the root folder containing your service code.</span></span> 
1. <span data-ttu-id="ecd5a-184">If you do not have a _azds.yaml_ file in the code folder, run `azds prep` to generate Docker, Kubernetes, and Azure Dev Spaces assets.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-184">If you do not have a _azds.yaml_ file in the code folder, run `azds prep` to generate Docker, Kubernetes, and Azure Dev Spaces assets.</span></span>

## <a name="error-the-pipe-program-azds-exited-unexpectedly-with-code-126"></a><span data-ttu-id="ecd5a-185">Error: 'The pipe program 'azds' exited unexpectedly with code 126.'</span><span class="sxs-lookup"><span data-stu-id="ecd5a-185">Error: 'The pipe program 'azds' exited unexpectedly with code 126.'</span></span>
<span data-ttu-id="ecd5a-186">Starting the VS Code debugger may sometimes result in this error.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-186">Starting the VS Code debugger may sometimes result in this error.</span></span> <span data-ttu-id="ecd5a-187">This is a known issue.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-187">This is a known issue.</span></span>

### <a name="try"></a><span data-ttu-id="ecd5a-188">Try:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-188">Try:</span></span>
1. <span data-ttu-id="ecd5a-189">Close and reopen VS Code.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-189">Close and reopen VS Code.</span></span>
2. <span data-ttu-id="ecd5a-190">Hit F5 again.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-190">Hit F5 again.</span></span>

## <a name="debugging-error-failed-to-find-debugger-extension-for-typecoreclr"></a><span data-ttu-id="ecd5a-191">Debugging error 'Failed to find debugger extension for type:coreclr'</span><span class="sxs-lookup"><span data-stu-id="ecd5a-191">Debugging error 'Failed to find debugger extension for type:coreclr'</span></span>
<span data-ttu-id="ecd5a-192">Running the VS Code debugger reports the error: `Failed to find debugger extension for type:coreclr.`</span><span class="sxs-lookup"><span data-stu-id="ecd5a-192">Running the VS Code debugger reports the error: `Failed to find debugger extension for type:coreclr.`</span></span>

### <a name="reason"></a><span data-ttu-id="ecd5a-193">Reason</span><span class="sxs-lookup"><span data-stu-id="ecd5a-193">Reason</span></span>
<span data-ttu-id="ecd5a-194">You do not have the VS Code extension for C# installed on your development machine which includes debugging support for .Net Core (CoreCLR).</span><span class="sxs-lookup"><span data-stu-id="ecd5a-194">You do not have the VS Code extension for C# installed on your development machine which includes debugging support for .Net Core (CoreCLR).</span></span>

### <a name="try"></a><span data-ttu-id="ecd5a-195">Try:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-195">Try:</span></span>
<span data-ttu-id="ecd5a-196">Install the [VS Code extension for C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp).</span><span class="sxs-lookup"><span data-stu-id="ecd5a-196">Install the [VS Code extension for C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp).</span></span>

## <a name="debugging-error-configured-debug-type-coreclr-is-not-supported"></a><span data-ttu-id="ecd5a-197">Debugging error 'Configured debug type 'coreclr' is not supported'</span><span class="sxs-lookup"><span data-stu-id="ecd5a-197">Debugging error 'Configured debug type 'coreclr' is not supported'</span></span>
<span data-ttu-id="ecd5a-198">Running the VS Code debugger reports the error: `Configured debug type 'coreclr' is not supported.`</span><span class="sxs-lookup"><span data-stu-id="ecd5a-198">Running the VS Code debugger reports the error: `Configured debug type 'coreclr' is not supported.`</span></span>

### <a name="reason"></a><span data-ttu-id="ecd5a-199">Reason</span><span class="sxs-lookup"><span data-stu-id="ecd5a-199">Reason</span></span>
<span data-ttu-id="ecd5a-200">You do not have the VS Code extension for Azure Dev Spaces installed on your development machine.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-200">You do not have the VS Code extension for Azure Dev Spaces installed on your development machine.</span></span>

### <a name="try"></a><span data-ttu-id="ecd5a-201">Try:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-201">Try:</span></span>
<span data-ttu-id="ecd5a-202">Install the [VS Code extension for Azure Dev Spaces](get-started-netcore.md).</span><span class="sxs-lookup"><span data-stu-id="ecd5a-202">Install the [VS Code extension for Azure Dev Spaces](get-started-netcore.md).</span></span>

## <a name="the-type-or-namespace-name-mylibrary-could-not-be-found"></a><span data-ttu-id="ecd5a-203">The type or namespace name 'MyLibrary' could not be found</span><span class="sxs-lookup"><span data-stu-id="ecd5a-203">The type or namespace name 'MyLibrary' could not be found</span></span>

### <a name="reason"></a><span data-ttu-id="ecd5a-204">Reason</span><span class="sxs-lookup"><span data-stu-id="ecd5a-204">Reason</span></span> 
<span data-ttu-id="ecd5a-205">The build context is at the project/service level by default, therefore a library project you're using won't be found.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-205">The build context is at the project/service level by default, therefore a library project you're using won't be found.</span></span>

### <a name="try"></a><span data-ttu-id="ecd5a-206">Try:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-206">Try:</span></span>
<span data-ttu-id="ecd5a-207">What needs to be done:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-207">What needs to be done:</span></span>
1. <span data-ttu-id="ecd5a-208">Modify the _azds.yaml_ file to set the build context to the solution level.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-208">Modify the _azds.yaml_ file to set the build context to the solution level.</span></span>
2. <span data-ttu-id="ecd5a-209">Modify the _Dockerfile_ and _Dockerfile.develop_ files to refer to the project (_.csproj_) files correctly, relative to the new build context.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-209">Modify the _Dockerfile_ and _Dockerfile.develop_ files to refer to the project (_.csproj_) files correctly, relative to the new build context.</span></span>
3. <span data-ttu-id="ecd5a-210">Place a _.dockerignore_ file beside the .sln file and modify as needed.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-210">Place a _.dockerignore_ file beside the .sln file and modify as needed.</span></span>

<span data-ttu-id="ecd5a-211">You can find an example at https://github.com/sgreenmsft/buildcontextsample</span><span class="sxs-lookup"><span data-stu-id="ecd5a-211">You can find an example at https://github.com/sgreenmsft/buildcontextsample</span></span>

## <a name="microsoftdevspacesregisteraction-authorization-error"></a><span data-ttu-id="ecd5a-212">'Microsoft.DevSpaces/register/action' authorization error</span><span class="sxs-lookup"><span data-stu-id="ecd5a-212">'Microsoft.DevSpaces/register/action' authorization error</span></span>
<span data-ttu-id="ecd5a-213">You might see the following error when you are managing an Azure Dev Space and you are working in an Azure subscription for which you do not have Owner or Contributor access.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-213">You might see the following error when you are managing an Azure Dev Space and you are working in an Azure subscription for which you do not have Owner or Contributor access.</span></span>
`The client '<User email/Id>' with object id '<Guid>' does not have authorization to perform action 'Microsoft.DevSpaces/register/action' over scope '/subscriptions/<Subscription Id>'.`

### <a name="reason"></a><span data-ttu-id="ecd5a-214">Reason</span><span class="sxs-lookup"><span data-stu-id="ecd5a-214">Reason</span></span>
<span data-ttu-id="ecd5a-215">The selected Azure subscription has not registered the `Microsoft.DevSpaces` namespace.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-215">The selected Azure subscription has not registered the `Microsoft.DevSpaces` namespace.</span></span>

### <a name="try"></a><span data-ttu-id="ecd5a-216">Try:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-216">Try:</span></span>
<span data-ttu-id="ecd5a-217">Someone with Owner or Contributor access to the Azure subscription can run the following Azure CLI command to manually register the `Microsoft.DevSpaces` namespace:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-217">Someone with Owner or Contributor access to the Azure subscription can run the following Azure CLI command to manually register the `Microsoft.DevSpaces` namespace:</span></span>

```cmd
az provider register --namespace Microsoft.DevSpaces
```

## <a name="azure-dev-spaces-doesnt-seem-to-use-my-existing-dockerfile-to-build-a-container"></a><span data-ttu-id="ecd5a-218">Azure Dev Spaces doesn't seem to use my existing Dockerfile to build a container</span><span class="sxs-lookup"><span data-stu-id="ecd5a-218">Azure Dev Spaces doesn't seem to use my existing Dockerfile to build a container</span></span> 

### <a name="reason"></a><span data-ttu-id="ecd5a-219">Reason</span><span class="sxs-lookup"><span data-stu-id="ecd5a-219">Reason</span></span>
<span data-ttu-id="ecd5a-220">Azure Dev Spaces can be configured to point to a specific _Dockerfile_ in your project.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-220">Azure Dev Spaces can be configured to point to a specific _Dockerfile_ in your project.</span></span> <span data-ttu-id="ecd5a-221">If it appears Azure Dev Spaces isn't using the _Dockerfile_ you expect to build your containers, you might need to tell Azure Dev Spaces where it is explicitly.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-221">If it appears Azure Dev Spaces isn't using the _Dockerfile_ you expect to build your containers, you might need to tell Azure Dev Spaces where it is explicitly.</span></span> 

### <a name="try"></a><span data-ttu-id="ecd5a-222">Try:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-222">Try:</span></span>
<span data-ttu-id="ecd5a-223">Open the _azds.yaml_ file that was generated by Azure Dev Spaces in your project.</span><span class="sxs-lookup"><span data-stu-id="ecd5a-223">Open the _azds.yaml_ file that was generated by Azure Dev Spaces in your project.</span></span> <span data-ttu-id="ecd5a-224">Use the `configurations->develop->build->dockerfile` directive to point to the Dockerfile you want to use:</span><span class="sxs-lookup"><span data-stu-id="ecd5a-224">Use the `configurations->develop->build->dockerfile` directive to point to the Dockerfile you want to use:</span></span>

```
...
configurations:
  develop:
    build:
      dockerfile: Dockerfile.develop
```
