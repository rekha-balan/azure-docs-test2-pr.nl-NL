---
title: Creating web apps with Django in Azure
description: A tutorial that introduces you to running a Python web app in Azure App Service Web Apps.
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: ''
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 482d6d7569f32cfca96e2b66e45d7fbbcd01e154
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553530"
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="b3cab-103">Creating web apps with Django in Azure</span><span class="sxs-lookup"><span data-stu-id="b3cab-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="b3cab-104">This tutorial describes how to get started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b3cab-104">This tutorial describes how to get started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="b3cab-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span><span class="sxs-lookup"><span data-stu-id="b3cab-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="b3cab-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span><span class="sxs-lookup"><span data-stu-id="b3cab-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="b3cab-107">You will create an application using the Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="b3cab-107">You will create an application using the Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="b3cab-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span><span class="sxs-lookup"><span data-stu-id="b3cab-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="b3cab-109">Then you will run the application locally, make changes, commit and push them to Azure.</span><span class="sxs-lookup"><span data-stu-id="b3cab-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span> <span data-ttu-id="b3cab-110">The tutorial shows how to do this from Windows or Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="b3cab-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="b3cab-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="b3cab-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b3cab-112">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="b3cab-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b3cab-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b3cab-113">Prerequisites</span></span>
* <span data-ttu-id="b3cab-114">Windows, Mac or Linux</span><span class="sxs-lookup"><span data-stu-id="b3cab-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="b3cab-115">Python 2.7 or 3.4</span><span class="sxs-lookup"><span data-stu-id="b3cab-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="b3cab-116">setuptools, pip, virtualenv (Python 2.7 only)</span><span class="sxs-lookup"><span data-stu-id="b3cab-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="b3cab-117">Git</span><span class="sxs-lookup"><span data-stu-id="b3cab-117">Git</span></span>
* <span data-ttu-id="b3cab-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span><span class="sxs-lookup"><span data-stu-id="b3cab-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="b3cab-119">**Note**: TFS publishing is currently not supported for Python projects.</span><span class="sxs-lookup"><span data-stu-id="b3cab-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="b3cab-120">Windows</span><span class="sxs-lookup"><span data-stu-id="b3cab-120">Windows</span></span>
<span data-ttu-id="b3cab-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="b3cab-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="b3cab-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span><span class="sxs-lookup"><span data-stu-id="b3cab-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="b3cab-123">Alternatively, you can get Python from [python.org].</span><span class="sxs-lookup"><span data-stu-id="b3cab-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="b3cab-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span><span class="sxs-lookup"><span data-stu-id="b3cab-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="b3cab-125">If you use Visual Studio, you can use the integrated Git support.</span><span class="sxs-lookup"><span data-stu-id="b3cab-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="b3cab-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="b3cab-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="b3cab-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span><span class="sxs-lookup"><span data-stu-id="b3cab-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="b3cab-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="b3cab-128">Mac/Linux</span></span>
<span data-ttu-id="b3cab-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span><span class="sxs-lookup"><span data-stu-id="b3cab-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="b3cab-130">Web App Creation on Portal</span><span class="sxs-lookup"><span data-stu-id="b3cab-130">Web App Creation on Portal</span></span>
<span data-ttu-id="b3cab-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b3cab-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="b3cab-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span><span class="sxs-lookup"><span data-stu-id="b3cab-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span>
2. <span data-ttu-id="b3cab-133">In the search box, type "python".</span><span class="sxs-lookup"><span data-stu-id="b3cab-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="b3cab-134">In the search results, select **Django** (published by PTVS), then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b3cab-134">In the search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="b3cab-135">Configure the new Django app, such as creating a new App Service plan and a new resource group for it.</span><span class="sxs-lookup"><span data-stu-id="b3cab-135">Configure the new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="b3cab-136">Then, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b3cab-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="b3cab-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="b3cab-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="b3cab-138">Application Overview</span><span class="sxs-lookup"><span data-stu-id="b3cab-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="b3cab-139">Git repository contents</span><span class="sxs-lookup"><span data-stu-id="b3cab-139">Git repository contents</span></span>
<span data-ttu-id="b3cab-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span><span class="sxs-lookup"><span data-stu-id="b3cab-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

<span data-ttu-id="b3cab-141">Main sources for the application.</span><span class="sxs-lookup"><span data-stu-id="b3cab-141">Main sources for the application.</span></span> <span data-ttu-id="b3cab-142">Consists of 3 pages (index, about, contact) with a master layout.</span><span class="sxs-lookup"><span data-stu-id="b3cab-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="b3cab-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span><span class="sxs-lookup"><span data-stu-id="b3cab-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="b3cab-144">Local management and development server support.</span><span class="sxs-lookup"><span data-stu-id="b3cab-144">Local management and development server support.</span></span> <span data-ttu-id="b3cab-145">Use this to run the application locally, synchronize the database, etc.</span><span class="sxs-lookup"><span data-stu-id="b3cab-145">Use this to run the application locally, synchronize the database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="b3cab-146">Default database.</span><span class="sxs-lookup"><span data-stu-id="b3cab-146">Default database.</span></span> <span data-ttu-id="b3cab-147">Includes the necessary tables for the application to run, but does not contain any users (synchronize the database to create a user).</span><span class="sxs-lookup"><span data-stu-id="b3cab-147">Includes the necessary tables for the application to run, but does not contain any users (synchronize the database to create a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="b3cab-148">Project files for use with [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="b3cab-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="b3cab-149">IIS proxy for virtual environments and PTVS remote debugging support.</span><span class="sxs-lookup"><span data-stu-id="b3cab-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="b3cab-150">External packages needed by this application.</span><span class="sxs-lookup"><span data-stu-id="b3cab-150">External packages needed by this application.</span></span> <span data-ttu-id="b3cab-151">The deployment script will pip install the packages listed in this file.</span><span class="sxs-lookup"><span data-stu-id="b3cab-151">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="b3cab-152">IIS configuration files.</span><span class="sxs-lookup"><span data-stu-id="b3cab-152">IIS configuration files.</span></span> <span data-ttu-id="b3cab-153">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span><span class="sxs-lookup"><span data-stu-id="b3cab-153">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="b3cab-154">Optional files - Customizing deployment</span><span class="sxs-lookup"><span data-stu-id="b3cab-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="b3cab-155">Optional files - Python runtime</span><span class="sxs-lookup"><span data-stu-id="b3cab-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="b3cab-156">Additional files on server</span><span class="sxs-lookup"><span data-stu-id="b3cab-156">Additional files on server</span></span>
<span data-ttu-id="b3cab-157">Some files exist on the server but are not added to the git repository.</span><span class="sxs-lookup"><span data-stu-id="b3cab-157">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="b3cab-158">These are created by the deployment script.</span><span class="sxs-lookup"><span data-stu-id="b3cab-158">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="b3cab-159">IIS configuration file.</span><span class="sxs-lookup"><span data-stu-id="b3cab-159">IIS configuration file.</span></span> <span data-ttu-id="b3cab-160">Created from web.x.y.config on every deployment.</span><span class="sxs-lookup"><span data-stu-id="b3cab-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="b3cab-161">Python virtual environment.</span><span class="sxs-lookup"><span data-stu-id="b3cab-161">Python virtual environment.</span></span> <span data-ttu-id="b3cab-162">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span><span class="sxs-lookup"><span data-stu-id="b3cab-162">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span> <span data-ttu-id="b3cab-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span><span class="sxs-lookup"><span data-stu-id="b3cab-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="b3cab-164">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span><span class="sxs-lookup"><span data-stu-id="b3cab-164">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="b3cab-165">Windows, with Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b3cab-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="b3cab-166">Windows, with command line</span><span class="sxs-lookup"><span data-stu-id="b3cab-166">Windows, with command line</span></span>
* <span data-ttu-id="b3cab-167">Mac/Linux, with command line</span><span class="sxs-lookup"><span data-stu-id="b3cab-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="b3cab-168">Web app development - Windows - Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b3cab-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="b3cab-169">Clone the repository</span><span class="sxs-lookup"><span data-stu-id="b3cab-169">Clone the repository</span></span>
<span data-ttu-id="b3cab-170">First, clone the repository using the URL provided on the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b3cab-170">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="b3cab-171">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="b3cab-171">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="b3cab-172">Open the solution file (.sln) that is included in the root of the repository.</span><span class="sxs-lookup"><span data-stu-id="b3cab-172">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="b3cab-173">Create virtual environment</span><span class="sxs-lookup"><span data-stu-id="b3cab-173">Create virtual environment</span></span>
<span data-ttu-id="b3cab-174">Now we'll create a virtual environment for local development.</span><span class="sxs-lookup"><span data-stu-id="b3cab-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="b3cab-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span><span class="sxs-lookup"><span data-stu-id="b3cab-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="b3cab-176">Make sure the name of the environment is `env`.</span><span class="sxs-lookup"><span data-stu-id="b3cab-176">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="b3cab-177">Select the base interpreter.</span><span class="sxs-lookup"><span data-stu-id="b3cab-177">Select the base interpreter.</span></span> <span data-ttu-id="b3cab-178">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="b3cab-178">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="b3cab-179">Make sure the option to download and install packages is checked.</span><span class="sxs-lookup"><span data-stu-id="b3cab-179">Make sure the option to download and install packages is checked.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="b3cab-180">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b3cab-180">Click **Create**.</span></span> <span data-ttu-id="b3cab-181">This will create the virtual environment, and install dependencies listed in requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="b3cab-181">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="b3cab-182">Create a superuser</span><span class="sxs-lookup"><span data-stu-id="b3cab-182">Create a superuser</span></span>
<span data-ttu-id="b3cab-183">The database included with the application does not have any superuser defined.</span><span class="sxs-lookup"><span data-stu-id="b3cab-183">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="b3cab-184">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span><span class="sxs-lookup"><span data-stu-id="b3cab-184">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="b3cab-185">Run this from the command-line from your project folder:</span><span class="sxs-lookup"><span data-stu-id="b3cab-185">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="b3cab-186">Follow the prompts to set the user name, password, etc.</span><span class="sxs-lookup"><span data-stu-id="b3cab-186">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="b3cab-187">Run using development server</span><span class="sxs-lookup"><span data-stu-id="b3cab-187">Run using development server</span></span>
<span data-ttu-id="b3cab-188">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span><span class="sxs-lookup"><span data-stu-id="b3cab-188">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="b3cab-189">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span><span class="sxs-lookup"><span data-stu-id="b3cab-189">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="b3cab-190">Make changes</span><span class="sxs-lookup"><span data-stu-id="b3cab-190">Make changes</span></span>
<span data-ttu-id="b3cab-191">Now you can experiment by making changes to the application sources and/or templates.</span><span class="sxs-lookup"><span data-stu-id="b3cab-191">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="b3cab-192">After you've tested your changes, commit them to the Git repository:</span><span class="sxs-lookup"><span data-stu-id="b3cab-192">After you've tested your changes, commit them to the Git repository:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="b3cab-193">Install more packages</span><span class="sxs-lookup"><span data-stu-id="b3cab-193">Install more packages</span></span>
<span data-ttu-id="b3cab-194">Your application may have dependencies beyond Python and Django.</span><span class="sxs-lookup"><span data-stu-id="b3cab-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="b3cab-195">You can install additional packages using pip.</span><span class="sxs-lookup"><span data-stu-id="b3cab-195">You can install additional packages using pip.</span></span> <span data-ttu-id="b3cab-196">To install a package, right-click on the virtual environment and select **Install Python Package**.</span><span class="sxs-lookup"><span data-stu-id="b3cab-196">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="b3cab-197">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span><span class="sxs-lookup"><span data-stu-id="b3cab-197">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="b3cab-198">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="b3cab-198">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="b3cab-199">Then, commit the changes to requirements.txt to the Git repository.</span><span class="sxs-lookup"><span data-stu-id="b3cab-199">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="b3cab-200">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="b3cab-200">Deploy to Azure</span></span>
<span data-ttu-id="b3cab-201">To trigger a deployment, click on **Sync** or **Push**.</span><span class="sxs-lookup"><span data-stu-id="b3cab-201">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="b3cab-202">Sync does both a push and a pull.</span><span class="sxs-lookup"><span data-stu-id="b3cab-202">Sync does both a push and a pull.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="b3cab-203">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span><span class="sxs-lookup"><span data-stu-id="b3cab-203">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="b3cab-204">Visual Studio doesn't show the progress of the deployment.</span><span class="sxs-lookup"><span data-stu-id="b3cab-204">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="b3cab-205">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="b3cab-205">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="b3cab-206">Browse to the Azure URL to view your changes.</span><span class="sxs-lookup"><span data-stu-id="b3cab-206">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="b3cab-207">Web app development - Windows - command line</span><span class="sxs-lookup"><span data-stu-id="b3cab-207">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="b3cab-208">Clone the repository</span><span class="sxs-lookup"><span data-stu-id="b3cab-208">Clone the repository</span></span>
<span data-ttu-id="b3cab-209">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span><span class="sxs-lookup"><span data-stu-id="b3cab-209">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="b3cab-210">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="b3cab-210">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="b3cab-211">Create virtual environment</span><span class="sxs-lookup"><span data-stu-id="b3cab-211">Create virtual environment</span></span>
<span data-ttu-id="b3cab-212">We'll create a new virtual environment for development purposes (do not add it to the repository).</span><span class="sxs-lookup"><span data-stu-id="b3cab-212">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="b3cab-213">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span><span class="sxs-lookup"><span data-stu-id="b3cab-213">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="b3cab-214">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="b3cab-214">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="b3cab-215">For Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="b3cab-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="b3cab-216">For Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="b3cab-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="b3cab-217">Install any external packages required by your application.</span><span class="sxs-lookup"><span data-stu-id="b3cab-217">Install any external packages required by your application.</span></span> <span data-ttu-id="b3cab-218">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span><span class="sxs-lookup"><span data-stu-id="b3cab-218">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="b3cab-219">Create a superuser</span><span class="sxs-lookup"><span data-stu-id="b3cab-219">Create a superuser</span></span>
<span data-ttu-id="b3cab-220">The database included with the application does not have any superuser defined.</span><span class="sxs-lookup"><span data-stu-id="b3cab-220">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="b3cab-221">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span><span class="sxs-lookup"><span data-stu-id="b3cab-221">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="b3cab-222">Run this from the command-line from your project folder:</span><span class="sxs-lookup"><span data-stu-id="b3cab-222">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="b3cab-223">Follow the prompts to set the user name, password, etc.</span><span class="sxs-lookup"><span data-stu-id="b3cab-223">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="b3cab-224">Run using development server</span><span class="sxs-lookup"><span data-stu-id="b3cab-224">Run using development server</span></span>
<span data-ttu-id="b3cab-225">You can launch the application under a development server with the following command:</span><span class="sxs-lookup"><span data-stu-id="b3cab-225">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="b3cab-226">The console will display the URL and port the server listens to:</span><span class="sxs-lookup"><span data-stu-id="b3cab-226">The console will display the URL and port the server listens to:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="b3cab-227">Then, open your web browser to that URL.</span><span class="sxs-lookup"><span data-stu-id="b3cab-227">Then, open your web browser to that URL.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="b3cab-228">Make changes</span><span class="sxs-lookup"><span data-stu-id="b3cab-228">Make changes</span></span>
<span data-ttu-id="b3cab-229">Now you can experiment by making changes to the application sources and/or templates.</span><span class="sxs-lookup"><span data-stu-id="b3cab-229">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="b3cab-230">After you've tested your changes, commit them to the Git repository:</span><span class="sxs-lookup"><span data-stu-id="b3cab-230">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="b3cab-231">Install more packages</span><span class="sxs-lookup"><span data-stu-id="b3cab-231">Install more packages</span></span>
<span data-ttu-id="b3cab-232">Your application may have dependencies beyond Python and Django.</span><span class="sxs-lookup"><span data-stu-id="b3cab-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="b3cab-233">You can install additional packages using pip.</span><span class="sxs-lookup"><span data-stu-id="b3cab-233">You can install additional packages using pip.</span></span> <span data-ttu-id="b3cab-234">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span><span class="sxs-lookup"><span data-stu-id="b3cab-234">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="b3cab-235">Make sure to update requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="b3cab-235">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="b3cab-236">Commit the changes:</span><span class="sxs-lookup"><span data-stu-id="b3cab-236">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="b3cab-237">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="b3cab-237">Deploy to Azure</span></span>
<span data-ttu-id="b3cab-238">To trigger a deployment, push the changes to Azure:</span><span class="sxs-lookup"><span data-stu-id="b3cab-238">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="b3cab-239">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span><span class="sxs-lookup"><span data-stu-id="b3cab-239">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="b3cab-240">Browse to the Azure URL to view your changes.</span><span class="sxs-lookup"><span data-stu-id="b3cab-240">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="b3cab-241">Web app development - Mac/Linux - command line</span><span class="sxs-lookup"><span data-stu-id="b3cab-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="b3cab-242">Clone the repository</span><span class="sxs-lookup"><span data-stu-id="b3cab-242">Clone the repository</span></span>
<span data-ttu-id="b3cab-243">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span><span class="sxs-lookup"><span data-stu-id="b3cab-243">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="b3cab-244">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="b3cab-244">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="b3cab-245">Create virtual environment</span><span class="sxs-lookup"><span data-stu-id="b3cab-245">Create virtual environment</span></span>
<span data-ttu-id="b3cab-246">We'll create a new virtual environment for development purposes (do not add it to the repository).</span><span class="sxs-lookup"><span data-stu-id="b3cab-246">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="b3cab-247">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span><span class="sxs-lookup"><span data-stu-id="b3cab-247">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="b3cab-248">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="b3cab-248">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="b3cab-249">For Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="b3cab-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="b3cab-250">For Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="b3cab-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="b3cab-251">or</span><span class="sxs-lookup"><span data-stu-id="b3cab-251">or</span></span>

    pyvenv env

<span data-ttu-id="b3cab-252">Install any external packages required by your application.</span><span class="sxs-lookup"><span data-stu-id="b3cab-252">Install any external packages required by your application.</span></span> <span data-ttu-id="b3cab-253">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span><span class="sxs-lookup"><span data-stu-id="b3cab-253">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="b3cab-254">Create a superuser</span><span class="sxs-lookup"><span data-stu-id="b3cab-254">Create a superuser</span></span>
<span data-ttu-id="b3cab-255">The database included with the application does not have any superuser defined.</span><span class="sxs-lookup"><span data-stu-id="b3cab-255">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="b3cab-256">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span><span class="sxs-lookup"><span data-stu-id="b3cab-256">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="b3cab-257">Run this from the command-line from your project folder:</span><span class="sxs-lookup"><span data-stu-id="b3cab-257">Run this from the command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="b3cab-258">Follow the prompts to set the user name, password, etc.</span><span class="sxs-lookup"><span data-stu-id="b3cab-258">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="b3cab-259">Run using development server</span><span class="sxs-lookup"><span data-stu-id="b3cab-259">Run using development server</span></span>
<span data-ttu-id="b3cab-260">You can launch the application under a development server with the following command:</span><span class="sxs-lookup"><span data-stu-id="b3cab-260">You can launch the application under a development server with the following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="b3cab-261">The console will display the URL and port the server listens to:</span><span class="sxs-lookup"><span data-stu-id="b3cab-261">The console will display the URL and port the server listens to:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="b3cab-262">Then, open your web browser to that URL.</span><span class="sxs-lookup"><span data-stu-id="b3cab-262">Then, open your web browser to that URL.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="b3cab-263">Make changes</span><span class="sxs-lookup"><span data-stu-id="b3cab-263">Make changes</span></span>
<span data-ttu-id="b3cab-264">Now you can experiment by making changes to the application sources and/or templates.</span><span class="sxs-lookup"><span data-stu-id="b3cab-264">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="b3cab-265">After you've tested your changes, commit them to the Git repository:</span><span class="sxs-lookup"><span data-stu-id="b3cab-265">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="b3cab-266">Install more packages</span><span class="sxs-lookup"><span data-stu-id="b3cab-266">Install more packages</span></span>
<span data-ttu-id="b3cab-267">Your application may have dependencies beyond Python and Django.</span><span class="sxs-lookup"><span data-stu-id="b3cab-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="b3cab-268">You can install additional packages using pip.</span><span class="sxs-lookup"><span data-stu-id="b3cab-268">You can install additional packages using pip.</span></span> <span data-ttu-id="b3cab-269">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span><span class="sxs-lookup"><span data-stu-id="b3cab-269">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="b3cab-270">Make sure to update requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="b3cab-270">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="b3cab-271">Commit the changes:</span><span class="sxs-lookup"><span data-stu-id="b3cab-271">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="b3cab-272">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="b3cab-272">Deploy to Azure</span></span>
<span data-ttu-id="b3cab-273">To trigger a deployment, push the changes to Azure:</span><span class="sxs-lookup"><span data-stu-id="b3cab-273">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="b3cab-274">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span><span class="sxs-lookup"><span data-stu-id="b3cab-274">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="b3cab-275">Browse to the Azure URL to view your changes.</span><span class="sxs-lookup"><span data-stu-id="b3cab-275">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="b3cab-276">Troubleshooting - Package Installation</span><span class="sxs-lookup"><span data-stu-id="b3cab-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="b3cab-277">Troubleshooting - Virtual Environment</span><span class="sxs-lookup"><span data-stu-id="b3cab-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="b3cab-278">Troubleshooting - Static Files</span><span class="sxs-lookup"><span data-stu-id="b3cab-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="b3cab-279">Django has the concept of collecting static files.</span><span class="sxs-lookup"><span data-stu-id="b3cab-279">Django has the concept of collecting static files.</span></span> <span data-ttu-id="b3cab-280">This takes all the static files from their original location and copies them to a single folder.</span><span class="sxs-lookup"><span data-stu-id="b3cab-280">This takes all the static files from their original location and copies them to a single folder.</span></span> <span data-ttu-id="b3cab-281">For this application, they are copied to `/static`.</span><span class="sxs-lookup"><span data-stu-id="b3cab-281">For this application, they are copied to `/static`.</span></span>

<span data-ttu-id="b3cab-282">This is done because static files may come from different Django 'apps'.</span><span class="sxs-lookup"><span data-stu-id="b3cab-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="b3cab-283">For example, the static files from the Django admin interfaces are located in a Django library subfolder in the virtual environment.</span><span class="sxs-lookup"><span data-stu-id="b3cab-283">For example, the static files from the Django admin interfaces are located in a Django library subfolder in the virtual environment.</span></span> <span data-ttu-id="b3cab-284">Static files defined by this application are located in `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="b3cab-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="b3cab-285">As you use more Django 'apps', you'll have static files located in multiple places.</span><span class="sxs-lookup"><span data-stu-id="b3cab-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="b3cab-286">When running the application in debug mode, the application serves the static files from their original location.</span><span class="sxs-lookup"><span data-stu-id="b3cab-286">When running the application in debug mode, the application serves the static files from their original location.</span></span>

<span data-ttu-id="b3cab-287">When running the application in release mode, the application does **not** serve the static files.</span><span class="sxs-lookup"><span data-stu-id="b3cab-287">When running the application in release mode, the application does **not** serve the static files.</span></span> <span data-ttu-id="b3cab-288">It is the responsibility of the web server to serve the files.</span><span class="sxs-lookup"><span data-stu-id="b3cab-288">It is the responsibility of the web server to serve the files.</span></span> <span data-ttu-id="b3cab-289">For this application, IIS will serve the static files from `/static`.</span><span class="sxs-lookup"><span data-stu-id="b3cab-289">For this application, IIS will serve the static files from `/static`.</span></span>

<span data-ttu-id="b3cab-290">The collection of static files is done automatically as part of the deployment script, clearing previously collected files.</span><span class="sxs-lookup"><span data-stu-id="b3cab-290">The collection of static files is done automatically as part of the deployment script, clearing previously collected files.</span></span> <span data-ttu-id="b3cab-291">This means the collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span><span class="sxs-lookup"><span data-stu-id="b3cab-291">This means the collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="b3cab-292">If you want to skip collection of static files for your Django application:</span><span class="sxs-lookup"><span data-stu-id="b3cab-292">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="b3cab-293">Then you'll need to do the collection manually on your local machine:</span><span class="sxs-lookup"><span data-stu-id="b3cab-293">Then you'll need to do the collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="b3cab-294">Then remove the `\static` folder from `.gitignore` and add it to the Git repository.</span><span class="sxs-lookup"><span data-stu-id="b3cab-294">Then remove the `\static` folder from `.gitignore` and add it to the Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="b3cab-295">Troubleshooting - Settings</span><span class="sxs-lookup"><span data-stu-id="b3cab-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="b3cab-296">Various settings for the application can be changed in `DjangoWebProject/settings.py`.</span><span class="sxs-lookup"><span data-stu-id="b3cab-296">Various settings for the application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="b3cab-297">For developer convenience, debug mode is enabled.</span><span class="sxs-lookup"><span data-stu-id="b3cab-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="b3cab-298">One nice side effect of that is you'll be able to see images and other static content when running locally, without having to collect static files.</span><span class="sxs-lookup"><span data-stu-id="b3cab-298">One nice side effect of that is you'll be able to see images and other static content when running locally, without having to collect static files.</span></span>

<span data-ttu-id="b3cab-299">To disable debug mode:</span><span class="sxs-lookup"><span data-stu-id="b3cab-299">To disable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="b3cab-300">When debug is disabled, the value for `ALLOWED_HOSTS` needs to be updated to include the Azure host name.</span><span class="sxs-lookup"><span data-stu-id="b3cab-300">When debug is disabled, the value for `ALLOWED_HOSTS` needs to be updated to include the Azure host name.</span></span> <span data-ttu-id="b3cab-301">For example:</span><span class="sxs-lookup"><span data-stu-id="b3cab-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="b3cab-302">or to enable any:</span><span class="sxs-lookup"><span data-stu-id="b3cab-302">or to enable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="b3cab-303">In practice, you may want to do something more complex to deal with switching between debug and release mode, and getting the host name.</span><span class="sxs-lookup"><span data-stu-id="b3cab-303">In practice, you may want to do something more complex to deal with switching between debug and release mode, and getting the host name.</span></span>

<span data-ttu-id="b3cab-304">You can set environment variables through the Azure portal **CONFIGURE** page, in the **app settings** section.</span><span class="sxs-lookup"><span data-stu-id="b3cab-304">You can set environment variables through the Azure portal **CONFIGURE** page, in the **app settings** section.</span></span>  <span data-ttu-id="b3cab-305">This can be useful for setting values that you may not want to appear in the sources (connection strings, passwords, etc), or that you want to set differently between Azure and your local machine.</span><span class="sxs-lookup"><span data-stu-id="b3cab-305">This can be useful for setting values that you may not want to appear in the sources (connection strings, passwords, etc), or that you want to set differently between Azure and your local machine.</span></span> <span data-ttu-id="b3cab-306">In `settings.py`, you can query the environment variables using `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="b3cab-306">In `settings.py`, you can query the environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="b3cab-307">Using a Database</span><span class="sxs-lookup"><span data-stu-id="b3cab-307">Using a Database</span></span>
<span data-ttu-id="b3cab-308">The database that is included with the application is a sqlite database.</span><span class="sxs-lookup"><span data-stu-id="b3cab-308">The database that is included with the application is a sqlite database.</span></span> <span data-ttu-id="b3cab-309">This is a convenient and useful default database to use for development, as it requires almost no setup.</span><span class="sxs-lookup"><span data-stu-id="b3cab-309">This is a convenient and useful default database to use for development, as it requires almost no setup.</span></span> <span data-ttu-id="b3cab-310">The database is stored in the db.sqlite3 file in the project folder.</span><span class="sxs-lookup"><span data-stu-id="b3cab-310">The database is stored in the db.sqlite3 file in the project folder.</span></span>

<span data-ttu-id="b3cab-311">Azure provides database services which are easy to use from a Django application.</span><span class="sxs-lookup"><span data-stu-id="b3cab-311">Azure provides database services which are easy to use from a Django application.</span></span> <span data-ttu-id="b3cab-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show the steps necessary to create the database service, change the database settings in `DjangoWebProject/settings.py`, and the libraries required to install.</span><span class="sxs-lookup"><span data-stu-id="b3cab-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show the steps necessary to create the database service, change the database settings in `DjangoWebProject/settings.py`, and the libraries required to install.</span></span>

<span data-ttu-id="b3cab-313">Of course, if you prefer to manage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span><span class="sxs-lookup"><span data-stu-id="b3cab-313">Of course, if you prefer to manage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="b3cab-314">Django Admin Interface</span><span class="sxs-lookup"><span data-stu-id="b3cab-314">Django Admin Interface</span></span>
<span data-ttu-id="b3cab-315">Once you start building your models, you'll want to populate the database with some data.</span><span class="sxs-lookup"><span data-stu-id="b3cab-315">Once you start building your models, you'll want to populate the database with some data.</span></span> <span data-ttu-id="b3cab-316">An easy way to do add and edit content interactively is to use the Django administration interface.</span><span class="sxs-lookup"><span data-stu-id="b3cab-316">An easy way to do add and edit content interactively is to use the Django administration interface.</span></span>

<span data-ttu-id="b3cab-317">The code for the admin interface is commented out in the application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span><span class="sxs-lookup"><span data-stu-id="b3cab-317">The code for the admin interface is commented out in the application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="b3cab-318">After it's enabled, synchronize the database, run the application and navigate to `/admin`.</span><span class="sxs-lookup"><span data-stu-id="b3cab-318">After it's enabled, synchronize the database, run the application and navigate to `/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3cab-319">Next Steps</span><span class="sxs-lookup"><span data-stu-id="b3cab-319">Next Steps</span></span>
<span data-ttu-id="b3cab-320">Follow these links to learn more about Django and Python Tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="b3cab-320">Follow these links to learn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="b3cab-321">[Django Documentation]</span><span class="sxs-lookup"><span data-stu-id="b3cab-321">[Django Documentation]</span></span>
* <span data-ttu-id="b3cab-322">[Python Tools for Visual Studio Documentation]</span><span class="sxs-lookup"><span data-stu-id="b3cab-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="b3cab-323">For information on using SQL Database and MySQL:</span><span class="sxs-lookup"><span data-stu-id="b3cab-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="b3cab-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="b3cab-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="b3cab-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="b3cab-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="b3cab-326">For more information, see the [Python Developer Center](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="b3cab-326">For more information, see the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="b3cab-327">What's changed</span><span class="sxs-lookup"><span data-stu-id="b3cab-327">What's changed</span></span>
* <span data-ttu-id="b3cab-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b3cab-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Django and MySQL on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Django and SQL Database on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-django-sql.md
[SQL Database]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

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
[Django Documentation]: https://www.djangoproject.com/










