---
title: Django and MySQL on Azure with Python Tools 2.2 for Visual Studio
description: Learn how to use the Python Tools for Visual Studio to create a Django web app that stores data in a MySQL database instance and deploy it to Azure App Service Web Apps.
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: ''
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: get-started-article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 5ad1e9dfc0c72b6f14bd06a8f3a79e6b9b69d821
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662498"
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="91277-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="91277-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="91277-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) to create a simple polls web app using one of the PTVS sample templates.</span><span class="sxs-lookup"><span data-stu-id="91277-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="91277-105">You'll learn how to use a MySQL service hosted on Azure, how to configure the web app to use MySQL, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="91277-105">You'll learn how to use a MySQL service hosted on Azure, how to configure the web app to use MySQL, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="91277-106">The information contained in this tutorial is also available in the following video:</span><span class="sxs-lookup"><span data-stu-id="91277-106">The information contained in this tutorial is also available in the following video:</span></span>
> 
> <span data-ttu-id="91277-107">[PTVS 2.1: Django app with MySQL][video]</span><span class="sxs-lookup"><span data-stu-id="91277-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="91277-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span><span class="sxs-lookup"><span data-stu-id="91277-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="91277-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="91277-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91277-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="91277-110">Prerequisites</span></span>
* <span data-ttu-id="91277-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="91277-111">Visual Studio 2015</span></span>
* <span data-ttu-id="91277-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span><span class="sxs-lookup"><span data-stu-id="91277-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="91277-113">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="91277-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="91277-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="91277-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="91277-115">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="91277-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="91277-116">Django 1.9 or later</span><span class="sxs-lookup"><span data-stu-id="91277-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of the the previous include. -->

> [!NOTE]
> <span data-ttu-id="91277-117">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="91277-117">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="91277-118">No credit card is required, and no commitments are necessary.</span><span class="sxs-lookup"><span data-stu-id="91277-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="91277-119">Create the Project</span><span class="sxs-lookup"><span data-stu-id="91277-119">Create the Project</span></span>
<span data-ttu-id="91277-120">In this section, you'll create a Visual Studio project using a sample template.</span><span class="sxs-lookup"><span data-stu-id="91277-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="91277-121">You'll create a virtual environment and install required packages.</span><span class="sxs-lookup"><span data-stu-id="91277-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="91277-122">You'll create a local database using sqlite.</span><span class="sxs-lookup"><span data-stu-id="91277-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="91277-123">Then you'll run the application locally.</span><span class="sxs-lookup"><span data-stu-id="91277-123">Then you'll run the application locally.</span></span>

1. <span data-ttu-id="91277-124">In Visual Studio, select **File**, **New Project**.</span><span class="sxs-lookup"><span data-stu-id="91277-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="91277-125">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span><span class="sxs-lookup"><span data-stu-id="91277-125">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="91277-126">Select **Polls Django Web Project** and click OK to create the project.</span><span class="sxs-lookup"><span data-stu-id="91277-126">Select **Polls Django Web Project** and click OK to create the project.</span></span>
   
    ![New Project Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="91277-128">You will be prompted to install external packages.</span><span class="sxs-lookup"><span data-stu-id="91277-128">You will be prompted to install external packages.</span></span> <span data-ttu-id="91277-129">Select **Install into a virtual environment**.</span><span class="sxs-lookup"><span data-stu-id="91277-129">Select **Install into a virtual environment**.</span></span>
   
    ![External Packages Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="91277-131">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span><span class="sxs-lookup"><span data-stu-id="91277-131">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
    ![Add Virtual Environment Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="91277-133">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span><span class="sxs-lookup"><span data-stu-id="91277-133">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="91277-134">Then select **Django Create Superuser**.</span><span class="sxs-lookup"><span data-stu-id="91277-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="91277-135">This will open a Django Management Console and create a sqlite database in the project folder.</span><span class="sxs-lookup"><span data-stu-id="91277-135">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="91277-136">Follow the prompts to create a user.</span><span class="sxs-lookup"><span data-stu-id="91277-136">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="91277-137">Confirm that the application works by pressing `F5`.</span><span class="sxs-lookup"><span data-stu-id="91277-137">Confirm that the application works by pressing `F5`.</span></span>
8. <span data-ttu-id="91277-138">Click **Log in** from the navigation bar at the top.</span><span class="sxs-lookup"><span data-stu-id="91277-138">Click **Log in** from the navigation bar at the top.</span></span>
   
    ![Django Navigation Bar](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="91277-140">Enter the credentials for the user you created when you synchronized the database.</span><span class="sxs-lookup"><span data-stu-id="91277-140">Enter the credentials for the user you created when you synchronized the database.</span></span>
   
    ![Log In Form](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="91277-142">Click **Create Sample Polls**.</span><span class="sxs-lookup"><span data-stu-id="91277-142">Click **Create Sample Polls**.</span></span>
    
     ![Create Sample Polls](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="91277-144">Click on a poll and vote.</span><span class="sxs-lookup"><span data-stu-id="91277-144">Click on a poll and vote.</span></span>
    
     ![Voting in Sample Polls](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="91277-146">Create a MySQL Database</span><span class="sxs-lookup"><span data-stu-id="91277-146">Create a MySQL Database</span></span>
<span data-ttu-id="91277-147">For the database, you'll create a ClearDB MySQL hosted database on Azure.</span><span class="sxs-lookup"><span data-stu-id="91277-147">For the database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="91277-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span><span class="sxs-lookup"><span data-stu-id="91277-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="91277-149">You can create a database with a free plan by following these steps.</span><span class="sxs-lookup"><span data-stu-id="91277-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="91277-150">Log in to the [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="91277-150">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="91277-151">At the Top of the navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span><span class="sxs-lookup"><span data-stu-id="91277-151">At the Top of the navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="91277-152">Configure the new MySQL database by creating a new resource group and select the appropriate location for it.</span><span class="sxs-lookup"><span data-stu-id="91277-152">Configure the new MySQL database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="91277-153">Once the MySQL database is created, click **Properties** in the database blade.</span><span class="sxs-lookup"><span data-stu-id="91277-153">Once the MySQL database is created, click **Properties** in the database blade.</span></span>
5. <span data-ttu-id="91277-154">Use the copy button to put the value of **CONNECTION STRING** on the clipboard.</span><span class="sxs-lookup"><span data-stu-id="91277-154">Use the copy button to put the value of **CONNECTION STRING** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="91277-155">Configure the Project</span><span class="sxs-lookup"><span data-stu-id="91277-155">Configure the Project</span></span>
<span data-ttu-id="91277-156">In this section, you'll configure our web app to use the MySQL database you just created.</span><span class="sxs-lookup"><span data-stu-id="91277-156">In this section, you'll configure our web app to use the MySQL database you just created.</span></span> <span data-ttu-id="91277-157">You'll also install additional Python packages required to use MySQL databases with Django.</span><span class="sxs-lookup"><span data-stu-id="91277-157">You'll also install additional Python packages required to use MySQL databases with Django.</span></span> <span data-ttu-id="91277-158">Then you'll run the web app locally.</span><span class="sxs-lookup"><span data-stu-id="91277-158">Then you'll run the web app locally.</span></span>

1. <span data-ttu-id="91277-159">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span><span class="sxs-lookup"><span data-stu-id="91277-159">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="91277-160">Temporarily paste the connection string in the editor.</span><span class="sxs-lookup"><span data-stu-id="91277-160">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="91277-161">The connection string is in this format:</span><span class="sxs-lookup"><span data-stu-id="91277-161">The connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="91277-162">Change the default database **ENGINE** to use MySQL, and set the values for **NAME**, **USER**, **PASSWORD** and **HOST** from the **CONNECTIONSTRING**.</span><span class="sxs-lookup"><span data-stu-id="91277-162">Change the default database **ENGINE** to use MySQL, and set the values for **NAME**, **USER**, **PASSWORD** and **HOST** from the **CONNECTIONSTRING**.</span></span>
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. <span data-ttu-id="91277-163">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span><span class="sxs-lookup"><span data-stu-id="91277-163">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="91277-164">Install the package `mysqlclient` using **pip**.</span><span class="sxs-lookup"><span data-stu-id="91277-164">Install the package `mysqlclient` using **pip**.</span></span>
   
    ![Install Package Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="91277-166">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span><span class="sxs-lookup"><span data-stu-id="91277-166">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="91277-167">Then select **Django Create Superuser**.</span><span class="sxs-lookup"><span data-stu-id="91277-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="91277-168">This will create the tables for the MySQL database you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="91277-168">This will create the tables for the MySQL database you created in the previous section.</span></span> <span data-ttu-id="91277-169">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section of this article.</span><span class="sxs-lookup"><span data-stu-id="91277-169">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section of this article.</span></span>
5. <span data-ttu-id="91277-170">Run the application with `F5`.</span><span class="sxs-lookup"><span data-stu-id="91277-170">Run the application with `F5`.</span></span> <span data-ttu-id="91277-171">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="91277-171">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the MySQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="91277-172">Publish the web app to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="91277-172">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="91277-173">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="91277-173">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="91277-174">In **Solution Explorer**, right-click on the project node and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="91277-174">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
    ![Publish Web Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="91277-176">Click on **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="91277-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="91277-177">Click on **New** to create a new web app.</span><span class="sxs-lookup"><span data-stu-id="91277-177">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="91277-178">Fill in the following fields and click **Create**:</span><span class="sxs-lookup"><span data-stu-id="91277-178">Fill in the following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="91277-179">**Web App name**</span><span class="sxs-lookup"><span data-stu-id="91277-179">**Web App name**</span></span>
   * <span data-ttu-id="91277-180">**App Service plan**</span><span class="sxs-lookup"><span data-stu-id="91277-180">**App Service plan**</span></span>
   * <span data-ttu-id="91277-181">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="91277-181">**Resource group**</span></span>
   * <span data-ttu-id="91277-182">**Region**</span><span class="sxs-lookup"><span data-stu-id="91277-182">**Region**</span></span>
   * <span data-ttu-id="91277-183">Leave **Database server** set to **No database**</span><span class="sxs-lookup"><span data-stu-id="91277-183">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="91277-184">Accept all other defaults and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="91277-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="91277-185">Your web browser will open automatically to the published web app.</span><span class="sxs-lookup"><span data-stu-id="91277-185">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="91277-186">You should see the web app working as expected, using the **MySQL** database hosted on Azure.</span><span class="sxs-lookup"><span data-stu-id="91277-186">You should see the web app working as expected, using the **MySQL** database hosted on Azure.</span></span>
   
    ![Web Browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="91277-188">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="91277-188">Congratulations!</span></span> <span data-ttu-id="91277-189">You have successfully published your MySQL-based web app to Azure.</span><span class="sxs-lookup"><span data-stu-id="91277-189">You have successfully published your MySQL-based web app to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91277-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="91277-190">Next steps</span></span>
<span data-ttu-id="91277-191">Follow these links to learn more about Python Tools for Visual Studio, Django and MySQL.</span><span class="sxs-lookup"><span data-stu-id="91277-191">Follow these links to learn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="91277-192">[Python Tools for Visual Studio Documentation]</span><span class="sxs-lookup"><span data-stu-id="91277-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="91277-193">[Web Projects]</span><span class="sxs-lookup"><span data-stu-id="91277-193">[Web Projects]</span></span>
  * <span data-ttu-id="91277-194">[Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="91277-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="91277-195">[Remote Debugging on Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="91277-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="91277-196">[Django Documentation]</span><span class="sxs-lookup"><span data-stu-id="91277-196">[Django Documentation]</span></span>
* <span data-ttu-id="91277-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="91277-197">[MySQL]</span></span>

<span data-ttu-id="91277-198">For more information, see the [Python Developer Center](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="91277-198">For more information, see the [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Python Developer Center]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure Portal]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517191
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Remote Debugging on Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web Projects]: http://go.microsoft.com/fwlink/?LinkId=624027
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django Documentation]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo










