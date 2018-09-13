---
title: Creating web apps with Flask in Azure
description: A tutorial that introduces you to running a Python web app on Azure.
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: ''
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 8e5cdf59b97d21938cb198635aba56b909476989
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551645"
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="cdcf5-103">Creating web apps with Flask in Azure</span><span class="sxs-lookup"><span data-stu-id="cdcf5-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="cdcf5-104">This tutorial describes how to get started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-104">This tutorial describes how to get started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="cdcf5-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span><span class="sxs-lookup"><span data-stu-id="cdcf5-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="cdcf5-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="cdcf5-107">You will create an application using the Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-107">You will create an application using the Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="cdcf5-108">You will create the website from the Azure gallery, set up Git deployment, and clone the repository locally.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-108">You will create the website from the Azure gallery, set up Git deployment, and clone the repository locally.</span></span>  <span data-ttu-id="cdcf5-109">Then you will run the application locally, make changes, commit and push them to Azure.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span>  <span data-ttu-id="cdcf5-110">The tutorial shows how to do this from Windows or Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="cdcf5-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="cdcf5-112">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="cdcf5-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cdcf5-113">Prerequisites</span></span>
* <span data-ttu-id="cdcf5-114">Windows, Mac or Linux</span><span class="sxs-lookup"><span data-stu-id="cdcf5-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="cdcf5-115">Python 2.7 or 3.4</span><span class="sxs-lookup"><span data-stu-id="cdcf5-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="cdcf5-116">setuptools, pip, virtualenv (Python 2.7 only)</span><span class="sxs-lookup"><span data-stu-id="cdcf5-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="cdcf5-117">Git</span><span class="sxs-lookup"><span data-stu-id="cdcf5-117">Git</span></span>
* <span data-ttu-id="cdcf5-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span><span class="sxs-lookup"><span data-stu-id="cdcf5-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="cdcf5-119">**Note**: TFS publishing is currently not supported for Python projects.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="cdcf5-120">Windows</span><span class="sxs-lookup"><span data-stu-id="cdcf5-120">Windows</span></span>
<span data-ttu-id="cdcf5-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="cdcf5-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span>  <span data-ttu-id="cdcf5-123">Alternatively, you can get Python from [python.org].</span><span class="sxs-lookup"><span data-stu-id="cdcf5-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="cdcf5-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span><span class="sxs-lookup"><span data-stu-id="cdcf5-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="cdcf5-125">If you use Visual Studio, you can use the integrated Git support.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="cdcf5-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="cdcf5-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="cdcf5-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="cdcf5-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="cdcf5-128">Mac/Linux</span></span>
<span data-ttu-id="cdcf5-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-the-azure-portal"></a><span data-ttu-id="cdcf5-130">Web app create on the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cdcf5-130">Web app create on the Azure Portal</span></span>
<span data-ttu-id="cdcf5-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="cdcf5-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="cdcf5-133">Click **Web + Mobile**.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="cdcf5-134">In the search box, type "python".</span><span class="sxs-lookup"><span data-stu-id="cdcf5-134">In the search box, type "python".</span></span>
4. <span data-ttu-id="cdcf5-135">In the search results, select **Flask**, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-135">In the search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="cdcf5-136">Configure the new Flask app, such as creating a new App Service plan and a new resource group for it.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-136">Configure the new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="cdcf5-137">Then, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="cdcf5-138">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-138">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="cdcf5-139">Application Overview</span><span class="sxs-lookup"><span data-stu-id="cdcf5-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="cdcf5-140">Git repository contents</span><span class="sxs-lookup"><span data-stu-id="cdcf5-140">Git repository contents</span></span>
<span data-ttu-id="cdcf5-141">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-141">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="cdcf5-142">Main sources for the application.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-142">Main sources for the application.</span></span>  <span data-ttu-id="cdcf5-143">Consists of 3 pages (index, about, contact) with a master layout.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="cdcf5-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="cdcf5-145">Local development server support.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-145">Local development server support.</span></span> <span data-ttu-id="cdcf5-146">Use this to run the application locally.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-146">Use this to run the application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="cdcf5-147">Project files for use with [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="cdcf5-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="cdcf5-148">IIS proxy for virtual environments and PTVS remote debugging support.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="cdcf5-149">External packages needed by this application.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-149">External packages needed by this application.</span></span> <span data-ttu-id="cdcf5-150">The deployment script will pip install the packages listed in this file.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-150">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="cdcf5-151">IIS configuration files.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-151">IIS configuration files.</span></span>  <span data-ttu-id="cdcf5-152">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-152">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="cdcf5-153">Optional files - Customizing deployment</span><span class="sxs-lookup"><span data-stu-id="cdcf5-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="cdcf5-154">Optional files - Python runtime</span><span class="sxs-lookup"><span data-stu-id="cdcf5-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="cdcf5-155">Additional files on server</span><span class="sxs-lookup"><span data-stu-id="cdcf5-155">Additional files on server</span></span>
<span data-ttu-id="cdcf5-156">Some files exist on the server but are not added to the git repository.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-156">Some files exist on the server but are not added to the git repository.</span></span>  <span data-ttu-id="cdcf5-157">These are created by the deployment script.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-157">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="cdcf5-158">IIS configuration file.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-158">IIS configuration file.</span></span>  <span data-ttu-id="cdcf5-159">Created from web.x.y.config on every deployment.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="cdcf5-160">Python virtual environment.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-160">Python virtual environment.</span></span>  <span data-ttu-id="cdcf5-161">Created during deployment if a compatible virtual environment doesn't already exist on the app.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-161">Created during deployment if a compatible virtual environment doesn't already exist on the app.</span></span>  <span data-ttu-id="cdcf5-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="cdcf5-163">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-163">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="cdcf5-164">Windows, with Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cdcf5-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="cdcf5-165">Windows, with command line</span><span class="sxs-lookup"><span data-stu-id="cdcf5-165">Windows, with command line</span></span>
* <span data-ttu-id="cdcf5-166">Mac/Linux, with command line</span><span class="sxs-lookup"><span data-stu-id="cdcf5-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="cdcf5-167">Web app development - Windows - Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cdcf5-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="cdcf5-168">Clone the repository</span><span class="sxs-lookup"><span data-stu-id="cdcf5-168">Clone the repository</span></span>
<span data-ttu-id="cdcf5-169">First, clone the repository using the URL provided on the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-169">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="cdcf5-170">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-170">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="cdcf5-171">Open the solution file (.sln) that is included in the root of the repository.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-171">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="cdcf5-172">Create virtual environment</span><span class="sxs-lookup"><span data-stu-id="cdcf5-172">Create virtual environment</span></span>
<span data-ttu-id="cdcf5-173">Now we'll create a virtual environment for local development.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="cdcf5-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="cdcf5-175">Make sure the name of the environment is `env`.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-175">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="cdcf5-176">Select the base interpreter.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-176">Select the base interpreter.</span></span>  <span data-ttu-id="cdcf5-177">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-177">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="cdcf5-178">Make sure the option to download and install packages is checked.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-178">Make sure the option to download and install packages is checked.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="cdcf5-179">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-179">Click **Create**.</span></span>  <span data-ttu-id="cdcf5-180">This will create the virtual environment, and install dependencies listed in requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-180">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="cdcf5-181">Run using development server</span><span class="sxs-lookup"><span data-stu-id="cdcf5-181">Run using development server</span></span>
<span data-ttu-id="cdcf5-182">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-182">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="cdcf5-183">You can set breakpoints in the sources, use the watch windows, etc.  See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-183">You can set breakpoints in the sources, use the watch windows, etc.  See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="cdcf5-184">Make changes</span><span class="sxs-lookup"><span data-stu-id="cdcf5-184">Make changes</span></span>
<span data-ttu-id="cdcf5-185">Now you can experiment by making changes to the application sources and/or templates.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-185">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="cdcf5-186">After you've tested your changes, commit them to the Git repository:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-186">After you've tested your changes, commit them to the Git repository:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="cdcf5-187">Install more packages</span><span class="sxs-lookup"><span data-stu-id="cdcf5-187">Install more packages</span></span>
<span data-ttu-id="cdcf5-188">Your application may have dependencies beyond Python and Flask.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="cdcf5-189">You can install additional packages using pip.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="cdcf5-190">To install a package, right-click on the virtual environment and select **Install Python Package**.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-190">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="cdcf5-191">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-191">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="cdcf5-192">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-192">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="cdcf5-193">Then, commit the changes to requirements.txt to the Git repository.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-193">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="cdcf5-194">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="cdcf5-194">Deploy to Azure</span></span>
<span data-ttu-id="cdcf5-195">To trigger a deployment, click on **Sync** or **Push**.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-195">To trigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="cdcf5-196">Sync does both a push and a pull.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-196">Sync does both a push and a pull.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="cdcf5-197">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-197">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="cdcf5-198">Visual Studio doesn't show the progress of the deployment.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-198">Visual Studio doesn't show the progress of the deployment.</span></span>  <span data-ttu-id="cdcf5-199">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-199">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="cdcf5-200">Browse to the Azure URL to view your changes.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-200">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="cdcf5-201">Web app development - Windows - command line</span><span class="sxs-lookup"><span data-stu-id="cdcf5-201">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="cdcf5-202">Clone the repository</span><span class="sxs-lookup"><span data-stu-id="cdcf5-202">Clone the repository</span></span>
<span data-ttu-id="cdcf5-203">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-203">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="cdcf5-204">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-204">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="cdcf5-205">Create virtual environment</span><span class="sxs-lookup"><span data-stu-id="cdcf5-205">Create virtual environment</span></span>
<span data-ttu-id="cdcf5-206">We'll create a new virtual environment for development purposes (do not add it to the repository).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-206">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="cdcf5-207">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-207">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="cdcf5-208">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-208">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="cdcf5-209">For Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="cdcf5-210">For Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="cdcf5-211">Install any external packages required by your application.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-211">Install any external packages required by your application.</span></span> <span data-ttu-id="cdcf5-212">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-212">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="cdcf5-213">Run using development server</span><span class="sxs-lookup"><span data-stu-id="cdcf5-213">Run using development server</span></span>
<span data-ttu-id="cdcf5-214">You can launch the application under a development server with the following command:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-214">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="cdcf5-215">The console will display the URL and port the server listens to:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-215">The console will display the URL and port the server listens to:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="cdcf5-216">Then, open your web browser to that URL.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-216">Then, open your web browser to that URL.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="cdcf5-217">Make changes</span><span class="sxs-lookup"><span data-stu-id="cdcf5-217">Make changes</span></span>
<span data-ttu-id="cdcf5-218">Now you can experiment by making changes to the application sources and/or templates.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-218">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="cdcf5-219">After you've tested your changes, commit them to the Git repository:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-219">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="cdcf5-220">Install more packages</span><span class="sxs-lookup"><span data-stu-id="cdcf5-220">Install more packages</span></span>
<span data-ttu-id="cdcf5-221">Your application may have dependencies beyond Python and Flask.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="cdcf5-222">You can install additional packages using pip.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="cdcf5-223">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-223">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="cdcf5-224">Make sure to update requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-224">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="cdcf5-225">Commit the changes:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-225">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="cdcf5-226">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="cdcf5-226">Deploy to Azure</span></span>
<span data-ttu-id="cdcf5-227">To trigger a deployment, push the changes to Azure:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-227">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="cdcf5-228">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-228">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="cdcf5-229">Browse to the Azure URL to view your changes.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-229">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="cdcf5-230">Web app development - Mac/Linux - command line</span><span class="sxs-lookup"><span data-stu-id="cdcf5-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="cdcf5-231">Clone the repository</span><span class="sxs-lookup"><span data-stu-id="cdcf5-231">Clone the repository</span></span>
<span data-ttu-id="cdcf5-232">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-232">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="cdcf5-233">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-233">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="cdcf5-234">Create virtual environment</span><span class="sxs-lookup"><span data-stu-id="cdcf5-234">Create virtual environment</span></span>
<span data-ttu-id="cdcf5-235">We'll create a new virtual environment for development purposes (do not add it to the repository).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-235">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="cdcf5-236">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-236">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="cdcf5-237">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-237">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="cdcf5-238">For Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="cdcf5-239">For Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="cdcf5-240">or pyvenv env</span><span class="sxs-lookup"><span data-stu-id="cdcf5-240">or pyvenv env</span></span>

<span data-ttu-id="cdcf5-241">Install any external packages required by your application.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-241">Install any external packages required by your application.</span></span> <span data-ttu-id="cdcf5-242">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-242">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="cdcf5-243">Run using development server</span><span class="sxs-lookup"><span data-stu-id="cdcf5-243">Run using development server</span></span>
<span data-ttu-id="cdcf5-244">You can launch the application under a development server with the following command:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-244">You can launch the application under a development server with the following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="cdcf5-245">The console will display the URL and port the server listens to:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-245">The console will display the URL and port the server listens to:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="cdcf5-246">Then, open your web browser to that URL.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-246">Then, open your web browser to that URL.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="cdcf5-247">Make changes</span><span class="sxs-lookup"><span data-stu-id="cdcf5-247">Make changes</span></span>
<span data-ttu-id="cdcf5-248">Now you can experiment by making changes to the application sources and/or templates.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-248">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="cdcf5-249">After you've tested your changes, commit them to the Git repository:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-249">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="cdcf5-250">Install more packages</span><span class="sxs-lookup"><span data-stu-id="cdcf5-250">Install more packages</span></span>
<span data-ttu-id="cdcf5-251">Your application may have dependencies beyond Python and Flask.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="cdcf5-252">You can install additional packages using pip.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="cdcf5-253">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-253">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="cdcf5-254">Make sure to update requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-254">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="cdcf5-255">Commit the changes:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-255">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="cdcf5-256">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="cdcf5-256">Deploy to Azure</span></span>
<span data-ttu-id="cdcf5-257">To trigger a deployment, push the changes to Azure:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-257">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="cdcf5-258">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-258">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="cdcf5-259">Browse to the Azure URL to view your changes.</span><span class="sxs-lookup"><span data-stu-id="cdcf5-259">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="cdcf5-260">Troubleshooting - Package Installation</span><span class="sxs-lookup"><span data-stu-id="cdcf5-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="cdcf5-261">Troubleshooting - Virtual Environment</span><span class="sxs-lookup"><span data-stu-id="cdcf5-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="cdcf5-262">Next Steps</span><span class="sxs-lookup"><span data-stu-id="cdcf5-262">Next Steps</span></span>
<span data-ttu-id="cdcf5-263">Follow these links to learn more about Flask and Python Tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-263">Follow these links to learn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="cdcf5-264">[Flask Documentation]</span><span class="sxs-lookup"><span data-stu-id="cdcf5-264">[Flask Documentation]</span></span>
* <span data-ttu-id="cdcf5-265">[Python Tools for Visual Studio Documentation]</span><span class="sxs-lookup"><span data-stu-id="cdcf5-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="cdcf5-266">For information on using Azure Table Storage and MongoDB:</span><span class="sxs-lookup"><span data-stu-id="cdcf5-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="cdcf5-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="cdcf5-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="cdcf5-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="cdcf5-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="cdcf5-269">For more information, see also the [Python Developer Center](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="cdcf5-269">For more information, see also the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="cdcf5-270">What's changed</span><span class="sxs-lookup"><span data-stu-id="cdcf5-270">What's changed</span></span>
* <span data-ttu-id="cdcf5-271">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="cdcf5-271">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Flask and MongoDB on Azure with Python Tools for Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-flask-table-storage.md

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
[Flask Documentation]: http://flask.pocoo.org/ 











