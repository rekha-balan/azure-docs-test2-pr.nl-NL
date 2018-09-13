---
title: Create an ASP.NET app in Azure with SQL Database | Microsoft Docs
description: Learn how to get a ASP.NET app working in Azure, with connection to a SQL Database.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: ''
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 04/07/2017
ms.author: cephalin
ms.openlocfilehash: a3f98af95de7be143aef54dd426c3c9bddadfa8c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554734"
---
# <a name="create-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="bd39b-103">Create an ASP.NET app in Azure with SQL Database</span><span class="sxs-lookup"><span data-stu-id="bd39b-103">Create an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="bd39b-104">This tutorial shows you how to develop a data-driven ASP.NET web app in Azure, connect it to Azure SQL Database, and enable your data-driven functionality.</span><span class="sxs-lookup"><span data-stu-id="bd39b-104">This tutorial shows you how to develop a data-driven ASP.NET web app in Azure, connect it to Azure SQL Database, and enable your data-driven functionality.</span></span> <span data-ttu-id="bd39b-105">When you're finished, you'll have a ASP.NET application running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected to SQL Database.</span><span class="sxs-lookup"><span data-stu-id="bd39b-105">When you're finished, you'll have a ASP.NET application running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected to SQL Database.</span></span>

![Published ASP.NET application in Azure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

## <a name="before-you-begin"></a><span data-ttu-id="bd39b-107">Before you begin</span><span class="sxs-lookup"><span data-stu-id="bd39b-107">Before you begin</span></span>

<span data-ttu-id="bd39b-108">Before running this sample, [download and install the free Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bd39b-108">Before running this sample, [download and install the free Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="bd39b-109">Make sure that you enable **Azure development** during the Visual Studio setup.</span><span class="sxs-lookup"><span data-stu-id="bd39b-109">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="step-1---download-the-sample"></a><span data-ttu-id="bd39b-110">Step 1 - Download the sample</span><span class="sxs-lookup"><span data-stu-id="bd39b-110">Step 1 - Download the sample</span></span>
<span data-ttu-id="bd39b-111">In this step, you download a sample ASP.NET application.</span><span class="sxs-lookup"><span data-stu-id="bd39b-111">In this step, you download a sample ASP.NET application.</span></span>

### <a name="get-the-sample-project"></a><span data-ttu-id="bd39b-112">Get the sample project</span><span class="sxs-lookup"><span data-stu-id="bd39b-112">Get the sample project</span></span>

<span data-ttu-id="bd39b-113">Download the samples project by clicking [here](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="bd39b-113">Download the samples project by clicking [here](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="bd39b-114">Extract the downloaded `dotnet-sqldb-tutorial-master.zip` into a working directory.</span><span class="sxs-lookup"><span data-stu-id="bd39b-114">Extract the downloaded `dotnet-sqldb-tutorial-master.zip` into a working directory.</span></span>

> [!TIP]
> <span data-ttu-id="bd39b-115">You can get the same sample project by cloning the GitHub repository:</span><span class="sxs-lookup"><span data-stu-id="bd39b-115">You can get the same sample project by cloning the GitHub repository:</span></span>
>
> ```bash
> git clone https://github.com/Azure-Samples/dotnet-sqldb-tutorial.git
> ```
>
>

<span data-ttu-id="bd39b-116">This sample project contains a simple [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) application built on [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="bd39b-116">This sample project contains a simple [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) application built on [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-the-application"></a><span data-ttu-id="bd39b-117">Run the application</span><span class="sxs-lookup"><span data-stu-id="bd39b-117">Run the application</span></span>

<span data-ttu-id="bd39b-118">From the extracted directory, launch `dotnet-sqldb-tutorial-master\DotNetAppSqlDb.sln` in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="bd39b-118">From the extracted directory, launch `dotnet-sqldb-tutorial-master\DotNetAppSqlDb.sln` in Visual Studio 2017.</span></span>

<span data-ttu-id="bd39b-119">Once the sample solution is opened, type `F5` to run it in the browser.</span><span class="sxs-lookup"><span data-stu-id="bd39b-119">Once the sample solution is opened, type `F5` to run it in the browser.</span></span>

<span data-ttu-id="bd39b-120">You should see a simple to-do list in the homepage.</span><span class="sxs-lookup"><span data-stu-id="bd39b-120">You should see a simple to-do list in the homepage.</span></span> <span data-ttu-id="bd39b-121">Try to add a few to-dos to the empty list.</span><span class="sxs-lookup"><span data-stu-id="bd39b-121">Try to add a few to-dos to the empty list.</span></span>

![New ASP.NET Project dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="bd39b-123">Your database context uses a connection string called `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="bd39b-123">Your database context uses a connection string called `MyDbConnection`.</span></span> <span data-ttu-id="bd39b-124">This connection string is defined in `Web.config` and referenced in `Models\MyDatabaseContext.cs`.</span><span class="sxs-lookup"><span data-stu-id="bd39b-124">This connection string is defined in `Web.config` and referenced in `Models\MyDatabaseContext.cs`.</span></span> <span data-ttu-id="bd39b-125">The connection string name is all you will need later when connecting your Azure web app to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="bd39b-125">The connection string name is all you will need later when connecting your Azure web app to Azure SQL Database.</span></span> 

## <a name="step-2---publish-to-azure-with-sql-database"></a><span data-ttu-id="bd39b-126">Step 2 - Publish to Azure with SQL Database</span><span class="sxs-lookup"><span data-stu-id="bd39b-126">Step 2 - Publish to Azure with SQL Database</span></span>

<span data-ttu-id="bd39b-127">In the **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-127">In the **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Publish from Solution Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="bd39b-129">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-129">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Publish from project overview page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="bd39b-131">This opens the **Create App Service** dialog, which helps you create all the Azure resources you need to run your ASP.NET web app in Azure.</span><span class="sxs-lookup"><span data-stu-id="bd39b-131">This opens the **Create App Service** dialog, which helps you create all the Azure resources you need to run your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="bd39b-132">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="bd39b-132">Sign in to Azure</span></span>

<span data-ttu-id="bd39b-133">In the **Create App Service** dialog, click **Add an account**, and then sign in to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="bd39b-133">In the **Create App Service** dialog, click **Add an account**, and then sign in to your Azure subscription.</span></span> <span data-ttu-id="bd39b-134">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="bd39b-134">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="bd39b-135">If the signed-in Microsoft account doesn't have your Azure subscription, click it to add the correct account.</span><span class="sxs-lookup"><span data-stu-id="bd39b-135">If the signed-in Microsoft account doesn't have your Azure subscription, click it to add the correct account.</span></span>
   
![Sign in to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="bd39b-137">Once signed in, you're ready to create all the resources you need for your Azure web app in this dialog.</span><span class="sxs-lookup"><span data-stu-id="bd39b-137">Once signed in, you're ready to create all the resources you need for your Azure web app in this dialog.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="bd39b-138">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="bd39b-138">Create a resource group</span></span>

<span data-ttu-id="bd39b-139">First, you need a _resource group_.</span><span class="sxs-lookup"><span data-stu-id="bd39b-139">First, you need a _resource group_.</span></span> 

> [!NOTE] 
> <span data-ttu-id="bd39b-140">A resource group is a logical container into which Azure resources like web apps, databases, and storage accounts are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="bd39b-140">A resource group is a logical container into which Azure resources like web apps, databases, and storage accounts are deployed and managed.</span></span>
>
>

<span data-ttu-id="bd39b-141">Next to **Resource Group**, click **New**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-141">Next to **Resource Group**, click **New**.</span></span>

<span data-ttu-id="bd39b-142">Name your resource group **myResourceGroup** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-142">Name your resource group **myResourceGroup** and click **OK**.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="bd39b-143">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="bd39b-143">Create an App Service plan</span></span>

<span data-ttu-id="bd39b-144">Your Azure web app also needs an _App Service plan_.</span><span class="sxs-lookup"><span data-stu-id="bd39b-144">Your Azure web app also needs an _App Service plan_.</span></span> 

> [!NOTE]
> <span data-ttu-id="bd39b-145">An App Service plan represents the collection of physical resources used to host your apps.</span><span class="sxs-lookup"><span data-stu-id="bd39b-145">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="bd39b-146">All apps assigned to an App Service plan share the resources defined by it, which enables you to save cost when hosting multiple apps.</span><span class="sxs-lookup"><span data-stu-id="bd39b-146">All apps assigned to an App Service plan share the resources defined by it, which enables you to save cost when hosting multiple apps.</span></span> 
>
> <span data-ttu-id="bd39b-147">App Service plans define:</span><span class="sxs-lookup"><span data-stu-id="bd39b-147">App Service plans define:</span></span>
>
> - <span data-ttu-id="bd39b-148">Region (North Europe, East US, Southeast Asia)</span><span class="sxs-lookup"><span data-stu-id="bd39b-148">Region (North Europe, East US, Southeast Asia)</span></span>
> - <span data-ttu-id="bd39b-149">Instance Size (Small, Medium, Large)</span><span class="sxs-lookup"><span data-stu-id="bd39b-149">Instance Size (Small, Medium, Large)</span></span>
> - <span data-ttu-id="bd39b-150">Scale Count (one, two, or three instances, etc.)</span><span class="sxs-lookup"><span data-stu-id="bd39b-150">Scale Count (one, two, or three instances, etc.)</span></span> 
> - <span data-ttu-id="bd39b-151">SKU (Free, Shared, Basic, Standard, Premium)</span><span class="sxs-lookup"><span data-stu-id="bd39b-151">SKU (Free, Shared, Basic, Standard, Premium)</span></span>
>
>

<span data-ttu-id="bd39b-152">Next to **App Service Plan**, click **New**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-152">Next to **App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="bd39b-153">In the **Configure App Service Plan** dialog, configure the new App Service plan with the following settings:</span><span class="sxs-lookup"><span data-stu-id="bd39b-153">In the **Configure App Service Plan** dialog, configure the new App Service plan with the following settings:</span></span>

- <span data-ttu-id="bd39b-154">**App Service Plan**: Type **myAppServicePlan**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-154">**App Service Plan**: Type **myAppServicePlan**.</span></span> 
- <span data-ttu-id="bd39b-155">**Location**: Choose **West Europe**, or any other region you like.</span><span class="sxs-lookup"><span data-stu-id="bd39b-155">**Location**: Choose **West Europe**, or any other region you like.</span></span>
- <span data-ttu-id="bd39b-156">**Size**: Choose **Free**, or any other [pricing tier](https://azure.microsoft.com/pricing/details/app-service/) you like.</span><span class="sxs-lookup"><span data-stu-id="bd39b-156">**Size**: Choose **Free**, or any other [pricing tier](https://azure.microsoft.com/pricing/details/app-service/) you like.</span></span>

<span data-ttu-id="bd39b-157">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-157">Click **OK**.</span></span>

![Create App Service plan](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

### <a name="configure-the-web-app-name"></a><span data-ttu-id="bd39b-159">Configure the web app name</span><span class="sxs-lookup"><span data-stu-id="bd39b-159">Configure the web app name</span></span>

<span data-ttu-id="bd39b-160">In **Web App Name**, type a unique app name.</span><span class="sxs-lookup"><span data-stu-id="bd39b-160">In **Web App Name**, type a unique app name.</span></span> <span data-ttu-id="bd39b-161">This name will be used as part of the default DNS name for your app (`<app_name>.azurewebsites.net`), so it needs to be unique across all apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="bd39b-161">This name will be used as part of the default DNS name for your app (`<app_name>.azurewebsites.net`), so it needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="bd39b-162">You can later map a custom domain name to your app before you expose it to your users.</span><span class="sxs-lookup"><span data-stu-id="bd39b-162">You can later map a custom domain name to your app before you expose it to your users.</span></span>

<span data-ttu-id="bd39b-163">You can also accept the automatically generated name, which is already unique.</span><span class="sxs-lookup"><span data-stu-id="bd39b-163">You can also accept the automatically generated name, which is already unique.</span></span>

<span data-ttu-id="bd39b-164">To prepare for the next step, click **Explore additional Azure services**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-164">To prepare for the next step, click **Explore additional Azure services**.</span></span>

![Configure web app name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="bd39b-166">Create a SQL Server instance</span><span class="sxs-lookup"><span data-stu-id="bd39b-166">Create a SQL Server instance</span></span>

<span data-ttu-id="bd39b-167">In the **Services** tab, click the **+** icon next to **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-167">In the **Services** tab, click the **+** icon next to **SQL Database**.</span></span> 

<span data-ttu-id="bd39b-168">In the **Configure SQL Database** dialog, click **New** next to **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-168">In the **Configure SQL Database** dialog, click **New** next to **SQL Server**.</span></span> 

<span data-ttu-id="bd39b-169">In **Server Name**, type a unique name.</span><span class="sxs-lookup"><span data-stu-id="bd39b-169">In **Server Name**, type a unique name.</span></span> <span data-ttu-id="bd39b-170">This name will be used as part of the default DNS name for your database server (`<server_name>.database.windows.net`), so it needs to be unique across all SQL Server instances in Azure.</span><span class="sxs-lookup"><span data-stu-id="bd39b-170">This name will be used as part of the default DNS name for your database server (`<server_name>.database.windows.net`), so it needs to be unique across all SQL Server instances in Azure.</span></span> 

<span data-ttu-id="bd39b-171">Configure the rest of the fields as you like and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-171">Configure the rest of the fields as you like and click **OK**.</span></span>

![Create SQL Server instance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="configure-the-sql-database"></a><span data-ttu-id="bd39b-173">Configure the SQL Database</span><span class="sxs-lookup"><span data-stu-id="bd39b-173">Configure the SQL Database</span></span>

<span data-ttu-id="bd39b-174">In **Database Name**, type `myToDoAppDb`, or any name you like.</span><span class="sxs-lookup"><span data-stu-id="bd39b-174">In **Database Name**, type `myToDoAppDb`, or any name you like.</span></span>

<span data-ttu-id="bd39b-175">In **Connection String Name**, type `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="bd39b-175">In **Connection String Name**, type `MyDbConnection`.</span></span> <span data-ttu-id="bd39b-176">This name must match the connection string that is referenced in `Models\MyDatabaseContext.cs`.</span><span class="sxs-lookup"><span data-stu-id="bd39b-176">This name must match the connection string that is referenced in `Models\MyDatabaseContext.cs`.</span></span>

![Configure SQL Database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

### <a name="create-and-publish-the-web-app"></a><span data-ttu-id="bd39b-178">Create and publish the web app</span><span class="sxs-lookup"><span data-stu-id="bd39b-178">Create and publish the web app</span></span>

<span data-ttu-id="bd39b-179">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-179">Click **Create**.</span></span> 

<span data-ttu-id="bd39b-180">Once the wizard finishes creating the Azure resources, it automatically publishes your ASP.NET application to Azure for the first time, and then launches the published Azure web app in your default browser.</span><span class="sxs-lookup"><span data-stu-id="bd39b-180">Once the wizard finishes creating the Azure resources, it automatically publishes your ASP.NET application to Azure for the first time, and then launches the published Azure web app in your default browser.</span></span>

<span data-ttu-id="bd39b-181">Try to add a few to-do items to the empty list.</span><span class="sxs-lookup"><span data-stu-id="bd39b-181">Try to add a few to-do items to the empty list.</span></span>

![Published ASP.NET application in Azure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="bd39b-183">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="bd39b-183">Congratulations!</span></span> <span data-ttu-id="bd39b-184">Your data-driven ASP.NET application is running live in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="bd39b-184">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="step-3---access-the-sql-database-locally"></a><span data-ttu-id="bd39b-185">Step 3 - Access the SQL Database locally</span><span class="sxs-lookup"><span data-stu-id="bd39b-185">Step 3 - Access the SQL Database locally</span></span>

<span data-ttu-id="bd39b-186">Visual Studio lets you explorer and manage your new SQL Database easily in the **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-186">Visual Studio lets you explorer and manage your new SQL Database easily in the **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="bd39b-187">Create a database connection</span><span class="sxs-lookup"><span data-stu-id="bd39b-187">Create a database connection</span></span>

<span data-ttu-id="bd39b-188">Open **SQL Server Object Explorer** by typing `Ctrl`+`\`, `Ctrl`+`S`.</span><span class="sxs-lookup"><span data-stu-id="bd39b-188">Open **SQL Server Object Explorer** by typing `Ctrl`+`\`, `Ctrl`+`S`.</span></span>

<span data-ttu-id="bd39b-189">At the top of **SQL Server Object Explorer**, click the **Add SQL Server** button.</span><span class="sxs-lookup"><span data-stu-id="bd39b-189">At the top of **SQL Server Object Explorer**, click the **Add SQL Server** button.</span></span>

### <a name="configure-the-database-connection"></a><span data-ttu-id="bd39b-190">Configure the database connection</span><span class="sxs-lookup"><span data-stu-id="bd39b-190">Configure the database connection</span></span>

<span data-ttu-id="bd39b-191">In the **Connect** dialog, expand the **Azure** node.</span><span class="sxs-lookup"><span data-stu-id="bd39b-191">In the **Connect** dialog, expand the **Azure** node.</span></span> <span data-ttu-id="bd39b-192">All your SQL Databases in Azure are listed here.</span><span class="sxs-lookup"><span data-stu-id="bd39b-192">All your SQL Databases in Azure are listed here.</span></span>

<span data-ttu-id="bd39b-193">Select the SQL Database that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="bd39b-193">Select the SQL Database that you created earlier.</span></span> <span data-ttu-id="bd39b-194">The connection you used earlier are automatically filled at the bottom.</span><span class="sxs-lookup"><span data-stu-id="bd39b-194">The connection you used earlier are automatically filled at the bottom.</span></span>

<span data-ttu-id="bd39b-195">Type the database administrator password you used earlier and click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-195">Type the database administrator password you used earlier and click **Connect**.</span></span>

![Configure database connection from Visual Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="bd39b-197">Allow client connection from your computer</span><span class="sxs-lookup"><span data-stu-id="bd39b-197">Allow client connection from your computer</span></span>

<span data-ttu-id="bd39b-198">The **Create a new firewall rule** dialog is opened.</span><span class="sxs-lookup"><span data-stu-id="bd39b-198">The **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="bd39b-199">By default, your SQL Server instance only allows connections from Azure services, such as your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="bd39b-199">By default, your SQL Server instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="bd39b-200">To connect to your database directly from Visual Studio, you need to create a firewall rule in the SQL Server instance to allow the public IP address of your local computer.</span><span class="sxs-lookup"><span data-stu-id="bd39b-200">To connect to your database directly from Visual Studio, you need to create a firewall rule in the SQL Server instance to allow the public IP address of your local computer.</span></span>

<span data-ttu-id="bd39b-201">This is easy in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bd39b-201">This is easy in Visual Studio.</span></span> <span data-ttu-id="bd39b-202">The dialog is already filled with your computer's public IP address.</span><span class="sxs-lookup"><span data-stu-id="bd39b-202">The dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="bd39b-203">Make sure that **Add my client IP** is selected and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-203">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Set firewall for SQL Server instance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="bd39b-205">Once Visual Studio finishes creating the firewall setting for your SQL Server instance, your connection shows up in **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-205">Once Visual Studio finishes creating the firewall setting for your SQL Server instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="bd39b-206">Here, you can perform the most common database operations, such as run queries, create views and stored procedures, and more.</span><span class="sxs-lookup"><span data-stu-id="bd39b-206">Here, you can perform the most common database operations, such as run queries, create views and stored procedures, and more.</span></span> <span data-ttu-id="bd39b-207">The following example shows you how to view database data.</span><span class="sxs-lookup"><span data-stu-id="bd39b-207">The following example shows you how to view database data.</span></span> 

![Explore SQL Database objects](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="step-4---update-app-with-code-first-migrations"></a><span data-ttu-id="bd39b-209">Step 4 - Update app with Code First Migrations</span><span class="sxs-lookup"><span data-stu-id="bd39b-209">Step 4 - Update app with Code First Migrations</span></span>

<span data-ttu-id="bd39b-210">In this step, you'll use Code First Migrations in Entity Framework to make a change to your database schema and publish it to Azure.</span><span class="sxs-lookup"><span data-stu-id="bd39b-210">In this step, you'll use Code First Migrations in Entity Framework to make a change to your database schema and publish it to Azure.</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="bd39b-211">Update your data model</span><span class="sxs-lookup"><span data-stu-id="bd39b-211">Update your data model</span></span>

<span data-ttu-id="bd39b-212">Open `Models\Todo.cs` in the code editor.</span><span class="sxs-lookup"><span data-stu-id="bd39b-212">Open `Models\Todo.cs` in the code editor.</span></span> <span data-ttu-id="bd39b-213">Add the following property to the `ToDo` class:</span><span class="sxs-lookup"><span data-stu-id="bd39b-213">Add the following property to the `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="bd39b-214">Run Code First Migrations locally</span><span class="sxs-lookup"><span data-stu-id="bd39b-214">Run Code First Migrations locally</span></span>

<span data-ttu-id="bd39b-215">Next, run a few commands to make updates to your localdb database.</span><span class="sxs-lookup"><span data-stu-id="bd39b-215">Next, run a few commands to make updates to your localdb database.</span></span> 

<span data-ttu-id="bd39b-216">From the **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-216">From the **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="bd39b-217">The console is usually opened in the bottom window.</span><span class="sxs-lookup"><span data-stu-id="bd39b-217">The console is usually opened in the bottom window.</span></span>

<span data-ttu-id="bd39b-218">Enable Code First Migrations like this:</span><span class="sxs-lookup"><span data-stu-id="bd39b-218">Enable Code First Migrations like this:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="bd39b-219">Add a migration like this:</span><span class="sxs-lookup"><span data-stu-id="bd39b-219">Add a migration like this:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="bd39b-220">Update the localdb database like this:</span><span class="sxs-lookup"><span data-stu-id="bd39b-220">Update the localdb database like this:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="bd39b-221">Test your changes by running the application with `F5`.</span><span class="sxs-lookup"><span data-stu-id="bd39b-221">Test your changes by running the application with `F5`.</span></span>

<span data-ttu-id="bd39b-222">If the application loads without errors, then Code First Migrations has succeeded.</span><span class="sxs-lookup"><span data-stu-id="bd39b-222">If the application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="bd39b-223">However, your page still looks the same because your application logic is not using this new property yet.</span><span class="sxs-lookup"><span data-stu-id="bd39b-223">However, your page still looks the same because your application logic is not using this new property yet.</span></span> 

### <a name="use-the-new-property"></a><span data-ttu-id="bd39b-224">Use the new property</span><span class="sxs-lookup"><span data-stu-id="bd39b-224">Use the new property</span></span>

<span data-ttu-id="bd39b-225">Lets make some changes in your code to use the `Done` property.</span><span class="sxs-lookup"><span data-stu-id="bd39b-225">Lets make some changes in your code to use the `Done` property.</span></span> <span data-ttu-id="bd39b-226">For simplicity in this tutorial, you're only going to change the `Index` and `Create` views to see the property in action.</span><span class="sxs-lookup"><span data-stu-id="bd39b-226">For simplicity in this tutorial, you're only going to change the `Index` and `Create` views to see the property in action.</span></span>

<span data-ttu-id="bd39b-227">Open `Controllers\TodosController.cs`.</span><span class="sxs-lookup"><span data-stu-id="bd39b-227">Open `Controllers\TodosController.cs`.</span></span>

<span data-ttu-id="bd39b-228">Find the `Create()` method and add `Done` to the list of properties in the `Bind` attribute.</span><span class="sxs-lookup"><span data-stu-id="bd39b-228">Find the `Create()` method and add `Done` to the list of properties in the `Bind` attribute.</span></span> <span data-ttu-id="bd39b-229">When you're done, your `Create()` method signature should look like this:</span><span class="sxs-lookup"><span data-stu-id="bd39b-229">When you're done, your `Create()` method signature should look like this:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="bd39b-230">Open `Views\Todos\Create.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="bd39b-230">Open `Views\Todos\Create.cshtml`.</span></span>

<span data-ttu-id="bd39b-231">In the Razor code, you should see a `<div class="form-group">` tag that uses `model.Description`, and then another `<div class="form-group">` tag that uses `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="bd39b-231">In the Razor code, you should see a `<div class="form-group">` tag that uses `model.Description`, and then another `<div class="form-group">` tag that uses `model.CreatedDate`.</span></span> <span data-ttu-id="bd39b-232">Immediately following these two tags, add another `<div class="form-group">` tag that uses `model.Done`, like this:</span><span class="sxs-lookup"><span data-stu-id="bd39b-232">Immediately following these two tags, add another `<div class="form-group">` tag that uses `model.Done`, like this:</span></span>

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

<span data-ttu-id="bd39b-233">Open `Views\Todos\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="bd39b-233">Open `Views\Todos\Index.cshtml`.</span></span>

<span data-ttu-id="bd39b-234">Search for the empty `<th></th>` tag.</span><span class="sxs-lookup"><span data-stu-id="bd39b-234">Search for the empty `<th></th>` tag.</span></span> <span data-ttu-id="bd39b-235">Just above this tag, add the following Razor code:</span><span class="sxs-lookup"><span data-stu-id="bd39b-235">Just above this tag, add the following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="bd39b-236">Find the `<td>` tag that contains the `Html.ActionLink()` helper methods.</span><span class="sxs-lookup"><span data-stu-id="bd39b-236">Find the `<td>` tag that contains the `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="bd39b-237">Just above this tag, add the following Razor code:</span><span class="sxs-lookup"><span data-stu-id="bd39b-237">Just above this tag, add the following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="bd39b-238">That's all you need to see the changes in the `Index` and `Create` views.</span><span class="sxs-lookup"><span data-stu-id="bd39b-238">That's all you need to see the changes in the `Index` and `Create` views.</span></span> 

<span data-ttu-id="bd39b-239">Type `F5` again to run the application.</span><span class="sxs-lookup"><span data-stu-id="bd39b-239">Type `F5` again to run the application.</span></span>

<span data-ttu-id="bd39b-240">You should be able now to add a to-do item and check **Done**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-240">You should be able now to add a to-do item and check **Done**.</span></span> <span data-ttu-id="bd39b-241">Then it should show up in your homepage as a completed item.</span><span class="sxs-lookup"><span data-stu-id="bd39b-241">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="bd39b-242">Remember that this is all you can do for now because you didn't change the `Edit` view.</span><span class="sxs-lookup"><span data-stu-id="bd39b-242">Remember that this is all you can do for now because you didn't change the `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="bd39b-243">Enable Code First Migrations in Azure</span><span class="sxs-lookup"><span data-stu-id="bd39b-243">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="bd39b-244">Now that your code change works, including database migration, you publish it to your Azure web app and update your SQL Database with Code First Migrations too.</span><span class="sxs-lookup"><span data-stu-id="bd39b-244">Now that your code change works, including database migration, you publish it to your Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="bd39b-245">Just like before, right-click your project and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-245">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="bd39b-246">Click **Settings** to open the publish wizard.</span><span class="sxs-lookup"><span data-stu-id="bd39b-246">Click **Settings** to open the publish wizard.</span></span>

![Open publish settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="bd39b-248">In the wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-248">In the wizard, click **Next**.</span></span>

<span data-ttu-id="bd39b-249">Make sure that the connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-249">Make sure that the connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="bd39b-250">You may need to select the **myToDoAppDb** database from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="bd39b-250">You may need to select the **myToDoAppDb** database from the dropdown.</span></span> 

<span data-ttu-id="bd39b-251">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-251">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Enable Code First Migrations in Azure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="bd39b-253">Publish your changes</span><span class="sxs-lookup"><span data-stu-id="bd39b-253">Publish your changes</span></span>

<span data-ttu-id="bd39b-254">Now that you enabled Code First Migrations in your Azure web app, just publish your code changes.</span><span class="sxs-lookup"><span data-stu-id="bd39b-254">Now that you enabled Code First Migrations in your Azure web app, just publish your code changes.</span></span>

<span data-ttu-id="bd39b-255">In the publish page, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-255">In the publish page, click **Publish**.</span></span>

<span data-ttu-id="bd39b-256">Try creating new to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span><span class="sxs-lookup"><span data-stu-id="bd39b-256">Try creating new to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Azure web app after Code First Migration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

> [!NOTE]
> <span data-ttu-id="bd39b-258">Note that all your existing to-do items are still displayed.</span><span class="sxs-lookup"><span data-stu-id="bd39b-258">Note that all your existing to-do items are still displayed.</span></span> <span data-ttu-id="bd39b-259">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span><span class="sxs-lookup"><span data-stu-id="bd39b-259">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="bd39b-260">Also, Code First Migrations only changes the data schema and leaves your existing data intact.</span><span class="sxs-lookup"><span data-stu-id="bd39b-260">Also, Code First Migrations only changes the data schema and leaves your existing data intact.</span></span>
>
>

## <a name="step-6---stream-application-logs"></a><span data-ttu-id="bd39b-261">Step 6 - Stream application logs</span><span class="sxs-lookup"><span data-stu-id="bd39b-261">Step 6 - Stream application logs</span></span>

<span data-ttu-id="bd39b-262">You can stream tracing messages directly from your Azure web app to Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bd39b-262">You can stream tracing messages directly from your Azure web app to Visual Studio.</span></span>

<span data-ttu-id="bd39b-263">Open `Controllers\TodosController.cs`.</span><span class="sxs-lookup"><span data-stu-id="bd39b-263">Open `Controllers\TodosController.cs`.</span></span>

<span data-ttu-id="bd39b-264">Note that each action starts with a `Trace.WriteLine()` method.</span><span class="sxs-lookup"><span data-stu-id="bd39b-264">Note that each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="bd39b-265">This code is added to show you how easy it is to add trace messages to your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="bd39b-265">This code is added to show you how easy it is to add trace messages to your Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="bd39b-266">Open Server Explorer</span><span class="sxs-lookup"><span data-stu-id="bd39b-266">Open Server Explorer</span></span>

<span data-ttu-id="bd39b-267">You can configure logging for your Azure web app in **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-267">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

<span data-ttu-id="bd39b-268">To open it, type `Ctrl`+`Alt`+`S`.</span><span class="sxs-lookup"><span data-stu-id="bd39b-268">To open it, type `Ctrl`+`Alt`+`S`.</span></span>

### <a name="enable-log-streaming"></a><span data-ttu-id="bd39b-269">Enable log streaming</span><span class="sxs-lookup"><span data-stu-id="bd39b-269">Enable log streaming</span></span>

<span data-ttu-id="bd39b-270">In **Server Explorer**, expand **Azure** > **App Service**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-270">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="bd39b-271">Expand the **myResourceGroup** resource group, you created when you first created the Azure web app.</span><span class="sxs-lookup"><span data-stu-id="bd39b-271">Expand the **myResourceGroup** resource group, you created when you first created the Azure web app.</span></span>

<span data-ttu-id="bd39b-272">Right-click your Azure web app and select **View Streaming Longs**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-272">Right-click your Azure web app and select **View Streaming Longs**.</span></span>

![Enable log streaming](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="bd39b-274">The logs are now streamed into the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="bd39b-274">The logs are now streamed into the **Output** window.</span></span> 

![Log streaming in Output window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="bd39b-276">However, you won't see any of the trace messages yet.</span><span class="sxs-lookup"><span data-stu-id="bd39b-276">However, you won't see any of the trace messages yet.</span></span> <span data-ttu-id="bd39b-277">That's because when you first select **View Streaming Logs**, your Azure web app sets the trace level to `Error`, which only logs error events (with the `Trace.TraceError()` method).</span><span class="sxs-lookup"><span data-stu-id="bd39b-277">That's because when you first select **View Streaming Logs**, your Azure web app sets the trace level to `Error`, which only logs error events (with the `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="bd39b-278">Change trace levels</span><span class="sxs-lookup"><span data-stu-id="bd39b-278">Change trace levels</span></span>

<span data-ttu-id="bd39b-279">To change the trace levels to output other trace messages, go back to **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-279">To change the trace levels to output other trace messages, go back to **Server Explorer**.</span></span>

<span data-ttu-id="bd39b-280">Right-click your Azure web app again and select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-280">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="bd39b-281">In the **Application Logging (File System)** dropdown, select **Verbose**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-281">In the **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="bd39b-282">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bd39b-282">Click **Save**.</span></span>

![Change trace level to Verbose](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="bd39b-284">You can experiment with different trace levels to see what types of messages is displayed for each level.</span><span class="sxs-lookup"><span data-stu-id="bd39b-284">You can experiment with different trace levels to see what types of messages is displayed for each level.</span></span> <span data-ttu-id="bd39b-285">For example, the **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="bd39b-285">For example, the **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="bd39b-286">In your browser, try clicking around the to-do list application in Azure.</span><span class="sxs-lookup"><span data-stu-id="bd39b-286">In your browser, try clicking around the to-do list application in Azure.</span></span> <span data-ttu-id="bd39b-287">The trace messages are now streamed to the **Output** window in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bd39b-287">The trace messages are now streamed to the **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```

### <a name="stop-log-streaming"></a><span data-ttu-id="bd39b-288">Stop log streaming</span><span class="sxs-lookup"><span data-stu-id="bd39b-288">Stop log streaming</span></span>

<span data-ttu-id="bd39b-289">To stop the log-streaming service, click the **Stop monitoring** button in the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="bd39b-289">To stop the log-streaming service, click the **Stop monitoring** button in the **Output** window.</span></span>

![Stop log streaming](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="step-7---manage-your-azure-web-app"></a><span data-ttu-id="bd39b-291">Step 7 - Manage your Azure web app</span><span class="sxs-lookup"><span data-stu-id="bd39b-291">Step 7 - Manage your Azure web app</span></span>

<span data-ttu-id="bd39b-292">Go to the Azure portal to see the web app you created.</span><span class="sxs-lookup"><span data-stu-id="bd39b-292">Go to the Azure portal to see the web app you created.</span></span> 

<span data-ttu-id="bd39b-293">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bd39b-293">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="bd39b-294">From the left menu, click **App Service**, then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="bd39b-294">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="bd39b-296">You have landed in your web app's _blade_ (a portal page that opens horizontally).</span><span class="sxs-lookup"><span data-stu-id="bd39b-296">You have landed in your web app's _blade_ (a portal page that opens horizontally).</span></span> 

<span data-ttu-id="bd39b-297">By default, your web app's blade shows the **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="bd39b-297">By default, your web app's blade shows the **Overview** page.</span></span> <span data-ttu-id="bd39b-298">This page gives you a view of how your app is doing.</span><span class="sxs-lookup"><span data-stu-id="bd39b-298">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="bd39b-299">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="bd39b-299">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="bd39b-300">The tabs on the left side of the blade show the different configuration pages you can open.</span><span class="sxs-lookup"><span data-stu-id="bd39b-300">The tabs on the left side of the blade show the different configuration pages you can open.</span></span> 

![App Service blade in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

<span data-ttu-id="bd39b-302">These tabs in the blade show the many great features you can add to your web app.</span><span class="sxs-lookup"><span data-stu-id="bd39b-302">These tabs in the blade show the many great features you can add to your web app.</span></span> <span data-ttu-id="bd39b-303">The following list gives you just a few of the possibilities:</span><span class="sxs-lookup"><span data-stu-id="bd39b-303">The following list gives you just a few of the possibilities:</span></span>

- <span data-ttu-id="bd39b-304">Map a custom DNS name</span><span class="sxs-lookup"><span data-stu-id="bd39b-304">Map a custom DNS name</span></span>
- <span data-ttu-id="bd39b-305">Bind a custom SSL certificate</span><span class="sxs-lookup"><span data-stu-id="bd39b-305">Bind a custom SSL certificate</span></span>
- <span data-ttu-id="bd39b-306">Configure continuous deployment</span><span class="sxs-lookup"><span data-stu-id="bd39b-306">Configure continuous deployment</span></span>
- <span data-ttu-id="bd39b-307">Scale up and out</span><span class="sxs-lookup"><span data-stu-id="bd39b-307">Scale up and out</span></span>
- <span data-ttu-id="bd39b-308">Add user authentication</span><span class="sxs-lookup"><span data-stu-id="bd39b-308">Add user authentication</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd39b-309">Next steps</span><span class="sxs-lookup"><span data-stu-id="bd39b-309">Next steps</span></span>

<span data-ttu-id="bd39b-310">Explore pre-created [Web apps PowerShell scripts](app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bd39b-310">Explore pre-created [Web apps PowerShell scripts](app-service-powershell-samples.md).</span></span>





















