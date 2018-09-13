---
title: Python web apps with Bottle in Azure
description: A tutorial that introduces you to running a Python web app in Azure App Service Web Apps.
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: ''
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 22ad4786568eea928c751bebe1a6cdf628db14b4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540902"
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="47f47-103">Creating web apps with Bottle in Azure</span><span class="sxs-lookup"><span data-stu-id="47f47-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="47f47-104">This tutorial describes how to get started running Python in Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="47f47-104">This tutorial describes how to get started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="47f47-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span><span class="sxs-lookup"><span data-stu-id="47f47-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="47f47-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span><span class="sxs-lookup"><span data-stu-id="47f47-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="47f47-107">You will create a web app using the Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="47f47-107">You will create a web app using the Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="47f47-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span><span class="sxs-lookup"><span data-stu-id="47f47-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="47f47-109">Then you will run the web app locally, make changes, commit and push them to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="47f47-109">Then you will run the web app locally, make changes, commit and push them to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="47f47-110">The tutorial shows how to do this from Windows or Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="47f47-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="47f47-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="47f47-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="47f47-112">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="47f47-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="47f47-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="47f47-113">Prerequisites</span></span>
* <span data-ttu-id="47f47-114">Windows, Mac or Linux</span><span class="sxs-lookup"><span data-stu-id="47f47-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="47f47-115">Python 2.7 or 3.4</span><span class="sxs-lookup"><span data-stu-id="47f47-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="47f47-116">setuptools, pip, virtualenv (Python 2.7 only)</span><span class="sxs-lookup"><span data-stu-id="47f47-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="47f47-117">Git</span><span class="sxs-lookup"><span data-stu-id="47f47-117">Git</span></span>
* <span data-ttu-id="47f47-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span><span class="sxs-lookup"><span data-stu-id="47f47-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="47f47-119">**Note**: TFS publishing is currently not supported for Python projects.</span><span class="sxs-lookup"><span data-stu-id="47f47-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="47f47-120">Windows</span><span class="sxs-lookup"><span data-stu-id="47f47-120">Windows</span></span>
<span data-ttu-id="47f47-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="47f47-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="47f47-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span><span class="sxs-lookup"><span data-stu-id="47f47-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="47f47-123">Alternatively, you can get Python from [python.org].</span><span class="sxs-lookup"><span data-stu-id="47f47-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="47f47-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span><span class="sxs-lookup"><span data-stu-id="47f47-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="47f47-125">If you use Visual Studio, you can use the integrated Git support.</span><span class="sxs-lookup"><span data-stu-id="47f47-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="47f47-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="47f47-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="47f47-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span><span class="sxs-lookup"><span data-stu-id="47f47-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="47f47-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="47f47-128">Mac/Linux</span></span>
<span data-ttu-id="47f47-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span><span class="sxs-lookup"><span data-stu-id="47f47-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-the-azure-portal"></a><span data-ttu-id="47f47-130">Web app creation on the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="47f47-130">Web app creation on the Azure Portal</span></span>
<span data-ttu-id="47f47-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="47f47-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="47f47-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span><span class="sxs-lookup"><span data-stu-id="47f47-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="47f47-133">In the search box, type "python".</span><span class="sxs-lookup"><span data-stu-id="47f47-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="47f47-134">In the search results, select **Bottle**, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="47f47-134">In the search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="47f47-135">Configure the new Bottle app, such as creating a new App Service plan and a new resource group for it.</span><span class="sxs-lookup"><span data-stu-id="47f47-135">Configure the new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="47f47-136">Then, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="47f47-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="47f47-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="47f47-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="47f47-138">Application Overview</span><span class="sxs-lookup"><span data-stu-id="47f47-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="47f47-139">Git repository contents</span><span class="sxs-lookup"><span data-stu-id="47f47-139">Git repository contents</span></span>
<span data-ttu-id="47f47-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span><span class="sxs-lookup"><span data-stu-id="47f47-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="47f47-141">Main sources for the application.</span><span class="sxs-lookup"><span data-stu-id="47f47-141">Main sources for the application.</span></span> <span data-ttu-id="47f47-142">Consists of 3 pages (index, about, contact) with a master layout.</span><span class="sxs-lookup"><span data-stu-id="47f47-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="47f47-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span><span class="sxs-lookup"><span data-stu-id="47f47-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="47f47-144">Local development server support.</span><span class="sxs-lookup"><span data-stu-id="47f47-144">Local development server support.</span></span> <span data-ttu-id="47f47-145">Use this to run the application locally.</span><span class="sxs-lookup"><span data-stu-id="47f47-145">Use this to run the application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="47f47-146">Project files for use with [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="47f47-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="47f47-147">IIS proxy for virtual environments and PTVS remote debugging support.</span><span class="sxs-lookup"><span data-stu-id="47f47-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="47f47-148">External packages needed by this application.</span><span class="sxs-lookup"><span data-stu-id="47f47-148">External packages needed by this application.</span></span> <span data-ttu-id="47f47-149">The deployment script will pip install the packages listed in this file.</span><span class="sxs-lookup"><span data-stu-id="47f47-149">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="47f47-150">IIS configuration files.</span><span class="sxs-lookup"><span data-stu-id="47f47-150">IIS configuration files.</span></span> <span data-ttu-id="47f47-151">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span><span class="sxs-lookup"><span data-stu-id="47f47-151">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="47f47-152">Optional files - Customizing deployment</span><span class="sxs-lookup"><span data-stu-id="47f47-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="47f47-153">Optional files - Python runtime</span><span class="sxs-lookup"><span data-stu-id="47f47-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="47f47-154">Additional files on server</span><span class="sxs-lookup"><span data-stu-id="47f47-154">Additional files on server</span></span>
<span data-ttu-id="47f47-155">Some files exist on the server but are not added to the git repository.</span><span class="sxs-lookup"><span data-stu-id="47f47-155">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="47f47-156">These are created by the deployment script.</span><span class="sxs-lookup"><span data-stu-id="47f47-156">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="47f47-157">IIS configuration file.</span><span class="sxs-lookup"><span data-stu-id="47f47-157">IIS configuration file.</span></span> <span data-ttu-id="47f47-158">Created from web.x.y.config on every deployment.</span><span class="sxs-lookup"><span data-stu-id="47f47-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="47f47-159">Python virtual environment.</span><span class="sxs-lookup"><span data-stu-id="47f47-159">Python virtual environment.</span></span> <span data-ttu-id="47f47-160">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span><span class="sxs-lookup"><span data-stu-id="47f47-160">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span>  <span data-ttu-id="47f47-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span><span class="sxs-lookup"><span data-stu-id="47f47-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="47f47-162">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span><span class="sxs-lookup"><span data-stu-id="47f47-162">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="47f47-163">Windows, with Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="47f47-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="47f47-164">Windows, with command line</span><span class="sxs-lookup"><span data-stu-id="47f47-164">Windows, with command line</span></span>
* <span data-ttu-id="47f47-165">Mac/Linux, with command line</span><span class="sxs-lookup"><span data-stu-id="47f47-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="47f47-166">Web App development - Windows - Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="47f47-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="47f47-167">Clone the repository</span><span class="sxs-lookup"><span data-stu-id="47f47-167">Clone the repository</span></span>
<span data-ttu-id="47f47-168">First, clone the repository using the url provided on the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="47f47-168">First, clone the repository using the url provided on the Azure Portal.</span></span> <span data-ttu-id="47f47-169">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="47f47-169">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="47f47-170">Open the solution file (.sln) that is included in the root of the repository.</span><span class="sxs-lookup"><span data-stu-id="47f47-170">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="47f47-171">Create virtual environment</span><span class="sxs-lookup"><span data-stu-id="47f47-171">Create virtual environment</span></span>
<span data-ttu-id="47f47-172">Now we'll create a virtual environment for local development.</span><span class="sxs-lookup"><span data-stu-id="47f47-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="47f47-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span><span class="sxs-lookup"><span data-stu-id="47f47-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="47f47-174">Make sure the name of the environment is `env`.</span><span class="sxs-lookup"><span data-stu-id="47f47-174">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="47f47-175">Select the base interpreter.</span><span class="sxs-lookup"><span data-stu-id="47f47-175">Select the base interpreter.</span></span> <span data-ttu-id="47f47-176">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="47f47-176">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="47f47-177">Make sure the option to download and install packages is checked.</span><span class="sxs-lookup"><span data-stu-id="47f47-177">Make sure the option to download and install packages is checked.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="47f47-178">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="47f47-178">Click **Create**.</span></span> <span data-ttu-id="47f47-179">This will create the virtual environment, and install dependencies listed in requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="47f47-179">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="47f47-180">Run using development server</span><span class="sxs-lookup"><span data-stu-id="47f47-180">Run using development server</span></span>
<span data-ttu-id="47f47-181">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span><span class="sxs-lookup"><span data-stu-id="47f47-181">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="47f47-182">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span><span class="sxs-lookup"><span data-stu-id="47f47-182">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="47f47-183">Make changes</span><span class="sxs-lookup"><span data-stu-id="47f47-183">Make changes</span></span>
<span data-ttu-id="47f47-184">Now you can experiment by making changes to the application sources and/or templates.</span><span class="sxs-lookup"><span data-stu-id="47f47-184">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="47f47-185">After you've tested your changes, commit them to the Git repository:</span><span class="sxs-lookup"><span data-stu-id="47f47-185">After you've tested your changes, commit them to the Git repository:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="47f47-186">Install more packages</span><span class="sxs-lookup"><span data-stu-id="47f47-186">Install more packages</span></span>
<span data-ttu-id="47f47-187">Your application may have dependencies beyond Python and Bottle.</span><span class="sxs-lookup"><span data-stu-id="47f47-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="47f47-188">You can install additional packages using pip.</span><span class="sxs-lookup"><span data-stu-id="47f47-188">You can install additional packages using pip.</span></span> <span data-ttu-id="47f47-189">To install a package, right-click on the virtual environment and select **Install Python Package**.</span><span class="sxs-lookup"><span data-stu-id="47f47-189">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="47f47-190">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span><span class="sxs-lookup"><span data-stu-id="47f47-190">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="47f47-191">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="47f47-191">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="47f47-192">Then, commit the changes to requirements.txt to the Git repository.</span><span class="sxs-lookup"><span data-stu-id="47f47-192">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="47f47-193">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="47f47-193">Deploy to Azure</span></span>
<span data-ttu-id="47f47-194">To trigger a deployment, click on **Sync** or **Push**.</span><span class="sxs-lookup"><span data-stu-id="47f47-194">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="47f47-195">Sync does both a push and a pull.</span><span class="sxs-lookup"><span data-stu-id="47f47-195">Sync does both a push and a pull.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="47f47-196">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span><span class="sxs-lookup"><span data-stu-id="47f47-196">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="47f47-197">Visual Studio doesn't show the progress of the deployment.</span><span class="sxs-lookup"><span data-stu-id="47f47-197">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="47f47-198">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="47f47-198">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="47f47-199">Browse to the Azure URL to view your changes.</span><span class="sxs-lookup"><span data-stu-id="47f47-199">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="47f47-200">Web app development - Windows - Command Line</span><span class="sxs-lookup"><span data-stu-id="47f47-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="47f47-201">Clone the repository</span><span class="sxs-lookup"><span data-stu-id="47f47-201">Clone the repository</span></span>
<span data-ttu-id="47f47-202">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span><span class="sxs-lookup"><span data-stu-id="47f47-202">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="47f47-203">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="47f47-203">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="47f47-204">Create virtual environment</span><span class="sxs-lookup"><span data-stu-id="47f47-204">Create virtual environment</span></span>
<span data-ttu-id="47f47-205">We'll create a new virtual environment for development purposes (do not add it to the repository).</span><span class="sxs-lookup"><span data-stu-id="47f47-205">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="47f47-206">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span><span class="sxs-lookup"><span data-stu-id="47f47-206">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="47f47-207">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade for your web app in the Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="47f47-207">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade for your web app in the Azure Portal)</span></span>

<span data-ttu-id="47f47-208">For Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="47f47-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="47f47-209">For Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="47f47-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="47f47-210">Install any external packages required by your application.</span><span class="sxs-lookup"><span data-stu-id="47f47-210">Install any external packages required by your application.</span></span> <span data-ttu-id="47f47-211">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span><span class="sxs-lookup"><span data-stu-id="47f47-211">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="47f47-212">Run using development server</span><span class="sxs-lookup"><span data-stu-id="47f47-212">Run using development server</span></span>
<span data-ttu-id="47f47-213">You can launch the application under a development server with the following command:</span><span class="sxs-lookup"><span data-stu-id="47f47-213">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="47f47-214">The console will display the URL and port the server listens to:</span><span class="sxs-lookup"><span data-stu-id="47f47-214">The console will display the URL and port the server listens to:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="47f47-215">Then, open your web browser to that URL.</span><span class="sxs-lookup"><span data-stu-id="47f47-215">Then, open your web browser to that URL.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="47f47-216">Make changes</span><span class="sxs-lookup"><span data-stu-id="47f47-216">Make changes</span></span>
<span data-ttu-id="47f47-217">Now you can experiment by making changes to the application sources and/or templates.</span><span class="sxs-lookup"><span data-stu-id="47f47-217">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="47f47-218">After you've tested your changes, commit them to the Git repository:</span><span class="sxs-lookup"><span data-stu-id="47f47-218">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="47f47-219">Install more packages</span><span class="sxs-lookup"><span data-stu-id="47f47-219">Install more packages</span></span>
<span data-ttu-id="47f47-220">Your application may have dependencies beyond Python and Bottle.</span><span class="sxs-lookup"><span data-stu-id="47f47-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="47f47-221">You can install additional packages using pip.</span><span class="sxs-lookup"><span data-stu-id="47f47-221">You can install additional packages using pip.</span></span> <span data-ttu-id="47f47-222">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span><span class="sxs-lookup"><span data-stu-id="47f47-222">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="47f47-223">Make sure to update requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="47f47-223">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="47f47-224">Commit the changes:</span><span class="sxs-lookup"><span data-stu-id="47f47-224">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="47f47-225">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="47f47-225">Deploy to Azure</span></span>
<span data-ttu-id="47f47-226">To trigger a deployment, push the changes to Azure:</span><span class="sxs-lookup"><span data-stu-id="47f47-226">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="47f47-227">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span><span class="sxs-lookup"><span data-stu-id="47f47-227">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="47f47-228">Browse to the Azure URL to view your changes.</span><span class="sxs-lookup"><span data-stu-id="47f47-228">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="47f47-229">Web app development - Mac/Linux - command line</span><span class="sxs-lookup"><span data-stu-id="47f47-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="47f47-230">Clone the repository</span><span class="sxs-lookup"><span data-stu-id="47f47-230">Clone the repository</span></span>
<span data-ttu-id="47f47-231">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span><span class="sxs-lookup"><span data-stu-id="47f47-231">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="47f47-232">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="47f47-232">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="47f47-233">Create virtual environment</span><span class="sxs-lookup"><span data-stu-id="47f47-233">Create virtual environment</span></span>
<span data-ttu-id="47f47-234">We'll create a new virtual environment for development purposes (do not add it to the repository).</span><span class="sxs-lookup"><span data-stu-id="47f47-234">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="47f47-235">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span><span class="sxs-lookup"><span data-stu-id="47f47-235">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="47f47-236">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="47f47-236">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="47f47-237">For Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="47f47-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="47f47-238">For Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="47f47-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="47f47-239">or pyvenv env</span><span class="sxs-lookup"><span data-stu-id="47f47-239">or pyvenv env</span></span>

<span data-ttu-id="47f47-240">Install any external packages required by your application.</span><span class="sxs-lookup"><span data-stu-id="47f47-240">Install any external packages required by your application.</span></span> <span data-ttu-id="47f47-241">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span><span class="sxs-lookup"><span data-stu-id="47f47-241">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="47f47-242">Run using development server</span><span class="sxs-lookup"><span data-stu-id="47f47-242">Run using development server</span></span>
<span data-ttu-id="47f47-243">You can launch the application under a development server with the following command:</span><span class="sxs-lookup"><span data-stu-id="47f47-243">You can launch the application under a development server with the following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="47f47-244">The console will display the URL and port the server listens to:</span><span class="sxs-lookup"><span data-stu-id="47f47-244">The console will display the URL and port the server listens to:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="47f47-245">Then, open your web browser to that URL.</span><span class="sxs-lookup"><span data-stu-id="47f47-245">Then, open your web browser to that URL.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="47f47-246">Make changes</span><span class="sxs-lookup"><span data-stu-id="47f47-246">Make changes</span></span>
<span data-ttu-id="47f47-247">Now you can experiment by making changes to the application sources and/or templates.</span><span class="sxs-lookup"><span data-stu-id="47f47-247">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="47f47-248">After you've tested your changes, commit them to the Git repository:</span><span class="sxs-lookup"><span data-stu-id="47f47-248">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="47f47-249">Install more packages</span><span class="sxs-lookup"><span data-stu-id="47f47-249">Install more packages</span></span>
<span data-ttu-id="47f47-250">Your application may have dependencies beyond Python and Bottle.</span><span class="sxs-lookup"><span data-stu-id="47f47-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="47f47-251">You can install additional packages using pip.</span><span class="sxs-lookup"><span data-stu-id="47f47-251">You can install additional packages using pip.</span></span> <span data-ttu-id="47f47-252">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span><span class="sxs-lookup"><span data-stu-id="47f47-252">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="47f47-253">Make sure to update requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="47f47-253">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="47f47-254">Commit the changes:</span><span class="sxs-lookup"><span data-stu-id="47f47-254">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="47f47-255">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="47f47-255">Deploy to Azure</span></span>
<span data-ttu-id="47f47-256">To trigger a deployment, push the changes to Azure:</span><span class="sxs-lookup"><span data-stu-id="47f47-256">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="47f47-257">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span><span class="sxs-lookup"><span data-stu-id="47f47-257">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="47f47-258">Browse to the Azure URL to view your changes.</span><span class="sxs-lookup"><span data-stu-id="47f47-258">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="47f47-259">Troubleshooting - Package Installation</span><span class="sxs-lookup"><span data-stu-id="47f47-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="47f47-260">Troubleshooting - Virtual Environment</span><span class="sxs-lookup"><span data-stu-id="47f47-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="47f47-261">Next Steps</span><span class="sxs-lookup"><span data-stu-id="47f47-261">Next Steps</span></span>
<span data-ttu-id="47f47-262">Follow these links to learn more about Bottle and Python Tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="47f47-262">Follow these links to learn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="47f47-263">[Bottle Documentation]</span><span class="sxs-lookup"><span data-stu-id="47f47-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="47f47-264">[Python Tools for Visual Studio Documentation]</span><span class="sxs-lookup"><span data-stu-id="47f47-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="47f47-265">For information on using Azure Table Storage and MongoDB:</span><span class="sxs-lookup"><span data-stu-id="47f47-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="47f47-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="47f47-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="47f47-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="47f47-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="47f47-268">What's changed</span><span class="sxs-lookup"><span data-stu-id="47f47-268">What's changed</span></span>
* <span data-ttu-id="47f47-269">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="47f47-269">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Bottle and MongoDB on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md
[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md

<!--External Link references-->
[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git for Windows]: http://msysgit.github.io/
[GitHub for Windows]: https://windows.github.com/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs 
[Bottle Documentation]: http://bottlepy.org/docs/dev/index.html











