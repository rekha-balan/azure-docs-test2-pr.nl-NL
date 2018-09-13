---
title: Build a .NET Core and SQL Database web app in Azure App Service | Microsoft Docs
description: Learn how to get a .NET Core app working in Azure App Service, with connection to a SQL Database.
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: syntaxc4
editor: ''
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: tutorial
ms.date: 04/11/2018
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: f870902e5bd5ef92d12d1e5e846696c4b26362a3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868411"
---
# <a name="tutorial-build-a-net-core-and-sql-database-web-app-in-azure-app-service"></a><span data-ttu-id="3a635-103">Tutorial: Build a .NET Core and SQL Database web app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3a635-103">Tutorial: Build a .NET Core and SQL Database web app in Azure App Service</span></span>

> [!NOTE]
> <span data-ttu-id="3a635-104">This article deploys an app to App Service on Windows.</span><span class="sxs-lookup"><span data-stu-id="3a635-104">This article deploys an app to App Service on Windows.</span></span> <span data-ttu-id="3a635-105">To deploy to App Service on _Linux_, see [Build a .NET Core and SQL Database web app in Azure App Service on Linux](./containers/tutorial-dotnetcore-sqldb-app.md).</span><span class="sxs-lookup"><span data-stu-id="3a635-105">To deploy to App Service on _Linux_, see [Build a .NET Core and SQL Database web app in Azure App Service on Linux](./containers/tutorial-dotnetcore-sqldb-app.md).</span></span>
>

<span data-ttu-id="3a635-106">[App Service](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service in Azure.</span><span class="sxs-lookup"><span data-stu-id="3a635-106">[App Service](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service in Azure.</span></span> <span data-ttu-id="3a635-107">This tutorial shows how to create a .NET Core web app and connect it to a SQL Database.</span><span class="sxs-lookup"><span data-stu-id="3a635-107">This tutorial shows how to create a .NET Core web app and connect it to a SQL Database.</span></span> <span data-ttu-id="3a635-108">When you're done, you'll have a .NET Core MVC app running in App Service.</span><span class="sxs-lookup"><span data-stu-id="3a635-108">When you're done, you'll have a .NET Core MVC app running in App Service.</span></span>

![app running in App Service](./media/app-service-web-tutorial-dotnetcore-sqldb/azure-app-in-browser.png)

<span data-ttu-id="3a635-110">What you learn how to:</span><span class="sxs-lookup"><span data-stu-id="3a635-110">What you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3a635-111">Create a SQL Database in Azure</span><span class="sxs-lookup"><span data-stu-id="3a635-111">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="3a635-112">Connect a .NET Core app to SQL Database</span><span class="sxs-lookup"><span data-stu-id="3a635-112">Connect a .NET Core app to SQL Database</span></span>
> * <span data-ttu-id="3a635-113">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="3a635-113">Deploy the app to Azure</span></span>
> * <span data-ttu-id="3a635-114">Update the data model and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="3a635-114">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="3a635-115">Stream diagnostic logs from Azure</span><span class="sxs-lookup"><span data-stu-id="3a635-115">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="3a635-116">Manage the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3a635-116">Manage the app in the Azure portal</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="3a635-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3a635-117">Prerequisites</span></span>

<span data-ttu-id="3a635-118">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="3a635-118">To complete this tutorial:</span></span>

* [<span data-ttu-id="3a635-119">Install Git</span><span class="sxs-lookup"><span data-stu-id="3a635-119">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="3a635-120">Install .NET Core</span><span class="sxs-lookup"><span data-stu-id="3a635-120">Install .NET Core</span></span>](https://www.microsoft.com/net/core/)

## <a name="create-local-net-core-app"></a><span data-ttu-id="3a635-121">Create local .NET Core app</span><span class="sxs-lookup"><span data-stu-id="3a635-121">Create local .NET Core app</span></span>

<span data-ttu-id="3a635-122">In this step, you set up the local .NET Core project.</span><span class="sxs-lookup"><span data-stu-id="3a635-122">In this step, you set up the local .NET Core project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="3a635-123">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="3a635-123">Clone the sample application</span></span>

<span data-ttu-id="3a635-124">In the terminal window, `cd` to a working directory.</span><span class="sxs-lookup"><span data-stu-id="3a635-124">In the terminal window, `cd` to a working directory.</span></span>

<span data-ttu-id="3a635-125">Run the following commands to clone the sample repository and change to its root.</span><span class="sxs-lookup"><span data-stu-id="3a635-125">Run the following commands to clone the sample repository and change to its root.</span></span>

```bash
git clone https://github.com/azure-samples/dotnetcore-sqldb-tutorial
cd dotnetcore-sqldb-tutorial
```

<span data-ttu-id="3a635-126">The sample project contains a basic CRUD (create-read-update-delete) app using [Entity Framework Core](https://docs.microsoft.com/ef/core/).</span><span class="sxs-lookup"><span data-stu-id="3a635-126">The sample project contains a basic CRUD (create-read-update-delete) app using [Entity Framework Core](https://docs.microsoft.com/ef/core/).</span></span>

### <a name="run-the-application"></a><span data-ttu-id="3a635-127">Run the application</span><span class="sxs-lookup"><span data-stu-id="3a635-127">Run the application</span></span>

<span data-ttu-id="3a635-128">Run the following commands to install the required packages, run database migrations, and start the application.</span><span class="sxs-lookup"><span data-stu-id="3a635-128">Run the following commands to install the required packages, run database migrations, and start the application.</span></span>

```bash
dotnet restore
dotnet ef database update
dotnet run
```

<span data-ttu-id="3a635-129">Navigate to `http://localhost:5000` in a browser.</span><span class="sxs-lookup"><span data-stu-id="3a635-129">Navigate to `http://localhost:5000` in a browser.</span></span> <span data-ttu-id="3a635-130">Select the **Create New** link and create a couple _to-do_ items.</span><span class="sxs-lookup"><span data-stu-id="3a635-130">Select the **Create New** link and create a couple _to-do_ items.</span></span>

![connects successfully to SQL Database](./media/app-service-web-tutorial-dotnetcore-sqldb/local-app-in-browser.png)

<span data-ttu-id="3a635-132">To stop .NET Core at any time, press `Ctrl+C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="3a635-132">To stop .NET Core at any time, press `Ctrl+C` in the terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-production-sql-database"></a><span data-ttu-id="3a635-133">Create production SQL Database</span><span class="sxs-lookup"><span data-stu-id="3a635-133">Create production SQL Database</span></span>

<span data-ttu-id="3a635-134">In this step, you create a SQL Database in Azure.</span><span class="sxs-lookup"><span data-stu-id="3a635-134">In this step, you create a SQL Database in Azure.</span></span> <span data-ttu-id="3a635-135">When your app is deployed to Azure, it uses this cloud database.</span><span class="sxs-lookup"><span data-stu-id="3a635-135">When your app is deployed to Azure, it uses this cloud database.</span></span>

<span data-ttu-id="3a635-136">For SQL Database, this tutorial uses [Azure SQL Database](/azure/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="3a635-136">For SQL Database, this tutorial uses [Azure SQL Database](/azure/sql-database/).</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="3a635-137">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="3a635-137">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)]

### <a name="create-a-sql-database-logical-server"></a><span data-ttu-id="3a635-138">Create a SQL Database logical server</span><span class="sxs-lookup"><span data-stu-id="3a635-138">Create a SQL Database logical server</span></span>

<span data-ttu-id="3a635-139">In the Cloud Shell, create a SQL Database logical server with the [`az sql server create`](/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-create) command.</span><span class="sxs-lookup"><span data-stu-id="3a635-139">In the Cloud Shell, create a SQL Database logical server with the [`az sql server create`](/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-create) command.</span></span>

<span data-ttu-id="3a635-140">Replace the *\<server_name>* placeholder with a unique SQL Database name.</span><span class="sxs-lookup"><span data-stu-id="3a635-140">Replace the *\<server_name>* placeholder with a unique SQL Database name.</span></span> <span data-ttu-id="3a635-141">This name is used as the part of the SQL Database endpoint, `<server_name>.database.windows.net`, so the name needs to be unique across all logical servers in Azure.</span><span class="sxs-lookup"><span data-stu-id="3a635-141">This name is used as the part of the SQL Database endpoint, `<server_name>.database.windows.net`, so the name needs to be unique across all logical servers in Azure.</span></span> <span data-ttu-id="3a635-142">The name must contain only lowercase letters, numbers, and the hyphen (-) character, and must be between 3 and 50 characters long.</span><span class="sxs-lookup"><span data-stu-id="3a635-142">The name must contain only lowercase letters, numbers, and the hyphen (-) character, and must be between 3 and 50 characters long.</span></span> <span data-ttu-id="3a635-143">Also, replace *\<db_username>* and *\<db_password>* with a username and password of your choice.</span><span class="sxs-lookup"><span data-stu-id="3a635-143">Also, replace *\<db_username>* and *\<db_password>* with a username and password of your choice.</span></span> 


```azurecli-interactive
az sql server create --name <server_name> --resource-group myResourceGroup --location "West Europe" --admin-user <db_username> --admin-password <db_password>
```

<span data-ttu-id="3a635-144">When the SQL Database logical server is created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="3a635-144">When the SQL Database logical server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "sqladmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Sql/servers/<server_name>",
  "identity": null,
  "kind": "v12.0",
  "location": "westeurope",
  "name": "<server_name>",
  "resourceGroup": "myResourceGroup",
  "state": "Ready",
  "tags": null,
  "type": "Microsoft.Sql/servers",
  "version": "12.0"
}
```

### <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="3a635-145">Configure a server firewall rule</span><span class="sxs-lookup"><span data-stu-id="3a635-145">Configure a server firewall rule</span></span>

<span data-ttu-id="3a635-146">Create an [Azure SQL Database server-level firewall rule](../sql-database/sql-database-firewall-configure.md) using the [`az sql server firewall create`](/cli/azure/sql/server/firewall-rule?view=azure-cli-latest#az-sql-server-firewall-rule-create) command.</span><span class="sxs-lookup"><span data-stu-id="3a635-146">Create an [Azure SQL Database server-level firewall rule](../sql-database/sql-database-firewall-configure.md) using the [`az sql server firewall create`](/cli/azure/sql/server/firewall-rule?view=azure-cli-latest#az-sql-server-firewall-rule-create) command.</span></span> <span data-ttu-id="3a635-147">When both starting IP and end IP are set to 0.0.0.0, the firewall is only opened for other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="3a635-147">When both starting IP and end IP are set to 0.0.0.0, the firewall is only opened for other Azure resources.</span></span> 

```azurecli-interactive
az sql server firewall-rule create --resource-group myResourceGroup --server <server_name> --name AllowYourIp --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP] 
> <span data-ttu-id="3a635-148">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](app-service-ip-addresses.md#find-outbound-ips).</span><span class="sxs-lookup"><span data-stu-id="3a635-148">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](app-service-ip-addresses.md#find-outbound-ips).</span></span>
>

### <a name="create-a-database"></a><span data-ttu-id="3a635-149">Create a database</span><span class="sxs-lookup"><span data-stu-id="3a635-149">Create a database</span></span>

<span data-ttu-id="3a635-150">Create a database with an [S0 performance level](../sql-database/sql-database-service-tiers-dtu.md) in the server using the [`az sql db create`](/cli/azure/sql/db?view=azure-cli-latest#az-sql-db-create) command.</span><span class="sxs-lookup"><span data-stu-id="3a635-150">Create a database with an [S0 performance level](../sql-database/sql-database-service-tiers-dtu.md) in the server using the [`az sql db create`](/cli/azure/sql/db?view=azure-cli-latest#az-sql-db-create) command.</span></span>

```azurecli-interactive
az sql db create --resource-group myResourceGroup --server <server_name> --name coreDB --service-objective S0
```

### <a name="create-connection-string"></a><span data-ttu-id="3a635-151">Create connection string</span><span class="sxs-lookup"><span data-stu-id="3a635-151">Create connection string</span></span>

<span data-ttu-id="3a635-152">Replace the following string with the *\<server_name>*, *\<db_username>*, and *\<db_password>* you used earlier.</span><span class="sxs-lookup"><span data-stu-id="3a635-152">Replace the following string with the *\<server_name>*, *\<db_username>*, and *\<db_password>* you used earlier.</span></span>

```
Server=tcp:<server_name>.database.windows.net,1433;Database=coreDB;User ID=<db_username>;Password=<db_password>;Encrypt=true;Connection Timeout=30;
```

<span data-ttu-id="3a635-153">This is the connection string for your .NET Core app.</span><span class="sxs-lookup"><span data-stu-id="3a635-153">This is the connection string for your .NET Core app.</span></span> <span data-ttu-id="3a635-154">Copy it for use later.</span><span class="sxs-lookup"><span data-stu-id="3a635-154">Copy it for use later.</span></span>

## <a name="deploy-app-to-azure"></a><span data-ttu-id="3a635-155">Deploy app to Azure</span><span class="sxs-lookup"><span data-stu-id="3a635-155">Deploy app to Azure</span></span>

<span data-ttu-id="3a635-156">In this step, you deploy your SQL Database-connected .NET Core application to App Service.</span><span class="sxs-lookup"><span data-stu-id="3a635-156">In this step, you deploy your SQL Database-connected .NET Core application to App Service.</span></span>

### <a name="configure-local-git-deployment"></a><span data-ttu-id="3a635-157">Configure local git deployment</span><span class="sxs-lookup"><span data-stu-id="3a635-157">Configure local git deployment</span></span>

[!INCLUDE [Configure a deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="create-an-app-service-plan"></a><span data-ttu-id="3a635-158">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="3a635-158">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="3a635-159">Create a web app</span><span class="sxs-lookup"><span data-stu-id="3a635-159">Create a web app</span></span>

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app-dotnetcore-win-no-h.md)] 

### <a name="configure-an-environment-variable"></a><span data-ttu-id="3a635-160">Configure an environment variable</span><span class="sxs-lookup"><span data-stu-id="3a635-160">Configure an environment variable</span></span>

<span data-ttu-id="3a635-161">To set connection strings for your Azure app, use the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="3a635-161">To set connection strings for your Azure app, use the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in the Cloud Shell.</span></span> <span data-ttu-id="3a635-162">In the following command, replace *\<app name>*, as well as the *\<connection_string>* parameter with the connection string you created earlier.</span><span class="sxs-lookup"><span data-stu-id="3a635-162">In the following command, replace *\<app name>*, as well as the *\<connection_string>* parameter with the connection string you created earlier.</span></span>

```azurecli-interactive
az webapp config connection-string set --resource-group myResourceGroup --name <app name> --settings MyDbConnection='<connection_string>' --connection-string-type SQLServer
```

<span data-ttu-id="3a635-163">Next, set `ASPNETCORE_ENVIRONMENT` app setting to _Production_.</span><span class="sxs-lookup"><span data-stu-id="3a635-163">Next, set `ASPNETCORE_ENVIRONMENT` app setting to _Production_.</span></span> <span data-ttu-id="3a635-164">This setting lets you know whether you are running in Azure, because you use SQLite for your local development environment and SQL Database for your Azure environment.</span><span class="sxs-lookup"><span data-stu-id="3a635-164">This setting lets you know whether you are running in Azure, because you use SQLite for your local development environment and SQL Database for your Azure environment.</span></span>

<span data-ttu-id="3a635-165">The following example configures a `ASPNETCORE_ENVIRONMENT` app setting in your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="3a635-165">The following example configures a `ASPNETCORE_ENVIRONMENT` app setting in your Azure web app.</span></span> <span data-ttu-id="3a635-166">Replace the *\<app_name>* placeholder.</span><span class="sxs-lookup"><span data-stu-id="3a635-166">Replace the *\<app_name>* placeholder.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings ASPNETCORE_ENVIRONMENT="Production"
```

### <a name="connect-to-sql-database-in-production"></a><span data-ttu-id="3a635-167">Connect to SQL Database in production</span><span class="sxs-lookup"><span data-stu-id="3a635-167">Connect to SQL Database in production</span></span>

<span data-ttu-id="3a635-168">In your local repository, open Startup.cs and find the following code:</span><span class="sxs-lookup"><span data-stu-id="3a635-168">In your local repository, open Startup.cs and find the following code:</span></span>

```csharp
services.AddDbContext<MyDatabaseContext>(options =>
        options.UseSqlite("Data Source=localdatabase.db"));
```

<span data-ttu-id="3a635-169">Replace it with the following code, which uses the environment variables that you configured earlier.</span><span class="sxs-lookup"><span data-stu-id="3a635-169">Replace it with the following code, which uses the environment variables that you configured earlier.</span></span>

```csharp
// Use SQL Database if in Azure, otherwise, use SQLite
if(Environment.GetEnvironmentVariable("ASPNETCORE_ENVIRONMENT") == "Production")
    services.AddDbContext<MyDatabaseContext>(options =>
            options.UseSqlServer(Configuration.GetConnectionString("MyDbConnection")));
else
    services.AddDbContext<MyDatabaseContext>(options =>
            options.UseSqlite("Data Source=localdatabase.db"));

// Automatically perform database migration
services.BuildServiceProvider().GetService<MyDatabaseContext>().Database.Migrate();
```

<span data-ttu-id="3a635-170">If this code detects that it is running in production (which indicates the Azure environment), then it uses the connection string you configured to connect to the SQL Database.</span><span class="sxs-lookup"><span data-stu-id="3a635-170">If this code detects that it is running in production (which indicates the Azure environment), then it uses the connection string you configured to connect to the SQL Database.</span></span>

<span data-ttu-id="3a635-171">The `Database.Migrate()` call helps you when it is run in Azure, because it automatically creates the databases that your .NET Core app needs, based on its migration configuration.</span><span class="sxs-lookup"><span data-stu-id="3a635-171">The `Database.Migrate()` call helps you when it is run in Azure, because it automatically creates the databases that your .NET Core app needs, based on its migration configuration.</span></span> 

<span data-ttu-id="3a635-172">Save your changes, then commit it into your Git repository.</span><span class="sxs-lookup"><span data-stu-id="3a635-172">Save your changes, then commit it into your Git repository.</span></span> 

```bash
git add .
git commit -m "connect to SQLDB in Azure"
```

### <a name="push-to-azure-from-git"></a><span data-ttu-id="3a635-173">Push to Azure from Git</span><span class="sxs-lookup"><span data-stu-id="3a635-173">Push to Azure from Git</span></span>

[!INCLUDE [app-service-plan-no-h](../../includes/app-service-web-git-push-to-azure-no-h.md)]

```bash
Counting objects: 98, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (92/92), done.
Writing objects: 100% (98/98), 524.98 KiB | 5.58 MiB/s, done.
Total 98 (delta 8), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: .
remote: Updating submodules.
remote: Preparing deployment for commit id '0c497633b8'.
remote: Generating deployment script.
remote: Project file path: ./DotNetCoreSqlDb.csproj
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling ASP.NET Core Web Application deployment.
remote: .
remote: .
remote: .
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
remote: App container will begin restart within 10 seconds.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="3a635-174">Browse to the Azure web app</span><span class="sxs-lookup"><span data-stu-id="3a635-174">Browse to the Azure web app</span></span>

<span data-ttu-id="3a635-175">Browse to the deployed web app using your web browser.</span><span class="sxs-lookup"><span data-stu-id="3a635-175">Browse to the deployed web app using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="3a635-176">Add a few to-do items.</span><span class="sxs-lookup"><span data-stu-id="3a635-176">Add a few to-do items.</span></span>

![app running in App Service](./media/app-service-web-tutorial-dotnetcore-sqldb/azure-app-in-browser.png)

<span data-ttu-id="3a635-178">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="3a635-178">**Congratulations!**</span></span> <span data-ttu-id="3a635-179">You're running a data-driven .NET Core app in App Service.</span><span class="sxs-lookup"><span data-stu-id="3a635-179">You're running a data-driven .NET Core app in App Service.</span></span>

## <a name="update-locally-and-redeploy"></a><span data-ttu-id="3a635-180">Update locally and redeploy</span><span class="sxs-lookup"><span data-stu-id="3a635-180">Update locally and redeploy</span></span>

<span data-ttu-id="3a635-181">In this step, you make a change to your database schema and publish it to Azure.</span><span class="sxs-lookup"><span data-stu-id="3a635-181">In this step, you make a change to your database schema and publish it to Azure.</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="3a635-182">Update your data model</span><span class="sxs-lookup"><span data-stu-id="3a635-182">Update your data model</span></span>

<span data-ttu-id="3a635-183">Open _Models\Todo.cs_ in the code editor.</span><span class="sxs-lookup"><span data-stu-id="3a635-183">Open _Models\Todo.cs_ in the code editor.</span></span> <span data-ttu-id="3a635-184">Add the following property to the `ToDo` class:</span><span class="sxs-lookup"><span data-stu-id="3a635-184">Add the following property to the `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="3a635-185">Run Code First Migrations locally</span><span class="sxs-lookup"><span data-stu-id="3a635-185">Run Code First Migrations locally</span></span>

<span data-ttu-id="3a635-186">Run a few commands to make updates to your local database.</span><span class="sxs-lookup"><span data-stu-id="3a635-186">Run a few commands to make updates to your local database.</span></span>

```bash
dotnet ef migrations add AddProperty
```

<span data-ttu-id="3a635-187">Update the local database:</span><span class="sxs-lookup"><span data-stu-id="3a635-187">Update the local database:</span></span>

```bash
dotnet ef database update
```

### <a name="use-the-new-property"></a><span data-ttu-id="3a635-188">Use the new property</span><span class="sxs-lookup"><span data-stu-id="3a635-188">Use the new property</span></span>

<span data-ttu-id="3a635-189">Make some changes in your code to use the `Done` property.</span><span class="sxs-lookup"><span data-stu-id="3a635-189">Make some changes in your code to use the `Done` property.</span></span> <span data-ttu-id="3a635-190">For simplicity in this tutorial, you're only going to change the `Index` and `Create` views to see the property in action.</span><span class="sxs-lookup"><span data-stu-id="3a635-190">For simplicity in this tutorial, you're only going to change the `Index` and `Create` views to see the property in action.</span></span>

<span data-ttu-id="3a635-191">Open _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="3a635-191">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="3a635-192">Find the `Create([Bind("ID,Description,CreatedDate")] Todo todo)` method and add `Done` to the list of properties in the `Bind` attribute.</span><span class="sxs-lookup"><span data-stu-id="3a635-192">Find the `Create([Bind("ID,Description,CreatedDate")] Todo todo)` method and add `Done` to the list of properties in the `Bind` attribute.</span></span> <span data-ttu-id="3a635-193">When you're done, your `Create()` method signature looks like the following code:</span><span class="sxs-lookup"><span data-stu-id="3a635-193">When you're done, your `Create()` method signature looks like the following code:</span></span>

```csharp
public async Task<IActionResult> Create([Bind("ID,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="3a635-194">Open _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="3a635-194">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="3a635-195">In the Razor code, you should see a `<div class="form-group">` element for `Description`, and then another `<div class="form-group">` element for `CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="3a635-195">In the Razor code, you should see a `<div class="form-group">` element for `Description`, and then another `<div class="form-group">` element for `CreatedDate`.</span></span> <span data-ttu-id="3a635-196">Immediately following these two elements, add another `<div class="form-group">` element for `Done`:</span><span class="sxs-lookup"><span data-stu-id="3a635-196">Immediately following these two elements, add another `<div class="form-group">` element for `Done`:</span></span>

```csharp
<div class="form-group">
    <label asp-for="Done" class="col-md-2 control-label"></label>
    <div class="col-md-10">
        <input asp-for="Done" class="form-control" />
        <span asp-validation-for="Done" class="text-danger"></span>
    </div>
</div>
```

<span data-ttu-id="3a635-197">Open _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="3a635-197">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="3a635-198">Search for the empty `<th></th>` element.</span><span class="sxs-lookup"><span data-stu-id="3a635-198">Search for the empty `<th></th>` element.</span></span> <span data-ttu-id="3a635-199">Just above this element, add the following Razor code:</span><span class="sxs-lookup"><span data-stu-id="3a635-199">Just above this element, add the following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="3a635-200">Find the `<td>` element that contains the `asp-action` tag helpers.</span><span class="sxs-lookup"><span data-stu-id="3a635-200">Find the `<td>` element that contains the `asp-action` tag helpers.</span></span> <span data-ttu-id="3a635-201">Just above this element, add the following Razor code:</span><span class="sxs-lookup"><span data-stu-id="3a635-201">Just above this element, add the following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="3a635-202">That's all you need to see the changes in the `Index` and `Create` views.</span><span class="sxs-lookup"><span data-stu-id="3a635-202">That's all you need to see the changes in the `Index` and `Create` views.</span></span>

### <a name="test-your-changes-locally"></a><span data-ttu-id="3a635-203">Test your changes locally</span><span class="sxs-lookup"><span data-stu-id="3a635-203">Test your changes locally</span></span>

<span data-ttu-id="3a635-204">Run the app locally.</span><span class="sxs-lookup"><span data-stu-id="3a635-204">Run the app locally.</span></span>

```bash
dotnet run
```

<span data-ttu-id="3a635-205">In your browser, navigate to `http://localhost:5000/`.</span><span class="sxs-lookup"><span data-stu-id="3a635-205">In your browser, navigate to `http://localhost:5000/`.</span></span> <span data-ttu-id="3a635-206">You can now add a to-do item and check **Done**.</span><span class="sxs-lookup"><span data-stu-id="3a635-206">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="3a635-207">Then it should show up in your homepage as a completed item.</span><span class="sxs-lookup"><span data-stu-id="3a635-207">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="3a635-208">Remember that the `Edit` view doesn't show the `Done` field, because you didn't change the `Edit` view.</span><span class="sxs-lookup"><span data-stu-id="3a635-208">Remember that the `Edit` view doesn't show the `Done` field, because you didn't change the `Edit` view.</span></span>

### <a name="publish-changes-to-azure"></a><span data-ttu-id="3a635-209">Publish changes to Azure</span><span class="sxs-lookup"><span data-stu-id="3a635-209">Publish changes to Azure</span></span>

```bash
git add .
git commit -m "added done field"
git push azure master
```

<span data-ttu-id="3a635-210">Once the `git push` is complete, navigate to your Azure web app and try out the new functionality.</span><span class="sxs-lookup"><span data-stu-id="3a635-210">Once the `git push` is complete, navigate to your Azure web app and try out the new functionality.</span></span>

![Azure web app after Code First Migration](./media/app-service-web-tutorial-dotnetcore-sqldb/this-one-is-done.png)

<span data-ttu-id="3a635-212">All your existing to-do items are still displayed.</span><span class="sxs-lookup"><span data-stu-id="3a635-212">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="3a635-213">When you republish your .NET Core app, existing data in your SQL Database is not lost.</span><span class="sxs-lookup"><span data-stu-id="3a635-213">When you republish your .NET Core app, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="3a635-214">Also, Entity Framework Core Migrations only changes the data schema and leaves your existing data intact.</span><span class="sxs-lookup"><span data-stu-id="3a635-214">Also, Entity Framework Core Migrations only changes the data schema and leaves your existing data intact.</span></span>

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="3a635-215">Manage your Azure web app</span><span class="sxs-lookup"><span data-stu-id="3a635-215">Manage your Azure web app</span></span>

<span data-ttu-id="3a635-216">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span><span class="sxs-lookup"><span data-stu-id="3a635-216">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="3a635-217">From the left menu, click **App Services**, then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="3a635-217">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/app-service-web-tutorial-dotnetcore-sqldb/access-portal.png)

<span data-ttu-id="3a635-219">By default, the portal shows your web app's **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="3a635-219">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="3a635-220">This page gives you a view of how your app is doing.</span><span class="sxs-lookup"><span data-stu-id="3a635-220">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="3a635-221">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="3a635-221">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="3a635-222">The tabs on the left side of the page show the different configuration pages you can open.</span><span class="sxs-lookup"><span data-stu-id="3a635-222">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![App Service page in Azure portal](./media/app-service-web-tutorial-dotnetcore-sqldb/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="3a635-224">Next steps</span><span class="sxs-lookup"><span data-stu-id="3a635-224">Next steps</span></span>

<span data-ttu-id="3a635-225">What you learned:</span><span class="sxs-lookup"><span data-stu-id="3a635-225">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3a635-226">Create a SQL Database in Azure</span><span class="sxs-lookup"><span data-stu-id="3a635-226">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="3a635-227">Connect a .NET Core app to SQL Database</span><span class="sxs-lookup"><span data-stu-id="3a635-227">Connect a .NET Core app to SQL Database</span></span>
> * <span data-ttu-id="3a635-228">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="3a635-228">Deploy the app to Azure</span></span>
> * <span data-ttu-id="3a635-229">Update the data model and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="3a635-229">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="3a635-230">Stream logs from Azure to your terminal</span><span class="sxs-lookup"><span data-stu-id="3a635-230">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="3a635-231">Manage the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3a635-231">Manage the app in the Azure portal</span></span>

<span data-ttu-id="3a635-232">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span><span class="sxs-lookup"><span data-stu-id="3a635-232">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3a635-233">Map an existing custom DNS name to Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="3a635-233">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
