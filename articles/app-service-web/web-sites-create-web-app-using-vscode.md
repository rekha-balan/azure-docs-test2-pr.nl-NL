---
title: Create an ASP.NET 5 web app in Visual Studio Code
description: This tutorial illustrates how to create an ASP.NET 5 web app using Visual Studio Code.
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 9addadb087b95244e12a7bf582a1b94a2820e2a6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550117"
---
# <a name="create-an-aspnet-5-web-app-in-visual-studio-code"></a><span data-ttu-id="bcc8f-103">Create an ASP.NET 5 web app in Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="bcc8f-103">Create an ASP.NET 5 web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="bcc8f-104">Overview</span><span class="sxs-lookup"><span data-stu-id="bcc8f-104">Overview</span></span>
<span data-ttu-id="bcc8f-105">This tutorial shows you how to create an ASP.NET 5 web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it to [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="bcc8f-105">This tutorial shows you how to create an ASP.NET 5 web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it to [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="bcc8f-106">Although this article refers to web apps, it also applies to API apps and mobile apps.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-106">Although this article refers to web apps, it also applies to API apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="bcc8f-107">ASP.NET 5 is a significant redesign of ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-107">ASP.NET 5 is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="bcc8f-108">ASP.NET 5 is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-108">ASP.NET 5 is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="bcc8f-109">For more information, see [Introduction to ASP.NET 5](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="bcc8f-109">For more information, see [Introduction to ASP.NET 5](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="bcc8f-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bcc8f-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="bcc8f-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bcc8f-111">Prerequisites</span></span>
* <span data-ttu-id="bcc8f-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="bcc8f-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="bcc8f-113">Install [Node.js](http://nodejs.org) - Node.js is a platform for building fast and scalable server applications using JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-113">Install [Node.js](http://nodejs.org) - Node.js is a platform for building fast and scalable server applications using JavaScript.</span></span> <span data-ttu-id="bcc8f-114">Node is the runtime (Node), and [npm](http://www.npmjs.com/) is the Package Manager for Node modules.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-114">Node is the runtime (Node), and [npm](http://www.npmjs.com/) is the Package Manager for Node modules.</span></span> <span data-ttu-id="bcc8f-115">You will use npm to scaffold an ASP.NET 5 web app in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-115">You will use npm to scaffold an ASP.NET 5 web app in this tutorial.</span></span>
* <span data-ttu-id="bcc8f-116">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="bcc8f-116">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads).</span></span> <span data-ttu-id="bcc8f-117">If you are new to Git, choose [git-scm.com](http://git-scm.com/downloads) and select the option to **Use Git from the Windows Command Prompt**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-117">If you are new to Git, choose [git-scm.com](http://git-scm.com/downloads) and select the option to **Use Git from the Windows Command Prompt**.</span></span> <span data-ttu-id="bcc8f-118">Once you install Git, you'll also need to set the Git user name and email as it's required later in the tutorial (when performing a commit from VS Code).</span><span class="sxs-lookup"><span data-stu-id="bcc8f-118">Once you install Git, you'll also need to set the Git user name and email as it's required later in the tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-5-and-dnx"></a><span data-ttu-id="bcc8f-119">Install ASP.NET 5 and DNX</span><span class="sxs-lookup"><span data-stu-id="bcc8f-119">Install ASP.NET 5 and DNX</span></span>
<span data-ttu-id="bcc8f-120">ASP.NET 5/DNX (the .NET Execution Environment) is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-120">ASP.NET 5/DNX (the .NET Execution Environment) is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="bcc8f-121">It has been built from the ground up to provide an optimized development framework for apps that are either deployed to the cloud or run on-premises.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-121">It has been built from the ground up to provide an optimized development framework for apps that are either deployed to the cloud or run on-premises.</span></span> <span data-ttu-id="bcc8f-122">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-122">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="bcc8f-123">This tutorial is designed to get you started building applications with the latest development versions of ASP.NET 5 and DNX.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-123">This tutorial is designed to get you started building applications with the latest development versions of ASP.NET 5 and DNX.</span></span> <span data-ttu-id="bcc8f-124">The following instructions are specific to Windows.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-124">The following instructions are specific to Windows.</span></span> <span data-ttu-id="bcc8f-125">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET 5 and DNX](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="bcc8f-125">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET 5 and DNX](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 

1. <span data-ttu-id="bcc8f-126">To install .NET Version Manager (DNVM) in Windows, open a command prompt, and run the following command.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-126">To install .NET Version Manager (DNVM) in Windows, open a command prompt, and run the following command.</span></span>
   
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "&{$Branch='dev';iex ((new-object net.webclient).DownloadString('https://raw.githubusercontent.com/aspnet/Home/dev/dnvminstall.ps1'))}"
   
    <span data-ttu-id="bcc8f-127">This will download the DNVM script and put it in your user profile directory.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-127">This will download the DNVM script and put it in your user profile directory.</span></span> 
2. <span data-ttu-id="bcc8f-128">**Restart Windows** to complete the DNVM installation.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-128">**Restart Windows** to complete the DNVM installation.</span></span> 
   
    <span data-ttu-id="bcc8f-129">After you have restarted Windows, you can open the command prompt to verify the location of DNVM by entering the following:</span><span class="sxs-lookup"><span data-stu-id="bcc8f-129">After you have restarted Windows, you can open the command prompt to verify the location of DNVM by entering the following:</span></span>
   
        where dnvm
   
    <span data-ttu-id="bcc8f-130">The command prompt will show a path similar to the following.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-130">The command prompt will show a path similar to the following.</span></span>
   
    ![dnvm location](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/00-where-dnvm.png)
3. <span data-ttu-id="bcc8f-132">Now that you have DNVM, you must use it to download DNX to run your applications.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-132">Now that you have DNVM, you must use it to download DNX to run your applications.</span></span> <span data-ttu-id="bcc8f-133">Run the following at the command prompt:</span><span class="sxs-lookup"><span data-stu-id="bcc8f-133">Run the following at the command prompt:</span></span>
   
        dnvm upgrade
   
    <span data-ttu-id="bcc8f-134">Verify your DNVM, and view the active runtime by entering the following at the command prompt:</span><span class="sxs-lookup"><span data-stu-id="bcc8f-134">Verify your DNVM, and view the active runtime by entering the following at the command prompt:</span></span>
   
        dnvm list
   
    <span data-ttu-id="bcc8f-135">The command prompt will show the details of the active runtime.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-135">The command prompt will show the details of the active runtime.</span></span>
   
    ![DNVM location](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/00b-dnvm-list.png)
   
    <span data-ttu-id="bcc8f-137">If more than one DNX runtime is listed, you can choose to enter the following (or a more recent version) at the command prompt to set the active DNX runtime.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-137">If more than one DNX runtime is listed, you can choose to enter the following (or a more recent version) at the command prompt to set the active DNX runtime.</span></span> <span data-ttu-id="bcc8f-138">Set it to the same version that is used by the ASP.NET 5 generator when you create your web app later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-138">Set it to the same version that is used by the ASP.NET 5 generator when you create your web app later in this tutorial.</span></span> <span data-ttu-id="bcc8f-139">*You may not need to change the active runtime if it is set to the latest available.*</span><span class="sxs-lookup"><span data-stu-id="bcc8f-139">*You may not need to change the active runtime if it is set to the latest available.*</span></span>
   
        dnvm use 1.0.0-update1 –p

> [!NOTE]
> <span data-ttu-id="bcc8f-140">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET 5 and DNX](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="bcc8f-140">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET 5 and DNX](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-the-web-app"></a><span data-ttu-id="bcc8f-141">Create the web app</span><span class="sxs-lookup"><span data-stu-id="bcc8f-141">Create the web app</span></span>
<span data-ttu-id="bcc8f-142">This section shows you how to scaffold a new app ASP.NET web app.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-142">This section shows you how to scaffold a new app ASP.NET web app.</span></span> <span data-ttu-id="bcc8f-143">You will use the node package manager (npm) to install [Yeoman](http://yeoman.io/) (application scaffolding tool - the VS Code equivalent of the Visual Studio **File > New Project** operation), [Grunt](http://gruntjs.com/) (JavaScript task runner), and [Bower](http://bower.io/) (client side package manager).</span><span class="sxs-lookup"><span data-stu-id="bcc8f-143">You will use the node package manager (npm) to install [Yeoman](http://yeoman.io/) (application scaffolding tool - the VS Code equivalent of the Visual Studio **File > New Project** operation), [Grunt](http://gruntjs.com/) (JavaScript task runner), and [Bower](http://bower.io/) (client side package manager).</span></span> 

1. <span data-ttu-id="bcc8f-144">Open a command prompt with Administrator rights and navigate to the location where you want to create your ASP.NET project.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-144">Open a command prompt with Administrator rights and navigate to the location where you want to create your ASP.NET project.</span></span> <span data-ttu-id="bcc8f-145">For instance, create a *vscodeprojects* directory at the root of C:\.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-145">For instance, create a *vscodeprojects* directory at the root of C:\.</span></span>
2. <span data-ttu-id="bcc8f-146">Enter the following at the command prompt to install Yeoman and the supporting tools.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-146">Enter the following at the command prompt to install Yeoman and the supporting tools.</span></span>
   
        npm install -g yo grunt-cli generator-aspnet bower
   
   > [!NOTE]
   > <span data-ttu-id="bcc8f-147">You may get a warning suggesting that your npm version is out of date.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-147">You may get a warning suggesting that your npm version is out of date.</span></span> <span data-ttu-id="bcc8f-148">This warning should not affect this tutorial.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-148">This warning should not affect this tutorial.</span></span>
   > 
   > 
3. <span data-ttu-id="bcc8f-149">Enter the following at the command prompt to create the project folder and scaffold the app.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-149">Enter the following at the command prompt to create the project folder and scaffold the app.</span></span>
   
        yo aspnet
4. <span data-ttu-id="bcc8f-150">Use the arrow keys to select the **Web Application Basic** type from the ASP.NET 5 generator menu, and press **&lt;Enter>**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-150">Use the arrow keys to select the **Web Application Basic** type from the ASP.NET 5 generator menu, and press **&lt;Enter>**.</span></span>
   
    ![Yeoman - ASP.NET 5 generator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/01-yo-aspnet.png)
5. <span data-ttu-id="bcc8f-152">Set the name of your new ASP.NET web app to **SampleWebApp**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-152">Set the name of your new ASP.NET web app to **SampleWebApp**.</span></span> <span data-ttu-id="bcc8f-153">As this name is used throughout the tutorial, if you select a different name, you'll need to substitute it for each occurrence of **SampleWebApp**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-153">As this name is used throughout the tutorial, if you select a different name, you'll need to substitute it for each occurrence of **SampleWebApp**.</span></span> <span data-ttu-id="bcc8f-154">When you press **&lt;Enter>**, Yeoman will create a new folder named **SampleWebApp** and the necessary files for your new app.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-154">When you press **&lt;Enter>**, Yeoman will create a new folder named **SampleWebApp** and the necessary files for your new app.</span></span>
6. <span data-ttu-id="bcc8f-155">At the command prompt, change directories to your new project folder:</span><span class="sxs-lookup"><span data-stu-id="bcc8f-155">At the command prompt, change directories to your new project folder:</span></span>
   
        cd SampleWebApp
7. <span data-ttu-id="bcc8f-156">Also at the command prompt, to install the necessary NuGet packages to run the application, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="bcc8f-156">Also at the command prompt, to install the necessary NuGet packages to run the application, enter the following command:</span></span>
   
        dnu restore
8. <span data-ttu-id="bcc8f-157">Open VS Code by entering the following at the command prompt:</span><span class="sxs-lookup"><span data-stu-id="bcc8f-157">Open VS Code by entering the following at the command prompt:</span></span>
   
        code .

## <a name="run-the-web-app-locally"></a><span data-ttu-id="bcc8f-158">Run the web app locally</span><span class="sxs-lookup"><span data-stu-id="bcc8f-158">Run the web app locally</span></span>
<span data-ttu-id="bcc8f-159">Now that you have created the web app and retrieved all the NuGet packages for the app, you can run the web app locally.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-159">Now that you have created the web app and retrieved all the NuGet packages for the app, you can run the web app locally.</span></span>

1. <span data-ttu-id="bcc8f-160">From the **Command Palette** in VS Code, enter the following to show the available run command options:</span><span class="sxs-lookup"><span data-stu-id="bcc8f-160">From the **Command Palette** in VS Code, enter the following to show the available run command options:</span></span>
   
        dnx: Run Command
   
   > [!NOTE]
   > <span data-ttu-id="bcc8f-161">If the Omnisharp server is not currently running, it will start up.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-161">If the Omnisharp server is not currently running, it will start up.</span></span> <span data-ttu-id="bcc8f-162">Re-enter the above command.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-162">Re-enter the above command.</span></span>
   > 
   > 
   
    <span data-ttu-id="bcc8f-163">Next, select the following command to run your web app:</span><span class="sxs-lookup"><span data-stu-id="bcc8f-163">Next, select the following command to run your web app:</span></span>
   
        dnx web - (SampleWebApp)
   
    <span data-ttu-id="bcc8f-164">The command window will display that the application has started.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-164">The command window will display that the application has started.</span></span> <span data-ttu-id="bcc8f-165">If the command window doesn't display this message, check the lower left corning of VS Code for errors in your project.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-165">If the command window doesn't display this message, check the lower left corning of VS Code for errors in your project.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bcc8f-166">Issuing a command from the **Command Palette** requires a **>** character at the beginning of the command line.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-166">Issuing a command from the **Command Palette** requires a **>** character at the beginning of the command line.</span></span> <span data-ttu-id="bcc8f-167">You can view the details related to the **web** command in the *project.json* file.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-167">You can view the details related to the **web** command in the *project.json* file.</span></span>   
   > <span data-ttu-id="bcc8f-168">If the command does not appear or is not available, you may need to install the C# extension.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-168">If the command does not appear or is not available, you may need to install the C# extension.</span></span> <span data-ttu-id="bcc8f-169">Run  `>Extensions: Install Extension` and `ext install c#` to install the C# extensions.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-169">Run  `>Extensions: Install Extension` and `ext install c#` to install the C# extensions.</span></span>
   > 
   > 
2. <span data-ttu-id="bcc8f-170">Open a browser and navigate to the following URL.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-170">Open a browser and navigate to the following URL.</span></span>
   
    **http://localhost:5000**
   
    <span data-ttu-id="bcc8f-171">The default page of the web app will appear as follows.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-171">The default page of the web app will appear as follows.</span></span>
   
    ![Local web app in a browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="bcc8f-173">Close your browser.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-173">Close your browser.</span></span> <span data-ttu-id="bcc8f-174">In the **Command Window**, press **Ctrl+C** to shut down the application and close the **Command Window**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-174">In the **Command Window**, press **Ctrl+C** to shut down the application and close the **Command Window**.</span></span> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="bcc8f-175">Create a web app in the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bcc8f-175">Create a web app in the Azure Portal</span></span>
<span data-ttu-id="bcc8f-176">The following steps will guide you through creating a web app in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-176">The following steps will guide you through creating a web app in the Azure Portal.</span></span>

1. <span data-ttu-id="bcc8f-177">Log in to the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bcc8f-177">Log in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bcc8f-178">Click **NEW** at the top left of the Portal.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-178">Click **NEW** at the top left of the Portal.</span></span>
3. <span data-ttu-id="bcc8f-179">Click **Web Apps > Web App**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-179">Click **Web Apps > Web App**.</span></span>
   
    ![Azure new web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="bcc8f-181">Enter a value for **Name**, such as **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-181">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="bcc8f-182">Note that this name needs to be unique, and the portal will enforce that when you attempt to enter the name.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-182">Note that this name needs to be unique, and the portal will enforce that when you attempt to enter the name.</span></span> <span data-ttu-id="bcc8f-183">Therefore, if you select a enter a different value, you'll need to substitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-183">Therefore, if you select a enter a different value, you'll need to substitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="bcc8f-184">Select an existing **App Service Plan** or create a new one.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-184">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="bcc8f-185">If you create a new plan, select the pricing tier, location, and other options.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-185">If you create a new plan, select the pricing tier, location, and other options.</span></span> <span data-ttu-id="bcc8f-186">For more information on App Service plans, see the article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bcc8f-186">For more information on App Service plans, see the article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Azure new web app blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="bcc8f-188">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-188">Click **Create**.</span></span>
   
    ![web app blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a><span data-ttu-id="bcc8f-190">Enable Git publishing for the new web app</span><span class="sxs-lookup"><span data-stu-id="bcc8f-190">Enable Git publishing for the new web app</span></span>
<span data-ttu-id="bcc8f-191">Git is a distributed version control system that you can use to deploy your Azure App Service web app.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-191">Git is a distributed version control system that you can use to deploy your Azure App Service web app.</span></span> <span data-ttu-id="bcc8f-192">You'll store the code you write for your web app in a local Git repository, and you'll deploy your code to Azure by pushing to a remote repository.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-192">You'll store the code you write for your web app in a local Git repository, and you'll deploy your code to Azure by pushing to a remote repository.</span></span>   

1. <span data-ttu-id="bcc8f-193">Log into the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bcc8f-193">Log into the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bcc8f-194">Click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-194">Click **Browse**.</span></span>
3. <span data-ttu-id="bcc8f-195">Click **Web Apps** to view a list of the web apps associated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-195">Click **Web Apps** to view a list of the web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="bcc8f-196">Select the web app you created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-196">Select the web app you created in this tutorial.</span></span>
5. <span data-ttu-id="bcc8f-197">In the web app blade, click **Settings** > **Continuous deployment**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-197">In the web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Azure web app host](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="bcc8f-199">Click **Choose Source > Local Git Repository**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-199">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="bcc8f-200">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-200">Click **OK**.</span></span>
   
    ![Azure Local Git Respository](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="bcc8f-202">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span><span class="sxs-lookup"><span data-stu-id="bcc8f-202">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="bcc8f-203">Click **Settings** > **Deployment credentials**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-203">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="bcc8f-204">The **Set deployment credentials** blade will be displayed.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-204">The **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="bcc8f-205">Create a user name and password.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-205">Create a user name and password.</span></span>  <span data-ttu-id="bcc8f-206">You'll need this password later when setting up Git.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-206">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="bcc8f-207">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-207">Click **Save**.</span></span>
9. <span data-ttu-id="bcc8f-208">In your web app's blade, click **Settings > Properties**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-208">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="bcc8f-209">The URL of the remote Git repository that you'll deploy to is shown under **GIT URL**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-209">The URL of the remote Git repository that you'll deploy to is shown under **GIT URL**.</span></span>
10. <span data-ttu-id="bcc8f-210">Copy the **GIT URL** value for later use in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-210">Copy the **GIT URL** value for later use in the tutorial.</span></span>
    
    ![Azure Git URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-to-azure-app-service"></a><span data-ttu-id="bcc8f-212">Publish your web app to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="bcc8f-212">Publish your web app to Azure App Service</span></span>
<span data-ttu-id="bcc8f-213">In this section, you will create a local Git repository and push from that repository to Azure to deploy your web app to Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-213">In this section, you will create a local Git repository and push from that repository to Azure to deploy your web app to Azure.</span></span>

1. <span data-ttu-id="bcc8f-214">In VS Code, select the **Git** option in the left navigation bar.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-214">In VS Code, select the **Git** option in the left navigation bar.</span></span>
   
    ![Git icon in VS Code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="bcc8f-216">Select **Initialize git repository** to make sure your workspace is under git source control.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-216">Select **Initialize git repository** to make sure your workspace is under git source control.</span></span> 
   
    ![Initialize Git](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="bcc8f-218">Open the Command Window and change directories to the directory of your web app.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-218">Open the Command Window and change directories to the directory of your web app.</span></span> <span data-ttu-id="bcc8f-219">Then, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="bcc8f-219">Then, enter the following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="bcc8f-220">This command prevents an issue about text where CRLF endings and LF endings are involved.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-220">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="bcc8f-221">In VS Code, add a commit message and click the **Commit All** check icon.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-221">In VS Code, add a commit message and click the **Commit All** check icon.</span></span>
   
    ![Git Commit All](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="bcc8f-223">After Git has completed processing, you'll see that there are no files listed in the Git window under **Changes**.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-223">After Git has completed processing, you'll see that there are no files listed in the Git window under **Changes**.</span></span> 
   
    ![Git no changes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="bcc8f-225">Change back to the Command Window where the command prompt points to the directory where your web app is located.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-225">Change back to the Command Window where the command prompt points to the directory where your web app is located.</span></span>
7. <span data-ttu-id="bcc8f-226">Create a remote reference for pushing updates to your web app by using the Git URL (ending in ".git") that you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-226">Create a remote reference for pushing updates to your web app by using the Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="bcc8f-227">Configure Git to save your credentials locally so that they will be automatically appended to your push commands generated from VS Code.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-227">Configure Git to save your credentials locally so that they will be automatically appended to your push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="bcc8f-228">Push your changes to Azure by entering the following command.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-228">Push your changes to Azure by entering the following command.</span></span> <span data-ttu-id="bcc8f-229">After this initial push to Azure, you will be able to do all the push commands from VS Code.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-229">After this initial push to Azure, you will be able to do all the push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="bcc8f-230">You are prompted for the password you created earlier in Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-230">You are prompted for the password you created earlier in Azure.</span></span> <span data-ttu-id="bcc8f-231">**Note: Your password will not be visible.**</span><span class="sxs-lookup"><span data-stu-id="bcc8f-231">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="bcc8f-232">The output from the above command ends with a message that deployment is successful.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-232">The output from the above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        To https://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="bcc8f-233">If you make changes to your app, you can republish directly in VS Code using the built-in Git functionality by selecting the **Commit All** option followed by the **Push** option.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-233">If you make changes to your app, you can republish directly in VS Code using the built-in Git functionality by selecting the **Commit All** option followed by the **Push** option.</span></span> <span data-ttu-id="bcc8f-234">You will find the **Push** option available in the drop-down menu next to the **Commit All** and **Refresh** buttons.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-234">You will find the **Push** option available in the drop-down menu next to the **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="bcc8f-235">If you need to collaborate on a project, you should consider pushing to GitHub in between pushing to Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-235">If you need to collaborate on a project, you should consider pushing to GitHub in between pushing to Azure.</span></span>

## <a name="run-the-app-in-azure"></a><span data-ttu-id="bcc8f-236">Run the app in Azure</span><span class="sxs-lookup"><span data-stu-id="bcc8f-236">Run the app in Azure</span></span>
<span data-ttu-id="bcc8f-237">Now that you have deployed your web app, let's run the app while hosted in Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-237">Now that you have deployed your web app, let's run the app while hosted in Azure.</span></span> 

<span data-ttu-id="bcc8f-238">This can be done in two ways:</span><span class="sxs-lookup"><span data-stu-id="bcc8f-238">This can be done in two ways:</span></span>

* <span data-ttu-id="bcc8f-239">Open a browser and enter the name of your web app as follows.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-239">Open a browser and enter the name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="bcc8f-240">In the Azure Portal, locate the web app blade for your web app, and click **Browse** to view your app</span><span class="sxs-lookup"><span data-stu-id="bcc8f-240">In the Azure Portal, locate the web app blade for your web app, and click **Browse** to view your app</span></span> 
* <span data-ttu-id="bcc8f-241">in your default browser.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-241">in your default browser.</span></span>

![Azure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="bcc8f-243">Summary</span><span class="sxs-lookup"><span data-stu-id="bcc8f-243">Summary</span></span>
<span data-ttu-id="bcc8f-244">In this tutorial, you learned how to create a web app in VS Code and deploy it to Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc8f-244">In this tutorial, you learned how to create a web app in VS Code and deploy it to Azure.</span></span> <span data-ttu-id="bcc8f-245">For more information about VS Code, see the article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="bcc8f-245">For more information about VS Code, see the article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="bcc8f-246">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bcc8f-246">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 
















