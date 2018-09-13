---
title: Build an ASP.NET app in Azure with SQL Database | Microsoft Docs
description: Learn how to deploy a C# ASP.NET app with a SQL Server database to Azure.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/25/2018
ms.author: cephalin
ms.custom: mvc, devcenter, vs-azure
ms.openlocfilehash: b438ac221483fec7ea90847ec27a105a3f21ab78
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966004"
---
# <a name="tutorial-build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="19ae4-103">Tutorial: Build an ASP.NET app in Azure with SQL Database</span><span class="sxs-lookup"><span data-stu-id="19ae4-103">Tutorial: Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="19ae4-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span><span class="sxs-lookup"><span data-stu-id="19ae4-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="19ae4-105">This tutorial shows you how to deploy a data-driven ASP.NET web app in Azure and connect it to [Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="19ae4-105">This tutorial shows you how to deploy a data-driven ASP.NET web app in Azure and connect it to [Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="19ae4-106">When you're finished, you have a ASP.NET app running in Azure and connected to SQL Database.</span><span class="sxs-lookup"><span data-stu-id="19ae4-106">When you're finished, you have a ASP.NET app running in Azure and connected to SQL Database.</span></span>

![Published ASP.NET application in Azure web app](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="19ae4-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="19ae4-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="19ae4-109">Create a SQL Database in Azure</span><span class="sxs-lookup"><span data-stu-id="19ae4-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="19ae4-110">Connect an ASP.NET app to SQL Database</span><span class="sxs-lookup"><span data-stu-id="19ae4-110">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="19ae4-111">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="19ae4-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="19ae4-112">Update the data model and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="19ae4-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="19ae4-113">Stream logs from Azure to your terminal</span><span class="sxs-lookup"><span data-stu-id="19ae4-113">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="19ae4-114">Manage the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="19ae4-114">Manage the app in the Azure portal</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="19ae4-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="19ae4-115">Prerequisites</span></span>

<span data-ttu-id="19ae4-116">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="19ae4-116">To complete this tutorial:</span></span>

<span data-ttu-id="19ae4-117">Install <a href="https://www.visualstudio.com/downloads/" target="_blank">Visual Studio 2017</a> with the **ASP.NET and web development** workload.</span><span class="sxs-lookup"><span data-stu-id="19ae4-117">Install <a href="https://www.visualstudio.com/downloads/" target="_blank">Visual Studio 2017</a> with the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="19ae4-118">If you've installed Visual Studio already, add the workloads in Visual Studio by clicking **Tools** > **Get Tools and Features**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-118">If you've installed Visual Studio already, add the workloads in Visual Studio by clicking **Tools** > **Get Tools and Features**.</span></span>

## <a name="download-the-sample"></a><span data-ttu-id="19ae4-119">Download the sample</span><span class="sxs-lookup"><span data-stu-id="19ae4-119">Download the sample</span></span>

- <span data-ttu-id="19ae4-120">[Download the sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="19ae4-120">[Download the sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>
- <span data-ttu-id="19ae4-121">Extract (unzip) the  *dotnet-sqldb-tutorial-master.zip* file.</span><span class="sxs-lookup"><span data-stu-id="19ae4-121">Extract (unzip) the  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="19ae4-122">The sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) create-read-update-delete (CRUD) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="19ae4-122">The sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) create-read-update-delete (CRUD) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-the-app"></a><span data-ttu-id="19ae4-123">Run the app</span><span class="sxs-lookup"><span data-stu-id="19ae4-123">Run the app</span></span>

<span data-ttu-id="19ae4-124">Open the *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19ae4-124">Open the *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="19ae4-125">Type `Ctrl+F5` to run the app without debugging.</span><span class="sxs-lookup"><span data-stu-id="19ae4-125">Type `Ctrl+F5` to run the app without debugging.</span></span> <span data-ttu-id="19ae4-126">The app is displayed in your default browser.</span><span class="sxs-lookup"><span data-stu-id="19ae4-126">The app is displayed in your default browser.</span></span> <span data-ttu-id="19ae4-127">Select the **Create New** link and create a couple *to-do* items.</span><span class="sxs-lookup"><span data-stu-id="19ae4-127">Select the **Create New** link and create a couple *to-do* items.</span></span> 

![New ASP.NET Project dialog box](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="19ae4-129">Test the **Edit**, **Details**, and **Delete** links.</span><span class="sxs-lookup"><span data-stu-id="19ae4-129">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="19ae4-130">The app uses a database context to connect with the database.</span><span class="sxs-lookup"><span data-stu-id="19ae4-130">The app uses a database context to connect with the database.</span></span> <span data-ttu-id="19ae4-131">In this sample, the database context uses a connection string named `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="19ae4-131">In this sample, the database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="19ae4-132">The connection string is set in the *Web.config* file and referenced in the *Models/MyDatabaseContext.cs* file.</span><span class="sxs-lookup"><span data-stu-id="19ae4-132">The connection string is set in the *Web.config* file and referenced in the *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="19ae4-133">The connection string name is used later in the tutorial to connect the Azure web app to an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="19ae4-133">The connection string name is used later in the tutorial to connect the Azure web app to an Azure SQL Database.</span></span> 

## <a name="publish-to-azure-with-sql-database"></a><span data-ttu-id="19ae4-134">Publish to Azure with SQL Database</span><span class="sxs-lookup"><span data-stu-id="19ae4-134">Publish to Azure with SQL Database</span></span>

<span data-ttu-id="19ae4-135">In the **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-135">In the **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Publish from Solution Explorer](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="19ae4-137">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-137">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Publish from project overview page](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="19ae4-139">Publishing opens the **Create App Service** dialog, which helps you create all the Azure resources you need to run your ASP.NET web app in Azure.</span><span class="sxs-lookup"><span data-stu-id="19ae4-139">Publishing opens the **Create App Service** dialog, which helps you create all the Azure resources you need to run your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="19ae4-140">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="19ae4-140">Sign in to Azure</span></span>

<span data-ttu-id="19ae4-141">In the **Create App Service** dialog, click **Add an account**, and then sign in to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="19ae4-141">In the **Create App Service** dialog, click **Add an account**, and then sign in to your Azure subscription.</span></span> <span data-ttu-id="19ae4-142">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="19ae4-142">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="19ae4-143">If the signed-in Microsoft account doesn't have your Azure subscription, click it to add the correct account.</span><span class="sxs-lookup"><span data-stu-id="19ae4-143">If the signed-in Microsoft account doesn't have your Azure subscription, click it to add the correct account.</span></span> 

> [!NOTE]
> <span data-ttu-id="19ae4-144">If you're already signed in, don't select **Create** yet.</span><span class="sxs-lookup"><span data-stu-id="19ae4-144">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Sign in to Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

### <a name="configure-the-web-app-name"></a><span data-ttu-id="19ae4-146">Configure the web app name</span><span class="sxs-lookup"><span data-stu-id="19ae4-146">Configure the web app name</span></span>

<span data-ttu-id="19ae4-147">You can keep the generated web app name, or change it to another unique name (valid characters are `a-z`, `0-9`, and `-`).</span><span class="sxs-lookup"><span data-stu-id="19ae4-147">You can keep the generated web app name, or change it to another unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="19ae4-148">The web app name is used as part of the default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span><span class="sxs-lookup"><span data-stu-id="19ae4-148">The web app name is used as part of the default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="19ae4-149">The web app name needs to be unique across all apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="19ae4-149">The web app name needs to be unique across all apps in Azure.</span></span> 

![Create app service dialog](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="19ae4-151">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="19ae4-151">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="19ae4-152">Next to **Resource Group**, click **New**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-152">Next to **Resource Group**, click **New**.</span></span>

![Next to Resource Group, click New.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="19ae4-154">Name the resource group **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-154">Name the resource group **myResourceGroup**.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="19ae4-155">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="19ae4-155">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="19ae4-156">Next to **App Service Plan**, click **New**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-156">Next to **App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="19ae4-157">In the **Configure App Service Plan** dialog, configure the new App Service plan with the following settings:</span><span class="sxs-lookup"><span data-stu-id="19ae4-157">In the **Configure App Service Plan** dialog, configure the new App Service plan with the following settings:</span></span>

![Create App Service plan](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="19ae4-159">Setting</span><span class="sxs-lookup"><span data-stu-id="19ae4-159">Setting</span></span>  | <span data-ttu-id="19ae4-160">Suggested value</span><span class="sxs-lookup"><span data-stu-id="19ae4-160">Suggested value</span></span> | <span data-ttu-id="19ae4-161">For more information</span><span class="sxs-lookup"><span data-stu-id="19ae4-161">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="19ae4-162">**App Service Plan**</span><span class="sxs-lookup"><span data-stu-id="19ae4-162">**App Service Plan**</span></span>| <span data-ttu-id="19ae4-163">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="19ae4-163">myAppServicePlan</span></span> | [<span data-ttu-id="19ae4-164">App Service plans</span><span class="sxs-lookup"><span data-stu-id="19ae4-164">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="19ae4-165">**Location**</span><span class="sxs-lookup"><span data-stu-id="19ae4-165">**Location**</span></span>| <span data-ttu-id="19ae4-166">West Europe</span><span class="sxs-lookup"><span data-stu-id="19ae4-166">West Europe</span></span> | [<span data-ttu-id="19ae4-167">Azure regions</span><span class="sxs-lookup"><span data-stu-id="19ae4-167">Azure regions</span></span>](https://azure.microsoft.com/regions/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) |
|<span data-ttu-id="19ae4-168">**Size**</span><span class="sxs-lookup"><span data-stu-id="19ae4-168">**Size**</span></span>| <span data-ttu-id="19ae4-169">Free</span><span class="sxs-lookup"><span data-stu-id="19ae4-169">Free</span></span> | [<span data-ttu-id="19ae4-170">Pricing tiers</span><span class="sxs-lookup"><span data-stu-id="19ae4-170">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="19ae4-171">Create a SQL Server instance</span><span class="sxs-lookup"><span data-stu-id="19ae4-171">Create a SQL Server instance</span></span>

<span data-ttu-id="19ae4-172">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="19ae4-172">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="19ae4-173">A logical server contains a group of databases managed as a group.</span><span class="sxs-lookup"><span data-stu-id="19ae4-173">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="19ae4-174">Click **Create a SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-174">Click **Create a SQL Database**.</span></span>

![Create a SQL Database](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="19ae4-176">In the **Configure SQL Database** dialog, click **New** next to **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-176">In the **Configure SQL Database** dialog, click **New** next to **SQL Server**.</span></span> 

<span data-ttu-id="19ae4-177">A unique server name is generated.</span><span class="sxs-lookup"><span data-stu-id="19ae4-177">A unique server name is generated.</span></span> <span data-ttu-id="19ae4-178">This name is used as part of the default URL for your logical server, `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="19ae4-178">This name is used as part of the default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="19ae4-179">It must be unique across all logical server instances in Azure.</span><span class="sxs-lookup"><span data-stu-id="19ae4-179">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="19ae4-180">You can change the server name, but for this tutorial, keep the generated value.</span><span class="sxs-lookup"><span data-stu-id="19ae4-180">You can change the server name, but for this tutorial, keep the generated value.</span></span>

<span data-ttu-id="19ae4-181">Add an administrator username and password.</span><span class="sxs-lookup"><span data-stu-id="19ae4-181">Add an administrator username and password.</span></span> <span data-ttu-id="19ae4-182">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="19ae4-182">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="19ae4-183">Remember this username and password.</span><span class="sxs-lookup"><span data-stu-id="19ae4-183">Remember this username and password.</span></span> <span data-ttu-id="19ae4-184">You need them to manage the logical server instance later.</span><span class="sxs-lookup"><span data-stu-id="19ae4-184">You need them to manage the logical server instance later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19ae4-185">Even though your password in the connection strings is masked (in Visual Studio and also in App Service), the fact that it's maintained somewhere adds to the attack surface of your app.</span><span class="sxs-lookup"><span data-stu-id="19ae4-185">Even though your password in the connection strings is masked (in Visual Studio and also in App Service), the fact that it's maintained somewhere adds to the attack surface of your app.</span></span> <span data-ttu-id="19ae4-186">App Service can use [managed service identities](app-service-managed-service-identity.md) to eliminate this risk by removing the need to maintain secrets in your code or app configuration at all.</span><span class="sxs-lookup"><span data-stu-id="19ae4-186">App Service can use [managed service identities](app-service-managed-service-identity.md) to eliminate this risk by removing the need to maintain secrets in your code or app configuration at all.</span></span> <span data-ttu-id="19ae4-187">For more information, see [Next steps](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="19ae4-187">For more information, see [Next steps](#next-steps).</span></span>

![Create SQL Server instance](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

<span data-ttu-id="19ae4-189">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-189">Click **OK**.</span></span> <span data-ttu-id="19ae4-190">Don't close the **Configure SQL Database** dialog yet.</span><span class="sxs-lookup"><span data-stu-id="19ae4-190">Don't close the **Configure SQL Database** dialog yet.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="19ae4-191">Create a SQL Database</span><span class="sxs-lookup"><span data-stu-id="19ae4-191">Create a SQL Database</span></span>

<span data-ttu-id="19ae4-192">In the **Configure SQL Database** dialog:</span><span class="sxs-lookup"><span data-stu-id="19ae4-192">In the **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="19ae4-193">Keep the default generated **Database Name**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-193">Keep the default generated **Database Name**.</span></span>
* <span data-ttu-id="19ae4-194">In **Connection String Name**, type *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="19ae4-194">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="19ae4-195">This name must match the connection string that is referenced in *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="19ae4-195">This name must match the connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="19ae4-196">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-196">Select **OK**.</span></span>

![Configure SQL Database](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="19ae4-198">The **Create App Service** dialog shows the resources you've configured.</span><span class="sxs-lookup"><span data-stu-id="19ae4-198">The **Create App Service** dialog shows the resources you've configured.</span></span> <span data-ttu-id="19ae4-199">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-199">Click **Create**.</span></span> 

![the resources you've created](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="19ae4-201">Once the wizard finishes creating the Azure resources, it  publishes your ASP.NET app to Azure.</span><span class="sxs-lookup"><span data-stu-id="19ae4-201">Once the wizard finishes creating the Azure resources, it  publishes your ASP.NET app to Azure.</span></span> <span data-ttu-id="19ae4-202">Your default browser is launched with the URL to the deployed app.</span><span class="sxs-lookup"><span data-stu-id="19ae4-202">Your default browser is launched with the URL to the deployed app.</span></span> 

<span data-ttu-id="19ae4-203">Add a few to-do items.</span><span class="sxs-lookup"><span data-stu-id="19ae4-203">Add a few to-do items.</span></span>

![Published ASP.NET application in Azure web app](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="19ae4-205">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="19ae4-205">Congratulations!</span></span> <span data-ttu-id="19ae4-206">Your data-driven ASP.NET application is running live in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="19ae4-206">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-the-sql-database-locally"></a><span data-ttu-id="19ae4-207">Access the SQL Database locally</span><span class="sxs-lookup"><span data-stu-id="19ae4-207">Access the SQL Database locally</span></span>

<span data-ttu-id="19ae4-208">Visual Studio lets you explore and manage your new SQL Database easily in the **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-208">Visual Studio lets you explore and manage your new SQL Database easily in the **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="19ae4-209">Create a database connection</span><span class="sxs-lookup"><span data-stu-id="19ae4-209">Create a database connection</span></span>

<span data-ttu-id="19ae4-210">From the **View** menu, select **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-210">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="19ae4-211">At the top of **SQL Server Object Explorer**, click the **Add SQL Server** button.</span><span class="sxs-lookup"><span data-stu-id="19ae4-211">At the top of **SQL Server Object Explorer**, click the **Add SQL Server** button.</span></span>

### <a name="configure-the-database-connection"></a><span data-ttu-id="19ae4-212">Configure the database connection</span><span class="sxs-lookup"><span data-stu-id="19ae4-212">Configure the database connection</span></span>

<span data-ttu-id="19ae4-213">In the **Connect** dialog, expand the **Azure** node.</span><span class="sxs-lookup"><span data-stu-id="19ae4-213">In the **Connect** dialog, expand the **Azure** node.</span></span> <span data-ttu-id="19ae4-214">All your SQL Database instances in Azure are listed here.</span><span class="sxs-lookup"><span data-stu-id="19ae4-214">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="19ae4-215">Select the SQL Database that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="19ae4-215">Select the SQL Database that you created earlier.</span></span> <span data-ttu-id="19ae4-216">The connection you created earlier is automatically filled at the bottom.</span><span class="sxs-lookup"><span data-stu-id="19ae4-216">The connection you created earlier is automatically filled at the bottom.</span></span>

<span data-ttu-id="19ae4-217">Type the database administrator password you created earlier and click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-217">Type the database administrator password you created earlier and click **Connect**.</span></span>

![Configure database connection from Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="19ae4-219">Allow client connection from your computer</span><span class="sxs-lookup"><span data-stu-id="19ae4-219">Allow client connection from your computer</span></span>

<span data-ttu-id="19ae4-220">The **Create a new firewall rule** dialog is opened.</span><span class="sxs-lookup"><span data-stu-id="19ae4-220">The **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="19ae4-221">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="19ae4-221">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="19ae4-222">To connect to your database, create a firewall rule in the SQL Database instance.</span><span class="sxs-lookup"><span data-stu-id="19ae4-222">To connect to your database, create a firewall rule in the SQL Database instance.</span></span> <span data-ttu-id="19ae4-223">The firewall rule allows the public IP address of your local computer.</span><span class="sxs-lookup"><span data-stu-id="19ae4-223">The firewall rule allows the public IP address of your local computer.</span></span>

<span data-ttu-id="19ae4-224">The dialog is already filled with your computer's public IP address.</span><span class="sxs-lookup"><span data-stu-id="19ae4-224">The dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="19ae4-225">Make sure that **Add my client IP** is selected and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-225">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Set firewall for SQL Database instance](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="19ae4-227">Once Visual Studio finishes creating the firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-227">Once Visual Studio finishes creating the firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="19ae4-228">Here, you can perform the most common database operations, such as run queries, create views and stored procedures, and more.</span><span class="sxs-lookup"><span data-stu-id="19ae4-228">Here, you can perform the most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="19ae4-229">Expand your connection > **Databases** > **&lt;your database>** > **Tables**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-229">Expand your connection > **Databases** > **&lt;your database>** > **Tables**.</span></span> <span data-ttu-id="19ae4-230">Right-click on the `Todoes` table and select **View Data**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-230">Right-click on the `Todoes` table and select **View Data**.</span></span> 

![Explore SQL Database objects](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="19ae4-232">Update app with Code First Migrations</span><span class="sxs-lookup"><span data-stu-id="19ae4-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="19ae4-233">You can use the familiar tools in Visual Studio to update your database and web app in Azure.</span><span class="sxs-lookup"><span data-stu-id="19ae4-233">You can use the familiar tools in Visual Studio to update your database and web app in Azure.</span></span> <span data-ttu-id="19ae4-234">In this step, you use Code First Migrations in Entity Framework to make a change to your database schema and publish it to Azure.</span><span class="sxs-lookup"><span data-stu-id="19ae4-234">In this step, you use Code First Migrations in Entity Framework to make a change to your database schema and publish it to Azure.</span></span>

<span data-ttu-id="19ae4-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="19ae4-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="19ae4-236">Update your data model</span><span class="sxs-lookup"><span data-stu-id="19ae4-236">Update your data model</span></span>

<span data-ttu-id="19ae4-237">Open _Models\Todo.cs_ in the code editor.</span><span class="sxs-lookup"><span data-stu-id="19ae4-237">Open _Models\Todo.cs_ in the code editor.</span></span> <span data-ttu-id="19ae4-238">Add the following property to the `ToDo` class:</span><span class="sxs-lookup"><span data-stu-id="19ae4-238">Add the following property to the `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="19ae4-239">Run Code First Migrations locally</span><span class="sxs-lookup"><span data-stu-id="19ae4-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="19ae4-240">Run a few commands to make updates to your local database.</span><span class="sxs-lookup"><span data-stu-id="19ae4-240">Run a few commands to make updates to your local database.</span></span> 

<span data-ttu-id="19ae4-241">From the **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-241">From the **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="19ae4-242">In the Package Manager Console window, enable Code First Migrations:</span><span class="sxs-lookup"><span data-stu-id="19ae4-242">In the Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="19ae4-243">Add a migration:</span><span class="sxs-lookup"><span data-stu-id="19ae4-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="19ae4-244">Update the local database:</span><span class="sxs-lookup"><span data-stu-id="19ae4-244">Update the local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="19ae4-245">Type `Ctrl+F5` to run the app.</span><span class="sxs-lookup"><span data-stu-id="19ae4-245">Type `Ctrl+F5` to run the app.</span></span> <span data-ttu-id="19ae4-246">Test the edit, details, and create links.</span><span class="sxs-lookup"><span data-stu-id="19ae4-246">Test the edit, details, and create links.</span></span>

<span data-ttu-id="19ae4-247">If the application loads without errors, then Code First Migrations has succeeded.</span><span class="sxs-lookup"><span data-stu-id="19ae4-247">If the application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="19ae4-248">However, your page still looks the same because your application logic is not using this new property yet.</span><span class="sxs-lookup"><span data-stu-id="19ae4-248">However, your page still looks the same because your application logic is not using this new property yet.</span></span> 

### <a name="use-the-new-property"></a><span data-ttu-id="19ae4-249">Use the new property</span><span class="sxs-lookup"><span data-stu-id="19ae4-249">Use the new property</span></span>

<span data-ttu-id="19ae4-250">Make some changes in your code to use the `Done` property.</span><span class="sxs-lookup"><span data-stu-id="19ae4-250">Make some changes in your code to use the `Done` property.</span></span> <span data-ttu-id="19ae4-251">For simplicity in this tutorial, you're only going to change the `Index` and `Create` views to see the property in action.</span><span class="sxs-lookup"><span data-stu-id="19ae4-251">For simplicity in this tutorial, you're only going to change the `Index` and `Create` views to see the property in action.</span></span>

<span data-ttu-id="19ae4-252">Open _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="19ae4-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="19ae4-253">Find the `Create()` method on line 52 and add `Done` to the list of properties in the `Bind` attribute.</span><span class="sxs-lookup"><span data-stu-id="19ae4-253">Find the `Create()` method on line 52 and add `Done` to the list of properties in the `Bind` attribute.</span></span> <span data-ttu-id="19ae4-254">When you're done, your `Create()` method signature looks like the following code:</span><span class="sxs-lookup"><span data-stu-id="19ae4-254">When you're done, your `Create()` method signature looks like the following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="19ae4-255">Open _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="19ae4-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="19ae4-256">In the Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="19ae4-256">In the Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="19ae4-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="19ae4-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

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

<span data-ttu-id="19ae4-258">Open _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="19ae4-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="19ae4-259">Search for the empty `<th></th>` element.</span><span class="sxs-lookup"><span data-stu-id="19ae4-259">Search for the empty `<th></th>` element.</span></span> <span data-ttu-id="19ae4-260">Just above this element, add the following Razor code:</span><span class="sxs-lookup"><span data-stu-id="19ae4-260">Just above this element, add the following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="19ae4-261">Find the `<td>` element that contains the `Html.ActionLink()` helper methods.</span><span class="sxs-lookup"><span data-stu-id="19ae4-261">Find the `<td>` element that contains the `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="19ae4-262">_Above_ this `<td>`, add another `<td>` element with the following Razor code:</span><span class="sxs-lookup"><span data-stu-id="19ae4-262">_Above_ this `<td>`, add another `<td>` element with the following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="19ae4-263">That's all you need to see the changes in the `Index` and `Create` views.</span><span class="sxs-lookup"><span data-stu-id="19ae4-263">That's all you need to see the changes in the `Index` and `Create` views.</span></span> 

<span data-ttu-id="19ae4-264">Type `Ctrl+F5` to run the app.</span><span class="sxs-lookup"><span data-stu-id="19ae4-264">Type `Ctrl+F5` to run the app.</span></span>

<span data-ttu-id="19ae4-265">You can now add a to-do item and check **Done**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="19ae4-266">Then it should show up in your homepage as a completed item.</span><span class="sxs-lookup"><span data-stu-id="19ae4-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="19ae4-267">Remember that the `Edit` view doesn't show the `Done` field, because you didn't change the `Edit` view.</span><span class="sxs-lookup"><span data-stu-id="19ae4-267">Remember that the `Edit` view doesn't show the `Done` field, because you didn't change the `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="19ae4-268">Enable Code First Migrations in Azure</span><span class="sxs-lookup"><span data-stu-id="19ae4-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="19ae4-269">Now that your code change works, including database migration, you publish it to your Azure web app and update your SQL Database with Code First Migrations too.</span><span class="sxs-lookup"><span data-stu-id="19ae4-269">Now that your code change works, including database migration, you publish it to your Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="19ae4-270">Just like before, right-click your project and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="19ae4-271">Click **Configure** to open the publish settings.</span><span class="sxs-lookup"><span data-stu-id="19ae4-271">Click **Configure** to open the publish settings.</span></span>

![Open publish settings](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="19ae4-273">In the wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-273">In the wizard, click **Next**.</span></span>

<span data-ttu-id="19ae4-274">Make sure that the connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-274">Make sure that the connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="19ae4-275">You may need to select the **myToDoAppDb** database from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="19ae4-275">You may need to select the **myToDoAppDb** database from the dropdown.</span></span> 

<span data-ttu-id="19ae4-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Enable Code First Migrations in Azure web app](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="19ae4-278">Publish your changes</span><span class="sxs-lookup"><span data-stu-id="19ae4-278">Publish your changes</span></span>

<span data-ttu-id="19ae4-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span><span class="sxs-lookup"><span data-stu-id="19ae4-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="19ae4-280">In the publish page, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-280">In the publish page, click **Publish**.</span></span>

<span data-ttu-id="19ae4-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span><span class="sxs-lookup"><span data-stu-id="19ae4-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Azure web app after Code First Migration](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="19ae4-283">All your existing to-do items are still displayed.</span><span class="sxs-lookup"><span data-stu-id="19ae4-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="19ae4-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span><span class="sxs-lookup"><span data-stu-id="19ae4-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="19ae4-285">Also, Code First Migrations only changes the data schema and leaves your existing data intact.</span><span class="sxs-lookup"><span data-stu-id="19ae4-285">Also, Code First Migrations only changes the data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="19ae4-286">Stream application logs</span><span class="sxs-lookup"><span data-stu-id="19ae4-286">Stream application logs</span></span>

<span data-ttu-id="19ae4-287">You can stream tracing messages directly from your Azure web app to Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19ae4-287">You can stream tracing messages directly from your Azure web app to Visual Studio.</span></span>

<span data-ttu-id="19ae4-288">Open _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="19ae4-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="19ae4-289">Each action starts with a `Trace.WriteLine()` method.</span><span class="sxs-lookup"><span data-stu-id="19ae4-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="19ae4-290">This code is added to show you how to add trace messages to your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="19ae4-290">This code is added to show you how to add trace messages to your Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="19ae4-291">Open Server Explorer</span><span class="sxs-lookup"><span data-stu-id="19ae4-291">Open Server Explorer</span></span>

<span data-ttu-id="19ae4-292">From the **View** menu, select **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-292">From the **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="19ae4-293">You can configure logging for your Azure web app in **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="19ae4-294">Enable log streaming</span><span class="sxs-lookup"><span data-stu-id="19ae4-294">Enable log streaming</span></span>

<span data-ttu-id="19ae4-295">In **Server Explorer**, expand **Azure** > **App Service**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="19ae4-296">Expand the **myResourceGroup** resource group, you created when you first created the Azure web app.</span><span class="sxs-lookup"><span data-stu-id="19ae4-296">Expand the **myResourceGroup** resource group, you created when you first created the Azure web app.</span></span>

<span data-ttu-id="19ae4-297">Right-click your Azure web app and select **View Streaming Logs**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Enable log streaming](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="19ae4-299">The logs are now streamed into the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="19ae4-299">The logs are now streamed into the **Output** window.</span></span> 

![Log streaming in Output window](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="19ae4-301">However, you don't see any of the trace messages yet.</span><span class="sxs-lookup"><span data-stu-id="19ae4-301">However, you don't see any of the trace messages yet.</span></span> <span data-ttu-id="19ae4-302">That's because when you first select **View Streaming Logs**, your Azure web app sets the trace level to `Error`, which only logs error events (with the `Trace.TraceError()` method).</span><span class="sxs-lookup"><span data-stu-id="19ae4-302">That's because when you first select **View Streaming Logs**, your Azure web app sets the trace level to `Error`, which only logs error events (with the `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="19ae4-303">Change trace levels</span><span class="sxs-lookup"><span data-stu-id="19ae4-303">Change trace levels</span></span>

<span data-ttu-id="19ae4-304">To change the trace levels to output other trace messages, go back to **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-304">To change the trace levels to output other trace messages, go back to **Server Explorer**.</span></span>

<span data-ttu-id="19ae4-305">Right-click your Azure web app again and select **View Settings**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-305">Right-click your Azure web app again and select **View Settings**.</span></span>

<span data-ttu-id="19ae4-306">In the **Application Logging (File System)** dropdown, select **Verbose**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-306">In the **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="19ae4-307">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-307">Click **Save**.</span></span>

![Change trace level to Verbose](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="19ae4-309">You can experiment with different trace levels to see what types of messages are displayed for each level.</span><span class="sxs-lookup"><span data-stu-id="19ae4-309">You can experiment with different trace levels to see what types of messages are displayed for each level.</span></span> <span data-ttu-id="19ae4-310">For example, the **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="19ae4-310">For example, the **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="19ae4-311">In your browser navigate to your web app again at *http://&lt;your app name>.azurewebsites.net*, then try clicking around the to-do list application in Azure.</span><span class="sxs-lookup"><span data-stu-id="19ae4-311">In your browser navigate to your web app again at *http://&lt;your app name>.azurewebsites.net*, then try clicking around the to-do list application in Azure.</span></span> <span data-ttu-id="19ae4-312">The trace messages are now streamed to the **Output** window in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19ae4-312">The trace messages are now streamed to the **Output** window in Visual Studio.</span></span>

```console
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="19ae4-313">Stop log streaming</span><span class="sxs-lookup"><span data-stu-id="19ae4-313">Stop log streaming</span></span>

<span data-ttu-id="19ae4-314">To stop the log-streaming service, click the **Stop monitoring** button in the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="19ae4-314">To stop the log-streaming service, click the **Stop monitoring** button in the **Output** window.</span></span>

![Stop log streaming](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="19ae4-316">Manage your Azure web app</span><span class="sxs-lookup"><span data-stu-id="19ae4-316">Manage your Azure web app</span></span>

<span data-ttu-id="19ae4-317">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span><span class="sxs-lookup"><span data-stu-id="19ae4-317">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span> 



<span data-ttu-id="19ae4-318">From the left menu, click **App Service**, then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="19ae4-318">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="19ae4-320">You have landed in your web app's page.</span><span class="sxs-lookup"><span data-stu-id="19ae4-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="19ae4-321">By default, the portal shows the **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="19ae4-321">By default, the portal shows the **Overview** page.</span></span> <span data-ttu-id="19ae4-322">This page gives you a view of how your app is doing.</span><span class="sxs-lookup"><span data-stu-id="19ae4-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="19ae4-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="19ae4-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="19ae4-324">The tabs on the left side of the page show the different configuration pages you can open.</span><span class="sxs-lookup"><span data-stu-id="19ae4-324">The tabs on the left side of the page show the different configuration pages you can open.</span></span> 

![App Service page in Azure portal](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="19ae4-326">Next steps</span><span class="sxs-lookup"><span data-stu-id="19ae4-326">Next steps</span></span>

<span data-ttu-id="19ae4-327">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="19ae4-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="19ae4-328">Create a SQL Database in Azure</span><span class="sxs-lookup"><span data-stu-id="19ae4-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="19ae4-329">Connect an ASP.NET app to SQL Database</span><span class="sxs-lookup"><span data-stu-id="19ae4-329">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="19ae4-330">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="19ae4-330">Deploy the app to Azure</span></span>
> * <span data-ttu-id="19ae4-331">Update the data model and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="19ae4-331">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="19ae4-332">Stream logs from Azure to your terminal</span><span class="sxs-lookup"><span data-stu-id="19ae4-332">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="19ae4-333">Manage the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="19ae4-333">Manage the app in the Azure portal</span></span>

<span data-ttu-id="19ae4-334">Advance to the next tutorial to learn how to easily improve the security of your connection Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="19ae4-334">Advance to the next tutorial to learn how to easily improve the security of your connection Azure SQL Database.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="19ae4-335">Access SQL Database securely using managed service identity</span><span class="sxs-lookup"><span data-stu-id="19ae4-335">Access SQL Database securely using managed service identity</span></span>](app-service-web-tutorial-connect-msi.md)
