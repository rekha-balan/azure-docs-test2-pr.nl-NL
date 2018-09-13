---
title: Flask and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio
description: Learn how to use the Python Tools for Visual Studio to create a Flask web app that stores data in Azure Table Storage and deploy it to Azure App Service Web Apps.
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: ''
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 2b01b0698fbba0694344760c323343b2be04f5ab
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670175"
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="540c4-103">Flask and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="540c4-103">Flask and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="540c4-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span><span class="sxs-lookup"><span data-stu-id="540c4-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="540c4-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span><span class="sxs-lookup"><span data-stu-id="540c4-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span></span>

<span data-ttu-id="540c4-106">The polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="540c4-106">The polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="540c4-107">We'll learn how to create an Azure Storage account, how to configure the web app to use Azure Table Storage, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="540c4-107">We'll learn how to create an Azure Storage account, how to configure the web app to use Azure Table Storage, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="540c4-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span><span class="sxs-lookup"><span data-stu-id="540c4-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="540c4-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="540c4-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="540c4-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="540c4-110">Prerequisites</span></span>
* <span data-ttu-id="540c4-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="540c4-111">Visual Studio 2015</span></span>
* <span data-ttu-id="540c4-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="540c4-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="540c4-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="540c4-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="540c4-114">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="540c4-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="540c4-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span><span class="sxs-lookup"><span data-stu-id="540c4-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="540c4-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="540c4-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="540c4-117">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="540c4-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="540c4-118">Create the Project</span><span class="sxs-lookup"><span data-stu-id="540c4-118">Create the Project</span></span>
<span data-ttu-id="540c4-119">In this section, we'll create a Visual Studio project using a sample template.</span><span class="sxs-lookup"><span data-stu-id="540c4-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="540c4-120">We'll create a virtual environment and install required packages.</span><span class="sxs-lookup"><span data-stu-id="540c4-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="540c4-121">Then we'll run the application locally using the default in-memory repository.</span><span class="sxs-lookup"><span data-stu-id="540c4-121">Then we'll run the application locally using the default in-memory repository.</span></span>

1. <span data-ttu-id="540c4-122">In Visual Studio, select **File**, **New Project**.</span><span class="sxs-lookup"><span data-stu-id="540c4-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="540c4-123">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span><span class="sxs-lookup"><span data-stu-id="540c4-123">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="540c4-124">Select **Polls Flask Web Project** and click OK to create the project.</span><span class="sxs-lookup"><span data-stu-id="540c4-124">Select **Polls Flask Web Project** and click OK to create the project.</span></span>
   
     ![New Project Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. <span data-ttu-id="540c4-126">You will be prompted to install external packages.</span><span class="sxs-lookup"><span data-stu-id="540c4-126">You will be prompted to install external packages.</span></span> <span data-ttu-id="540c4-127">Select **Install into a virtual environment**.</span><span class="sxs-lookup"><span data-stu-id="540c4-127">Select **Install into a virtual environment**.</span></span>
   
     ![External Packages Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. <span data-ttu-id="540c4-129">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span><span class="sxs-lookup"><span data-stu-id="540c4-129">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
     ![Add Virtual Environment Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="540c4-131">Confirm that the application works by pressing `F5`.</span><span class="sxs-lookup"><span data-stu-id="540c4-131">Confirm that the application works by pressing `F5`.</span></span> <span data-ttu-id="540c4-132">By default, the application uses an in-memory repository which doesn't require any configuration.</span><span class="sxs-lookup"><span data-stu-id="540c4-132">By default, the application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="540c4-133">All data is lost when the web server is stopped.</span><span class="sxs-lookup"><span data-stu-id="540c4-133">All data is lost when the web server is stopped.</span></span>
6. <span data-ttu-id="540c4-134">Click **Create Sample Polls**, then click on a poll and vote.</span><span class="sxs-lookup"><span data-stu-id="540c4-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Web Browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="540c4-136">Create an Azure Storage Account</span><span class="sxs-lookup"><span data-stu-id="540c4-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="540c4-137">To use storage operations, you need an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="540c4-137">To use storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="540c4-138">You can create a storage account by following these steps.</span><span class="sxs-lookup"><span data-stu-id="540c4-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="540c4-139">Log into the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="540c4-139">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="540c4-140">Click the **New** icon on the top left of the Portal, then click **Data + Storage** > **Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="540c4-140">Click the **New** icon on the top left of the Portal, then click **Data + Storage** > **Storage Account**.</span></span> <span data-ttu-id="540c4-141">Click on **Create**, then give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span><span class="sxs-lookup"><span data-stu-id="540c4-141">Click on **Create**, then give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Quick Create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="540c4-143">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span><span class="sxs-lookup"><span data-stu-id="540c4-143">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="540c4-144">Click the **Access Keys** part in the storage account's blade.</span><span class="sxs-lookup"><span data-stu-id="540c4-144">Click the **Access Keys** part in the storage account's blade.</span></span> <span data-ttu-id="540c4-145">Take note of the account name and the key1.</span><span class="sxs-lookup"><span data-stu-id="540c4-145">Take note of the account name and the key1.</span></span>
   
      ![Keys](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="540c4-147">We will need this information to configure your project in the next section.</span><span class="sxs-lookup"><span data-stu-id="540c4-147">We will need this information to configure your project in the next section.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="540c4-148">Configure the Project</span><span class="sxs-lookup"><span data-stu-id="540c4-148">Configure the Project</span></span>
<span data-ttu-id="540c4-149">In this section, we'll configure our application to use the storage account we just created.</span><span class="sxs-lookup"><span data-stu-id="540c4-149">In this section, we'll configure our application to use the storage account we just created.</span></span> <span data-ttu-id="540c4-150">We'll see how to obtain connection settings from the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="540c4-150">We'll see how to obtain connection settings from the Azure Portal.</span></span> <span data-ttu-id="540c4-151">Then we'll run the application locally.</span><span class="sxs-lookup"><span data-stu-id="540c4-151">Then we'll run the application locally.</span></span>

1. <span data-ttu-id="540c4-152">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="540c4-152">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="540c4-153">Click on the **Debug** tab.</span><span class="sxs-lookup"><span data-stu-id="540c4-153">Click on the **Debug** tab.</span></span>
   
     ![Project Debug Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="540c4-155">Set the values of environment variables required by the application in **Debug Server Command**, **Environment**.</span><span class="sxs-lookup"><span data-stu-id="540c4-155">Set the values of environment variables required by the application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="540c4-156">This will set the environment variables when you **Start Debugging**.</span><span class="sxs-lookup"><span data-stu-id="540c4-156">This will set the environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="540c4-157">If you want the variables to be set when you **Start Without Debugging**, set the same values under **Run Server Command** as well.</span><span class="sxs-lookup"><span data-stu-id="540c4-157">If you want the variables to be set when you **Start Without Debugging**, set the same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="540c4-158">Alternatively, you can define environment variables using the Windows Control Panel.</span><span class="sxs-lookup"><span data-stu-id="540c4-158">Alternatively, you can define environment variables using the Windows Control Panel.</span></span> <span data-ttu-id="540c4-159">This is a better option if you want to avoid storing credentials in source code / project file.</span><span class="sxs-lookup"><span data-stu-id="540c4-159">This is a better option if you want to avoid storing credentials in source code / project file.</span></span> <span data-ttu-id="540c4-160">Note that you will need to restart Visual Studio for the new environment values to be available to the application.</span><span class="sxs-lookup"><span data-stu-id="540c4-160">Note that you will need to restart Visual Studio for the new environment values to be available to the application.</span></span>
3. <span data-ttu-id="540c4-161">The code that implements the Azure Table Storage repository is in **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="540c4-161">The code that implements the Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="540c4-162">See the [documentation] for more information on how to use Table Service from Python.</span><span class="sxs-lookup"><span data-stu-id="540c4-162">See the [documentation] for more information on how to use Table Service from Python.</span></span>
4. <span data-ttu-id="540c4-163">Run the application with `F5`.</span><span class="sxs-lookup"><span data-stu-id="540c4-163">Run the application with `F5`.</span></span> <span data-ttu-id="540c4-164">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="540c4-164">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="540c4-165">The Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="540c4-165">The Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="540c4-166">Press `F5` to continue loading the web project.</span><span class="sxs-lookup"><span data-stu-id="540c4-166">Press `F5` to continue loading the web project.</span></span>
   > 
   > 
5. <span data-ttu-id="540c4-167">Browse to the **About** page to verify that the application is using the **Azure Table Storage** repository.</span><span class="sxs-lookup"><span data-stu-id="540c4-167">Browse to the **About** page to verify that the application is using the **Azure Table Storage** repository.</span></span>
   
     ![Web Browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-the-azure-table-storage"></a><span data-ttu-id="540c4-169">Explore the Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="540c4-169">Explore the Azure Table Storage</span></span>
<span data-ttu-id="540c4-170">It's easy to view and edit storage tables using Cloud Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="540c4-170">It's easy to view and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="540c4-171">In this section we'll use Server Explorer to view the contents of the polls application tables.</span><span class="sxs-lookup"><span data-stu-id="540c4-171">In this section we'll use Server Explorer to view the contents of the polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="540c4-172">This requires Microsoft Azure Tools to be installed, which are available as part of the [Azure SDK for .NET].</span><span class="sxs-lookup"><span data-stu-id="540c4-172">This requires Microsoft Azure Tools to be installed, which are available as part of the [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="540c4-173">Open **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="540c4-173">Open **Cloud Explorer**.</span></span> <span data-ttu-id="540c4-174">Expand **Storage Accounts**, your storage account, then **Tables**.</span><span class="sxs-lookup"><span data-stu-id="540c4-174">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="540c4-176">Double-click on the **polls** or **choices** table to view the contents of the table in a document window, as well as add/remove/edit entities.</span><span class="sxs-lookup"><span data-stu-id="540c4-176">Double-click on the **polls** or **choices** table to view the contents of the table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Table Query Results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="540c4-178">Publish the web app to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="540c4-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="540c4-179">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="540c4-179">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="540c4-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="540c4-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
     ![Publish Web Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="540c4-182">Click on **Microsoft Azure Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="540c4-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="540c4-183">Click on **New** to create a new web app.</span><span class="sxs-lookup"><span data-stu-id="540c4-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="540c4-184">Fill in the following fields and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="540c4-184">Fill in the following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="540c4-185">**Web App name**</span><span class="sxs-lookup"><span data-stu-id="540c4-185">**Web App name**</span></span>
   * <span data-ttu-id="540c4-186">**App Service plan**</span><span class="sxs-lookup"><span data-stu-id="540c4-186">**App Service plan**</span></span>
   * <span data-ttu-id="540c4-187">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="540c4-187">**Resource group**</span></span>
   * <span data-ttu-id="540c4-188">**Region**</span><span class="sxs-lookup"><span data-stu-id="540c4-188">**Region**</span></span>
   * <span data-ttu-id="540c4-189">Leave **Database server** set to **No database**</span><span class="sxs-lookup"><span data-stu-id="540c4-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="540c4-190">Accept all other defaults and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="540c4-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="540c4-191">Your web browser will open automatically to the published web app.</span><span class="sxs-lookup"><span data-stu-id="540c4-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="540c4-192">If you browse to the about page, you'll see that it uses the **In-Memory** repository, not the **Azure Table Storage** repository.</span><span class="sxs-lookup"><span data-stu-id="540c4-192">If you browse to the about page, you'll see that it uses the **In-Memory** repository, not the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="540c4-193">That's because the environment variables are not set on the Web Apps instance in Azure App Service, so it uses the default values specified in **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="540c4-193">That's because the environment variables are not set on the Web Apps instance in Azure App Service, so it uses the default values specified in **settings.py**.</span></span>

## <a name="configure-the-web-apps-instance"></a><span data-ttu-id="540c4-194">Configure the Web Apps instance</span><span class="sxs-lookup"><span data-stu-id="540c4-194">Configure the Web Apps instance</span></span>
<span data-ttu-id="540c4-195">In this section, we'll configure environment variables for the Web Apps instance.</span><span class="sxs-lookup"><span data-stu-id="540c4-195">In this section, we'll configure environment variables for the Web Apps instance.</span></span>

1. <span data-ttu-id="540c4-196">In [Azure Portal](https://portal.azure.com), open the web app's blade by clicking **Browse** > **App Services** > your web app name.</span><span class="sxs-lookup"><span data-stu-id="540c4-196">In [Azure Portal](https://portal.azure.com), open the web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="540c4-197">In your web app's blade, click **All Settings**, then click **Application Settings**.</span><span class="sxs-lookup"><span data-stu-id="540c4-197">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="540c4-198">Scroll down to the **App settings** section and set the values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in the **Configure the project** section above.</span><span class="sxs-lookup"><span data-stu-id="540c4-198">Scroll down to the **App settings** section and set the values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in the **Configure the project** section above.</span></span>
   
     ![App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="540c4-200">Click on **Save**.</span><span class="sxs-lookup"><span data-stu-id="540c4-200">Click on **Save**.</span></span> <span data-ttu-id="540c4-201">After you've received the notifications that the changes were applied, click on **Browse** from the Web app main blade.</span><span class="sxs-lookup"><span data-stu-id="540c4-201">After you've received the notifications that the changes were applied, click on **Browse** from the Web app main blade.</span></span>
5. <span data-ttu-id="540c4-202">You should see the web app working as expected, using the **Azure Table Storage** repository.</span><span class="sxs-lookup"><span data-stu-id="540c4-202">You should see the web app working as expected, using the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="540c4-203">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="540c4-203">Congratulations!</span></span>
   
     ![Web Browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="540c4-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="540c4-205">Next steps</span></span>
<span data-ttu-id="540c4-206">Follow these links to learn more about Python Tools for Visual Studio, Flask and Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="540c4-206">Follow these links to learn more about Python Tools for Visual Studio, Flask and Azure Table Storage.</span></span>

* <span data-ttu-id="540c4-207">[Python Tools for Visual Studio Documentation]</span><span class="sxs-lookup"><span data-stu-id="540c4-207">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="540c4-208">[Web Projects]</span><span class="sxs-lookup"><span data-stu-id="540c4-208">[Web Projects]</span></span>
  * <span data-ttu-id="540c4-209">[Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="540c4-209">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="540c4-210">[Remote Debugging on Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="540c4-210">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="540c4-211">[Flask Documentation]</span><span class="sxs-lookup"><span data-stu-id="540c4-211">[Flask Documentation]</span></span>
* <span data-ttu-id="540c4-212">[Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="540c4-212">[Azure Storage]</span></span>
* <span data-ttu-id="540c4-213">[Azure SDK for Python]</span><span class="sxs-lookup"><span data-stu-id="540c4-213">[Azure SDK for Python]</span></span>
* <span data-ttu-id="540c4-214">[How to Use the Table Storage Service from Python]</span><span class="sxs-lookup"><span data-stu-id="540c4-214">[How to Use the Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="540c4-215">What's changed</span><span class="sxs-lookup"><span data-stu-id="540c4-215">What's changed</span></span>
* <span data-ttu-id="540c4-216">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="540c4-216">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python Developer Center]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md
[documentation]: ../storage/storage-python-how-to-use-table-storage.md
[How to Use the Table Storage Service from Python]: ../storage/storage-python-how-to-use-table-storage.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK for .NET]: http://azure.microsoft.com/downloads/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?linkid=518003
[Python 2.7 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517191
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Flask Documentation]: http://flask.pocoo.org/
[Remote Debugging on Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web Projects]: http://go.microsoft.com/fwlink/?LinkId=624027
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure Storage]: http://azure.microsoft.com/documentation/services/storage/
[Azure SDK for Python]: https://github.com/Azure/azure-sdk-for-python













