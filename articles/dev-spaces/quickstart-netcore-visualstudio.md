---
title: Create a Kubernetes dev space in the cloud | Microsoft Docs
titleSuffix: Azure Dev Spaces
author: ghogen
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
ms.author: ghogen
ms.date: 07/09/2018
ms.topic: quickstart
description: Rapid Kubernetes development with containers and microservices on Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Kubernetes Service, containers
manager: douge
ms.openlocfilehash: 600625f143041eaf983b7ec7e945c5a968b522f5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855671"
---
# <a name="quickstart-create-a-kubernetes-dev-space-with-azure-dev-spaces-net-core-and-visual-studio"></a>Quickstart: Create a Kubernetes dev space with Azure Dev Spaces (.NET Core and Visual Studio)

In this guide, you will learn how to:

- Set up Azure Dev Spaces with a managed Kubernetes cluster in Azure.
- Iteratively develop code in containers using Visual Studio.
- Debug code running in your cluster.

> [!Note]
> **If you get stuck** at any time, see the [Troubleshooting](troubleshooting.md) section, or post a comment on this page. You can also try the more detailed [tutorial](get-started-netcore-visualstudio.md).

## <a name="prerequisites"></a>Prerequisites

- A Kubernetes cluster running Kubernetes 1.9.6 or later, in the EastUS, CentralUS, WestUS2, WestEurope, CanadaCentral, or CanadaEast region, with Http Application Routing enabled.

  ![Be sure to enable Http Application Routing.](media/common/Kubernetes-Create-Cluster-3.PNG)

- Visual Studio 2017 with the Web Development workload installed. If you don't have it installed, download it [here](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).

## <a name="set-up-azure-dev-spaces"></a>Set up Azure Dev Spaces

Install [Visual Studio Tools for Kubernetes](https://aka.ms/get-azds-visualstudio).

## <a name="connect-to-a-cluster"></a>Connect to a cluster

Next, you'll create and configure a project for Azure Dev Spaces.

### <a name="create-an-aspnet-web-app"></a>Create an ASP.NET web app

From within Visual Studio 2017, create a new project. Currently, the project must be an **ASP.NET Core Web Application**. Name the project **webfrontend**.

Select the **Web Application (Model-View-Controller)** template and be sure you're targeting **.NET Core** and **ASP.NET Core 2.0**.

### <a name="enable-dev-spaces-for-an-aks-cluster"></a>Enable Dev Spaces for an AKS cluster

With the project you just created, select **Azure Dev Spaces** from the launch settings dropdown, as shown below.

![](media/get-started-netcore-visualstudio/LaunchSettings.png)

In the dialog that is displayed next, make sure you are signed in with the appropriate account, and then select an existing cluster.

![](media/get-started-netcore-visualstudio/Azure-Dev-Spaces-Dialog.png)

Leave the **Space** dropdown set to `default` for now. Check the **Publicly Accessible** checkbox so the web app will be accessible via a public endpoint.

![](media/get-started-netcore-visualstudio/Azure-Dev-Spaces-Dialog2.png)

Click **OK** to select or create the cluster.

If you choose a cluster that hasn't been configured to work with Azure Dev Spaces, you'll see a message asking if you want to configure it.

![](media/get-started-netcore-visualstudio/Add-Azure-Dev-Spaces-Resource.png)

Choose **OK**. 

### <a name="look-at-the-files-added-to-project"></a>Look at the files added to project
While you wait for the dev space to be created, look at the files that have been added to your project when you chose to use Azure Dev Spaces.

- A folder named `charts` has been added and within this folder a [Helm chart](https://docs.helm.sh) for your application has been scaffolded. These files are used to deploy your application into the dev space.
- `Dockerfile` has information needed to package your application in the standard Docker format.
- `azds.yaml` contains development-time configuration that is needed by the dev space.

![](media/get-started-netcore-visualstudio/ProjectFiles.png)

## <a name="debug-a-container-in-kubernetes"></a>Debug a container in Kubernetes
Once the dev space is successfully created, you can debug the application. Set a breakpoint in the code, for example on line 20 in the file `HomeController.cs` where the `Message` variable is set. Click **F5** to start debugging. 

Visual Studio will communicate with the dev space to build and deploy the application and then open a browser with the web app running. It might seem like the container is running locally, but actually it's running in the dev space in Azure. The reason for the localhost address is because Azure Dev Spaces creates a temporary SSH tunnel to the container running in AKS.

Click on the **About** link at the top of the page to trigger the breakpoint. You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, and so on.


## <a name="iteratively-develop-code"></a>Iteratively develop code

Azure Dev Spaces isn't just about getting code running in Kubernetes - it's about enabling you to quickly and iteratively see your code changes take effect in a Kubernetes environment in the cloud.

### <a name="update-a-content-file"></a>Update a content file
1. Locate the file `./Views/Home/Index.cshtml` and make an edit to the HTML. For example, change line 70 that reads `<h2>Application uses</h2>` to something like: `<h2>Hello k8s in Azure!</h2>`
1. Save the file.
1. Go to your browser and refresh the page. You should see the web page display the updated HTML.

What happened? Edits to content files, like HTML and CSS, don't require recompilation in a .NET Core web app, so an active F5 session automatically syncs any modified content files into the running container in AKS, so you can see your content edits right away.

### <a name="update-a-code-file"></a>Update a code file
Updating code files requires a little more work, because a .NET Core app needs to rebuild and produce updated application binaries.

1. Stop the debugger in Visual Studio.
1. Open the code file named `Controllers/HomeController.cs`, and edit the message that the About page will display: `ViewData["Message"] = "Your application description page.";`
1. Save the file.
1. Press **F5** to start debugging again. 

Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will incrementally recompile code within the existing container to provide a faster edit/debug loop.

Refresh the web app in the browser, and go to the About page. You should see your custom message appear in the UI.


## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Working with multiple containers and team development](team-development-netcore-visualstudio.md)
