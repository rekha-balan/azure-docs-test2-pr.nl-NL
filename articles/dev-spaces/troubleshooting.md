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
# <a name="troubleshooting-guide"></a>Troubleshooting guide

This guide contains information about common problems you may have when using Azure Dev Spaces.

## <a name="enabling-detailed-logging"></a>Enabling detailed logging

In order to troubleshoot problems more effectively, it may help to create more detailed logs for review.

For the Visual Studio extension, you can do this by setting the `MS_VS_AZUREDEVSPACES_TOOLS_LOGGING_ENABLED` environment variable to 1. Be sure to restart Visual Studio for the environment variable to take effect. Once enabled, detailed logs will be written to your `%TEMP%\Microsoft.VisualStudio.Azure.DevSpaces.Tools` directory.

In the CLI, you can output more information during command execution by using the `--verbose` switch.

## <a name="error-failed-to-create-azure-dev-spaces-controller"></a>Error 'Failed to create Azure Dev Spaces controller'

You might see this error when something goes wrong with the creation of the controller. If it's a transient error, deleting and recreating the controller will fix it.

### <a name="try"></a>Try:

To delete the controller, use the Azure Dev Spaces CLI. It’s not possible to do it in Visual Studio or Cloud Shell. To install the AZDS CLI, first install the Azure CLI, and then run this command:

```cmd
az aks use-dev-spaces -g <resource group name> -n <cluster name>
```

And then run this command to delete the controller:

```cmd
azds remove -g <resource group name> -n <cluster name>
```

Recreating the controller can be done from the CLI or Visual Studio. Follow the instructions in the tutorials as if starting for the first time.


## <a name="error-service-cannot-be-started"></a>Error 'Service cannot be started.'

You might see this error when your service code fails to start. The cause is often in user code. To get more diagnostic information, make the following changes to your commands and settings:

### <a name="try"></a>Try:

On the command line:

When using _azds.exe_, use the --verbose command-line option, and use the --output command-line option to specify the output format.
 
    ```cmd
    azds up --verbose --output json
    ```

In Visual Studio:

1. Open **Tools > Options** and under **Projects and Solutions**, choose and **Build and Run**.
2. Change the settings for **MSBuild project build output verbosity** to **Detailed** or **Diagnostic**.

    ![Screenshot of Tools Options dialog](media/common/VerbositySetting.PNG)
    
## <a name="dns-name-resolution-fails-for-a-public-url-associated-with-a-dev-spaces-service"></a>DNS name resolution fails for a public URL associated with a Dev Spaces service

When this happens, you might see a "Page cannot be displayed" or "This site cannot be reached" error in your web browser when attempting to connect to the public URL associated with a Dev Spaces service.

### <a name="try"></a>Try:

You can use the following command to list out all URLs associated with your Dev Spaces services:

```cmd
azds list-uris
```

If a URL is in the *Pending* state, that means that Dev Spaces is still waiting for DNS registration to complete. Sometimes, it takes a few minutes for this to happen. Dev Spaces also opens a localhost tunnel for each service, which you can use while waiting on DNS registration.

If a URL remains in the *Pending* state for more than 5 minutes, it may indicate a problem with the external DNS pod that creates the public endpoint and/or the nginx ingress controller pod that acquires the public endpoint. You can use the following commands to delete these pods. They will be recreated automatically.

```cmd
kubectl delete pod -n kube-system -l app=addon-http-application-routing-external-dns
kubectl delete pod -n kube-system -l app=addon-http-application-routing-nginx-ingress
```

## <a name="error-required-tools-and-configurations-are-missing"></a>Error 'Required tools and configurations are missing'

This error might occur when launching VS Code: "[Azure Dev Spaces] Required tools and configurations to build and debug '[project name]' are missing."
The error means that azds.exe is not in the PATH environment variable, as seen in VS Code.

### <a name="try"></a>Try:

Launch VS Code from a command prompt where the PATH environment variable is set properly.

## <a name="error-azds-is-not-recognized-as-an-internal-or-external-command-operable-program-or-batch-file"></a>Error 'azds' is not recognized as an internal or external command, operable program, or batch file
 
You might see this error if azds.exe is not installed or configured correctly.

### <a name="try"></a>Try:

1. Check the location %ProgramFiles%/Microsoft SDKs\Azure\Azure Dev Spaces CLI (Preview) for azds.exe. If it's there, add that location to the PATH environment variable.
2. If azds.exe is not installed, run the following command:

    ```cmd
    az aks use-dev-spaces -n <cluster-name> -g <resource-group>
    ```

## <a name="warning-dockerfile-could-not-be-generated-due-to-unsupported-language"></a>Warning 'Dockerfile could not be generated due to unsupported language'
Azure Dev Spaces provides native support for C# and Node.js. When you run *azds prep* in a directory containing code written in one of these languages, Azure Dev Spaces will automatically create an appropriate Dockerfile for you.

You can still use Azure Dev Spaces with code written in other languages, but you will need to create the Dockerfile yourself prior to running *azds up* for the first time.

### <a name="try"></a>Try:
If your application is written in a language that Azure Dev Spaces does not natively support, you'll need to provide an appropriate Dockerfile to build a container image running your code. Docker provides a [list of best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) as well as a [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) that can help you do this.

Once you have an appropriate Dockerfile in place, you can proceed with running *azds up* to run your application in Azure Dev Spaces.

## <a name="error-upstream-connect-error-or-disconnectreset-before-headers"></a>Error 'upstream connect error or disconnect/reset before headers'
You may see this error when trying to access your service. For example, when you go to the service's URL in a browser. 

### <a name="reason"></a>Reason 
The container port isn't available. This problem could occur because: 
* The container is still in the process of being built and deployed. This issue can arise if you run `azds up` or start the debugger, and then try to access the container before it has successfully deployed.
* Port configuration is not consistent across your _Dockerfile_, Helm Chart, and any server code that opens up a port.

### <a name="try"></a>Try:
1. If the container is in the process of being built/deployed, you can wait 2-3 seconds and try accessing the service again. 
1. Check your port configuration. The specified port numbers should be **identical** in all the assets below:
    * **Dockerfile:** Specified by the `EXPOSE` instruction.
    * **[Helm chart](https://docs.helm.sh):** Specified by the `externalPort` and `internalPort` values for a service (often located in a `values.yml` file),
    * Any ports being opened up in application code, for example in Node.js: `var server = app.listen(80, function () {...}`


## <a name="config-file-not-found"></a>Config file not found
You run `azds up` and get the following error: `Config file not found: .../azds.yaml`

### <a name="reason"></a>Reason
You must run `azds up` from the root directory of the code you want to run, and you must initialize the code folder to run with Azure Dev Spaces.

### <a name="try"></a>Try:
1. Change your current directory to the root folder containing your service code. 
1. If you do not have a _azds.yaml_ file in the code folder, run `azds prep` to generate Docker, Kubernetes, and Azure Dev Spaces assets.

## <a name="error-the-pipe-program-azds-exited-unexpectedly-with-code-126"></a>Error: 'The pipe program 'azds' exited unexpectedly with code 126.'
Starting the VS Code debugger may sometimes result in this error. This is a known issue.

### <a name="try"></a>Try:
1. Close and reopen VS Code.
2. Hit F5 again.

## <a name="debugging-error-failed-to-find-debugger-extension-for-typecoreclr"></a>Debugging error 'Failed to find debugger extension for type:coreclr'
Running the VS Code debugger reports the error: `Failed to find debugger extension for type:coreclr.`

### <a name="reason"></a>Reason
You do not have the VS Code extension for C# installed on your development machine which includes debugging support for .Net Core (CoreCLR).

### <a name="try"></a>Try:
Install the [VS Code extension for C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp).

## <a name="debugging-error-configured-debug-type-coreclr-is-not-supported"></a>Debugging error 'Configured debug type 'coreclr' is not supported'
Running the VS Code debugger reports the error: `Configured debug type 'coreclr' is not supported.`

### <a name="reason"></a>Reason
You do not have the VS Code extension for Azure Dev Spaces installed on your development machine.

### <a name="try"></a>Try:
Install the [VS Code extension for Azure Dev Spaces](get-started-netcore.md).

## <a name="the-type-or-namespace-name-mylibrary-could-not-be-found"></a>The type or namespace name 'MyLibrary' could not be found

### <a name="reason"></a>Reason 
The build context is at the project/service level by default, therefore a library project you're using won't be found.

### <a name="try"></a>Try:
What needs to be done:
1. Modify the _azds.yaml_ file to set the build context to the solution level.
2. Modify the _Dockerfile_ and _Dockerfile.develop_ files to refer to the project (_.csproj_) files correctly, relative to the new build context.
3. Place a _.dockerignore_ file beside the .sln file and modify as needed.

You can find an example at https://github.com/sgreenmsft/buildcontextsample

## <a name="microsoftdevspacesregisteraction-authorization-error"></a>'Microsoft.DevSpaces/register/action' authorization error
You might see the following error when you are managing an Azure Dev Space and you are working in an Azure subscription for which you do not have Owner or Contributor access.
`The client '<User email/Id>' with object id '<Guid>' does not have authorization to perform action 'Microsoft.DevSpaces/register/action' over scope '/subscriptions/<Subscription Id>'.`

### <a name="reason"></a>Reason
The selected Azure subscription has not registered the `Microsoft.DevSpaces` namespace.

### <a name="try"></a>Try:
Someone with Owner or Contributor access to the Azure subscription can run the following Azure CLI command to manually register the `Microsoft.DevSpaces` namespace:

```cmd
az provider register --namespace Microsoft.DevSpaces
```

## <a name="azure-dev-spaces-doesnt-seem-to-use-my-existing-dockerfile-to-build-a-container"></a>Azure Dev Spaces doesn't seem to use my existing Dockerfile to build a container 

### <a name="reason"></a>Reason
Azure Dev Spaces can be configured to point to a specific _Dockerfile_ in your project. If it appears Azure Dev Spaces isn't using the _Dockerfile_ you expect to build your containers, you might need to tell Azure Dev Spaces where it is explicitly. 

### <a name="try"></a>Try:
Open the _azds.yaml_ file that was generated by Azure Dev Spaces in your project. Use the `configurations->develop->build->dockerfile` directive to point to the Dockerfile you want to use:

```
...
configurations:
  develop:
    build:
      dockerfile: Dockerfile.develop
```
