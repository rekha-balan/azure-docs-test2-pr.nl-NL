---
title: Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio
description: Learn how to use the Python Tools for Visual Studio to create a Django web app that stores data in a SQL database instance and deploy it to Azure App Service Web Apps.
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: ''
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: d87b5004f1823361aa8260d9ad8c4caaa694415e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660682"
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="217b0-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="217b0-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="217b0-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span><span class="sxs-lookup"><span data-stu-id="217b0-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="217b0-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="217b0-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="217b0-106">We'll learn how to use a SQL database hosted on Azure, how to configure the web app to use a SQL database, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="217b0-106">We'll learn how to use a SQL database hosted on Azure, how to configure the web app to use a SQL database, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="217b0-107">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span><span class="sxs-lookup"><span data-stu-id="217b0-107">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="217b0-108">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="217b0-108">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="217b0-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="217b0-109">Prerequisites</span></span>
* <span data-ttu-id="217b0-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="217b0-110">Visual Studio 2015</span></span>
* <span data-ttu-id="217b0-111">[Python 2.7 32-bit]</span><span class="sxs-lookup"><span data-stu-id="217b0-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="217b0-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="217b0-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="217b0-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="217b0-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="217b0-114">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="217b0-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="217b0-115">Django 1.9 or later</span><span class="sxs-lookup"><span data-stu-id="217b0-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="217b0-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="217b0-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="217b0-117">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="217b0-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-the-project"></a><span data-ttu-id="217b0-118">Create the Project</span><span class="sxs-lookup"><span data-stu-id="217b0-118">Create the Project</span></span>
<span data-ttu-id="217b0-119">In this section, we'll create a Visual Studio project using a sample template.</span><span class="sxs-lookup"><span data-stu-id="217b0-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="217b0-120">We'll create a virtual environment and install required packages.</span><span class="sxs-lookup"><span data-stu-id="217b0-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="217b0-121">We'll create a local database using sqlite.</span><span class="sxs-lookup"><span data-stu-id="217b0-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="217b0-122">Then we'll run the web app locally.</span><span class="sxs-lookup"><span data-stu-id="217b0-122">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="217b0-123">In Visual Studio, select **File**, **New Project**.</span><span class="sxs-lookup"><span data-stu-id="217b0-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="217b0-124">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span><span class="sxs-lookup"><span data-stu-id="217b0-124">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="217b0-125">Select **Polls Django Web Project** and click OK to create the project.</span><span class="sxs-lookup"><span data-stu-id="217b0-125">Select **Polls Django Web Project** and click OK to create the project.</span></span>

     ![New Project Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="217b0-127">You will be prompted to install external packages.</span><span class="sxs-lookup"><span data-stu-id="217b0-127">You will be prompted to install external packages.</span></span> <span data-ttu-id="217b0-128">Select **Install into a virtual environment**.</span><span class="sxs-lookup"><span data-stu-id="217b0-128">Select **Install into a virtual environment**.</span></span>

     ![External Packages Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="217b0-130">Select **Python 2.7** as the base interpreter.</span><span class="sxs-lookup"><span data-stu-id="217b0-130">Select **Python 2.7** as the base interpreter.</span></span>

     ![Add Virtual Environment Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="217b0-132">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span><span class="sxs-lookup"><span data-stu-id="217b0-132">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="217b0-133">Then select **Django Create Superuser**.</span><span class="sxs-lookup"><span data-stu-id="217b0-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="217b0-134">This will open a Django Management Console and create a sqlite database in the project folder.</span><span class="sxs-lookup"><span data-stu-id="217b0-134">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="217b0-135">Follow the prompts to create a user.</span><span class="sxs-lookup"><span data-stu-id="217b0-135">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="217b0-136">Confirm that the application works by pressing <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="217b0-136">Confirm that the application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="217b0-137">Click **Log in** from the navigation bar at the top.</span><span class="sxs-lookup"><span data-stu-id="217b0-137">Click **Log in** from the navigation bar at the top.</span></span>

     ![Web Browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="217b0-139">Enter the credentials for the user you created when you synchronized the database.</span><span class="sxs-lookup"><span data-stu-id="217b0-139">Enter the credentials for the user you created when you synchronized the database.</span></span>

     ![Web Browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="217b0-141">Click **Create Sample Polls**.</span><span class="sxs-lookup"><span data-stu-id="217b0-141">Click **Create Sample Polls**.</span></span>

      ![Web Browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="217b0-143">Click on a poll and vote.</span><span class="sxs-lookup"><span data-stu-id="217b0-143">Click on a poll and vote.</span></span>

      ![Web Browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="217b0-145">Create a SQL Database</span><span class="sxs-lookup"><span data-stu-id="217b0-145">Create a SQL Database</span></span>
<span data-ttu-id="217b0-146">For the database, we'll create an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="217b0-146">For the database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="217b0-147">You can create a database by following these steps.</span><span class="sxs-lookup"><span data-stu-id="217b0-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="217b0-148">Log into the [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="217b0-148">Log into the [Azure Portal].</span></span>
2. <span data-ttu-id="217b0-149">At the bottom of the navigation pane, click **NEW**.</span><span class="sxs-lookup"><span data-stu-id="217b0-149">At the bottom of the navigation pane, click **NEW**.</span></span> <span data-ttu-id="217b0-150">, click **Data + Storage** > **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="217b0-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="217b0-151">Configure the new SQL Database by creating a new resource group and select the appropriate location for it.</span><span class="sxs-lookup"><span data-stu-id="217b0-151">Configure the new SQL Database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="217b0-152">Once the SQL Database is created, click **Open in Visual Studio** in the database blade.</span><span class="sxs-lookup"><span data-stu-id="217b0-152">Once the SQL Database is created, click **Open in Visual Studio** in the database blade.</span></span>
5. <span data-ttu-id="217b0-153">Click **Configure your firewall**.</span><span class="sxs-lookup"><span data-stu-id="217b0-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="217b0-154">In the **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set to the public IP address of your development machine.</span><span class="sxs-lookup"><span data-stu-id="217b0-154">In the **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set to the public IP address of your development machine.</span></span> <span data-ttu-id="217b0-155">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="217b0-155">Click **Save**.</span></span>

   <span data-ttu-id="217b0-156">This will allow connections to the database server from your development machine.</span><span class="sxs-lookup"><span data-stu-id="217b0-156">This will allow connections to the database server from your development machine.</span></span>
7. <span data-ttu-id="217b0-157">Back in the database blade, click **Properties**, then click **Show database connection strings**.</span><span class="sxs-lookup"><span data-stu-id="217b0-157">Back in the database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="217b0-158">Use the copy button to put the value of **ADO.NET** on the clipboard.</span><span class="sxs-lookup"><span data-stu-id="217b0-158">Use the copy button to put the value of **ADO.NET** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="217b0-159">Configure the Project</span><span class="sxs-lookup"><span data-stu-id="217b0-159">Configure the Project</span></span>
<span data-ttu-id="217b0-160">In this section, we'll configure our web app to use the SQL database we just created.</span><span class="sxs-lookup"><span data-stu-id="217b0-160">In this section, we'll configure our web app to use the SQL database we just created.</span></span> <span data-ttu-id="217b0-161">We'll also install additional Python packages required to use SQL databases with Django.</span><span class="sxs-lookup"><span data-stu-id="217b0-161">We'll also install additional Python packages required to use SQL databases with Django.</span></span> <span data-ttu-id="217b0-162">Then we'll run the web app locally.</span><span class="sxs-lookup"><span data-stu-id="217b0-162">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="217b0-163">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span><span class="sxs-lookup"><span data-stu-id="217b0-163">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="217b0-164">Temporarily paste the connection string in the editor.</span><span class="sxs-lookup"><span data-stu-id="217b0-164">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="217b0-165">The connection string is in this format:</span><span class="sxs-lookup"><span data-stu-id="217b0-165">The connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="217b0-166">Edit the definition of `DATABASES` to use the values above.</span><span class="sxs-lookup"><span data-stu-id="217b0-166">Edit the definition of `DATABASES` to use the values above.</span></span>

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. <span data-ttu-id="217b0-167">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span><span class="sxs-lookup"><span data-stu-id="217b0-167">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="217b0-168">Install the package `pyodbc` using **pip**.</span><span class="sxs-lookup"><span data-stu-id="217b0-168">Install the package `pyodbc` using **pip**.</span></span>

     ![Install Python Package Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="217b0-170">Install the package `django-pyodbc-azure` using **pip**.</span><span class="sxs-lookup"><span data-stu-id="217b0-170">Install the package `django-pyodbc-azure` using **pip**.</span></span>

     ![Install Python Package Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="217b0-172">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span><span class="sxs-lookup"><span data-stu-id="217b0-172">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="217b0-173">Then select **Django Create Superuser**.</span><span class="sxs-lookup"><span data-stu-id="217b0-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="217b0-174">This will create the tables for the SQL database we created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="217b0-174">This will create the tables for the SQL database we created in the previous section.</span></span> <span data-ttu-id="217b0-175">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section.</span><span class="sxs-lookup"><span data-stu-id="217b0-175">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section.</span></span>
5. <span data-ttu-id="217b0-176">Run the application with `F5`.</span><span class="sxs-lookup"><span data-stu-id="217b0-176">Run the application with `F5`.</span></span> <span data-ttu-id="217b0-177">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the SQL database.</span><span class="sxs-lookup"><span data-stu-id="217b0-177">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the SQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="217b0-178">Publish the web app to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="217b0-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="217b0-179">The Azure .NET SDK provides an easy way to deploy your web web app to Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="217b0-179">The Azure .NET SDK provides an easy way to deploy your web web app to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="217b0-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="217b0-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>

     ![Publish Web Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="217b0-182">Click on **Microsoft Azure Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="217b0-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="217b0-183">Click on **New** to create a new web app.</span><span class="sxs-lookup"><span data-stu-id="217b0-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="217b0-184">Fill in the following fields and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="217b0-184">Fill in the following fields and click **Create**.</span></span>

   * <span data-ttu-id="217b0-185">**Web App name**</span><span class="sxs-lookup"><span data-stu-id="217b0-185">**Web App name**</span></span>
   * <span data-ttu-id="217b0-186">**App Service plan**</span><span class="sxs-lookup"><span data-stu-id="217b0-186">**App Service plan**</span></span>
   * <span data-ttu-id="217b0-187">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="217b0-187">**Resource group**</span></span>
   * <span data-ttu-id="217b0-188">**Region**</span><span class="sxs-lookup"><span data-stu-id="217b0-188">**Region**</span></span>
   * <span data-ttu-id="217b0-189">Leave **Database server** set to **No database**</span><span class="sxs-lookup"><span data-stu-id="217b0-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="217b0-190">Accept all other defaults and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="217b0-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="217b0-191">Your web browser will open automatically to the published web app.</span><span class="sxs-lookup"><span data-stu-id="217b0-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="217b0-192">You should see the web app working as expected, using the **SQL** database hosted on Azure.</span><span class="sxs-lookup"><span data-stu-id="217b0-192">You should see the web app working as expected, using the **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="217b0-193">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="217b0-193">Congratulations!</span></span>

     ![Web Browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="217b0-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="217b0-195">Next steps</span></span>
<span data-ttu-id="217b0-196">Follow these links to learn more about Python Tools for Visual Studio, Django and SQL Database.</span><span class="sxs-lookup"><span data-stu-id="217b0-196">Follow these links to learn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="217b0-197">[Python Tools for Visual Studio Documentation]</span><span class="sxs-lookup"><span data-stu-id="217b0-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="217b0-198">[Web Projects]</span><span class="sxs-lookup"><span data-stu-id="217b0-198">[Web Projects]</span></span>
  * <span data-ttu-id="217b0-199">[Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="217b0-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="217b0-200">[Remote Debugging on Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="217b0-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="217b0-201">[Django Documentation]</span><span class="sxs-lookup"><span data-stu-id="217b0-201">[Django Documentation]</span></span>
* <span data-ttu-id="217b0-202">[SQL Database]</span><span class="sxs-lookup"><span data-stu-id="217b0-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="217b0-203">What's changed</span><span class="sxs-lookup"><span data-stu-id="217b0-203">What's changed</span></span>
* <span data-ttu-id="217b0-204">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="217b0-204">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python Developer Center]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Remote Debugging on Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web Projects]: http://go.microsoft.com/fwlink/?LinkId=624027
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django Documentation]: https://www.djangoproject.com/
[SQL Database]: /documentation/services/sql-database/











