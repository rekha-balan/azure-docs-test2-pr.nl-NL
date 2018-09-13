---
title: Debugging apps in a local Docker container | Microsoft Docs
description: Learn how to modify an app that is running in a local Docker container, refresh the container via Edit and Refresh and set debugging breakpoints
services: azure-container-service
documentationcenter: na
author: ghogen
manager: douge
editor: ''
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: 07a7c1e11d8ca20ff4f42abcb84961cb7cd9e0e1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809561"
---
# <a name="debugging-apps-in-a-local-docker-container"></a>Debugging apps in a local Docker container
## <a name="overview"></a>Overview
Visual Studio 2017 provides a consistent way to develop in a Linux Docker container and validate your application locally.
You don't have to restart the container each time you make a code change.
This article illustrates how to use the "Edit and Refresh" feature to start an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh the browser to see those changes.
This article also shows you how to set breakpoints for debugging.

> [!NOTE]
> Windows Container support will be coming in a future release
>
>

## <a name="prerequisites"></a>Prerequisites
The following tools must be installed.

* [Visual Studio 2017](https://www.visualstudio.com/downloads/)
* [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)

To run Docker containers locally, you'll need a local docker client.
You can use the [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V to be disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.

If using Docker Toolbox, you'll need to [configure the Docker client](vs-azure-tools-docker-setup.md)

## <a name="1-create-a-web-app"></a>1. Create a web app
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Add Docker support
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a>3. Edit your code and refresh
To quickly iterate changes, you can start your application within a container, and continue to make changes, viewing them as you would with IIS Express.

1. Set the Solution Configuration to `Debug` and press **&lt;CTRL + F5>** to build your docker image and run it locally.

    Once the container image has been built and is running in a Docker container, Visual Studio launches the Web app in your default browser.
    If you are using the Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.
2. Go to the About page, which is where we're going to make our changes.
3. Return to Visual Studio and open `Views\Home\About.cshtml`.
4. Add the following HTML content to the end of the file and save the changes.

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. Viewing the output window, when the .NET build is completed and you see these lines, switch back to your browser and refresh the About page.

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C to shut down
   ```
6. Your changes have been applied!

## <a name="4-debug-with-breakpoints"></a>4. Debug with breakpoints
Often, changes will need further inspection, leveraging the debugging features of Visual Studio.

1. Return to Visual Studio and open `Controllers\HomeController.cs`
2. Replace the contents of the About() method with the following:

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. Set a breakpoint to the left of the `string message`... line.
4. Hit **&lt;F5>** to start debugging.
5. Navigate to the About page to hit your breakpoint.
6. Switch to Visual Studio to view the breakpoint, and inspect the value of message.

   ![][2]

## <a name="summary"></a>Summary
With Docker support in Visual Studio 2017, you can get the productivity of working locally, with the production realism of developing within a Docker container.

## <a name="troubleshooting"></a>Troubleshooting
[Troubleshooting Visual Studio Docker Development](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>More about Docker with Visual Studio, Windows, and Azure
* [Docker Tools for Azure DevOps](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers
* [Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming
* [Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information
* [Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)
* For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/). For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).

## <a name="various-docker-tools"></a>Various Docker tools
[Some great docker tools (Steve Lasker's blog)](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a>Good articles
[Introduction to Microservices from NGINX](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a>Presentations
* [Steve Lasker: VS Live Las Vegas 2016 - Docker e2e](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [Introduction to ASP.NET Core @ build 2016 - Where You At Demo](https://channel9.msdn.com/Events/Build/2016/B810)
* [Developing .NET apps in containers, Channel 9](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
