---
title: Secure Azure SQL Database connection from App Service using a managed identity | Microsoft Docs
description: Learn how to make database connectivity more secure by using a managed identity, and also how to apply this to other Azure services.
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
ms.date: 04/17/2018
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3125db03dc13f70524fd094736f50b563ef712a4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869058"
---
# <a name="tutorial-secure-azure-sql-database-connection-from-app-service-using-a-managed-identity"></a><span data-ttu-id="6c1b6-103">Tutorial: Secure Azure SQL Database connection from App Service using a managed identity</span><span class="sxs-lookup"><span data-stu-id="6c1b6-103">Tutorial: Secure Azure SQL Database connection from App Service using a managed identity</span></span>

<span data-ttu-id="6c1b6-104">[App Service](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service in Azure.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-104">[App Service](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service in Azure.</span></span> <span data-ttu-id="6c1b6-105">It also provides a [managed identity](app-service-managed-service-identity.md) for your app, which is a turn-key solution for securing access to [Azure SQL Database](/azure/sql-database/) and other Azure services.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-105">It also provides a [managed identity](app-service-managed-service-identity.md) for your app, which is a turn-key solution for securing access to [Azure SQL Database](/azure/sql-database/) and other Azure services.</span></span> <span data-ttu-id="6c1b6-106">Managed identities in App Service make your app more secure by eliminating secrets from your app, such as credentials in the connection strings.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-106">Managed identities in App Service make your app more secure by eliminating secrets from your app, such as credentials in the connection strings.</span></span> <span data-ttu-id="6c1b6-107">In this tutorial, you will add managed identity to the sample ASP.NET web app you built in [Tutorial: Build an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md).</span><span class="sxs-lookup"><span data-stu-id="6c1b6-107">In this tutorial, you will add managed identity to the sample ASP.NET web app you built in [Tutorial: Build an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md).</span></span> <span data-ttu-id="6c1b6-108">When you're finished, your sample app will connect to SQL Database securely without the need of username and passwords.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-108">When you're finished, your sample app will connect to SQL Database securely without the need of username and passwords.</span></span>

<span data-ttu-id="6c1b6-109">What you learn how to:</span><span class="sxs-lookup"><span data-stu-id="6c1b6-109">What you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6c1b6-110">Enable managed identities</span><span class="sxs-lookup"><span data-stu-id="6c1b6-110">Enable managed identities</span></span>
> * <span data-ttu-id="6c1b6-111">Grant SQL Database access to the managed identity</span><span class="sxs-lookup"><span data-stu-id="6c1b6-111">Grant SQL Database access to the managed identity</span></span>
> * <span data-ttu-id="6c1b6-112">Configure application code to authenticate with SQL Database using Azure Active Directory authentication</span><span class="sxs-lookup"><span data-stu-id="6c1b6-112">Configure application code to authenticate with SQL Database using Azure Active Directory authentication</span></span>
> * <span data-ttu-id="6c1b6-113">Grant minimal privileges to the managed identity in SQL Database</span><span class="sxs-lookup"><span data-stu-id="6c1b6-113">Grant minimal privileges to the managed identity in SQL Database</span></span>

> [!NOTE]
> <span data-ttu-id="6c1b6-114">Azure Active Directory authentication is _different_ from [Integrated Windows authentication](/previous-versions/windows/it-pro/windows-server-2003/cc758557(v=ws.10)) in on-premises Active Directory (AD DS).</span><span class="sxs-lookup"><span data-stu-id="6c1b6-114">Azure Active Directory authentication is _different_ from [Integrated Windows authentication](/previous-versions/windows/it-pro/windows-server-2003/cc758557(v=ws.10)) in on-premises Active Directory (AD DS).</span></span> <span data-ttu-id="6c1b6-115">AD DS and Azure Active Directory use completely different authentication protocols.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-115">AD DS and Azure Active Directory use completely different authentication protocols.</span></span> <span data-ttu-id="6c1b6-116">For more information, see [The difference between Windows Server AD DS and Azure AD](../active-directory/fundamentals/understand-azure-identity-solutions.md#the-difference-between-windows-server-ad-ds-and-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="6c1b6-116">For more information, see [The difference between Windows Server AD DS and Azure AD](../active-directory/fundamentals/understand-azure-identity-solutions.md#the-difference-between-windows-server-ad-ds-and-azure-ad).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="6c1b6-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c1b6-117">Prerequisites</span></span>

<span data-ttu-id="6c1b6-118">This article continues where you left off in [Tutorial: Build an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md).</span><span class="sxs-lookup"><span data-stu-id="6c1b6-118">This article continues where you left off in [Tutorial: Build an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md).</span></span> <span data-ttu-id="6c1b6-119">If you haven't already, follow that tutorial first.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-119">If you haven't already, follow that tutorial first.</span></span> <span data-ttu-id="6c1b6-120">Alternatively, you can adapt the steps for your own ASP.NET app with SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-120">Alternatively, you can adapt the steps for your own ASP.NET app with SQL Database.</span></span>

<!-- ![app running in App Service](./media/app-service-web-tutorial-dotnetcore-sqldb/azure-app-in-browser.png) -->

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="enable-managed-identities"></a><span data-ttu-id="6c1b6-121">Enable managed identities</span><span class="sxs-lookup"><span data-stu-id="6c1b6-121">Enable managed identities</span></span>

<span data-ttu-id="6c1b6-122">To enable a managed identity for your Azure app, use the [az webapp identity assign](/cli/azure/webapp/identity?view=azure-cli-latest#az-webapp-identity-assign) command in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-122">To enable a managed identity for your Azure app, use the [az webapp identity assign](/cli/azure/webapp/identity?view=azure-cli-latest#az-webapp-identity-assign) command in the Cloud Shell.</span></span> <span data-ttu-id="6c1b6-123">In the following command, replace *\<app name>*.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-123">In the following command, replace *\<app name>*.</span></span>

```azurecli-interactive
az webapp identity assign --resource-group myResourceGroup --name <app name>
```

<span data-ttu-id="6c1b6-124">Here's an example of the output after the identity is created in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="6c1b6-124">Here's an example of the output after the identity is created in Azure Active Directory:</span></span>

```json
{
  "additionalProperties": {},
  "principalId": "21dfa71c-9e6f-4d17-9e90-1d28801c9735",
  "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
  "type": "SystemAssigned"
}
```

<span data-ttu-id="6c1b6-125">You'll use the value of `principalId` in the next step.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-125">You'll use the value of `principalId` in the next step.</span></span> <span data-ttu-id="6c1b6-126">If you want to see the details of the new identity in Azure Active Directory, run the following optional command with the value of `principalId`:</span><span class="sxs-lookup"><span data-stu-id="6c1b6-126">If you want to see the details of the new identity in Azure Active Directory, run the following optional command with the value of `principalId`:</span></span>

```azurecli-interactive
az ad sp show --id <principalid>
```

## <a name="grant-database-access-to-identity"></a><span data-ttu-id="6c1b6-127">Grant database access to identity</span><span class="sxs-lookup"><span data-stu-id="6c1b6-127">Grant database access to identity</span></span>

<span data-ttu-id="6c1b6-128">Next, you grant database access to your app's managed identity, using the [`az sql server ad-admin create`](/cli/azure/sql/server/ad-admin?view=azure-cli-latest#az-sql-server-ad-admin_create) command in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-128">Next, you grant database access to your app's managed identity, using the [`az sql server ad-admin create`](/cli/azure/sql/server/ad-admin?view=azure-cli-latest#az-sql-server-ad-admin_create) command in the Cloud Shell.</span></span> <span data-ttu-id="6c1b6-129">In the following command, replace *\<server_name>* and <principalid_from_last_step>.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-129">In the following command, replace *\<server_name>* and <principalid_from_last_step>.</span></span> <span data-ttu-id="6c1b6-130">Type an administrator name for *\<admin_user>*.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-130">Type an administrator name for *\<admin_user>*.</span></span>

```azurecli-interactive
az sql server ad-admin create --resource-group myResourceGroup --server-name <server_name> --display-name <admin_user> --object-id <principalid_from_last_step>
```

<span data-ttu-id="6c1b6-131">The managed identity now has access to your Azure SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-131">The managed identity now has access to your Azure SQL Database server.</span></span>

## <a name="modify-connection-string"></a><span data-ttu-id="6c1b6-132">Modify connection string</span><span class="sxs-lookup"><span data-stu-id="6c1b6-132">Modify connection string</span></span>

<span data-ttu-id="6c1b6-133">Modify the connection you set previously for your app, using the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-133">Modify the connection you set previously for your app, using the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in the Cloud Shell.</span></span> <span data-ttu-id="6c1b6-134">In the following command, replace *\<app name>* with the name of your app, and replace *\<server_name>* and *\<db_name>* with the ones for your SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-134">In the following command, replace *\<app name>* with the name of your app, and replace *\<server_name>* and *\<db_name>* with the ones for your SQL Database.</span></span>

```azurecli-interactive
az webapp config connection-string set --resource-group myResourceGroup --name <app name> --settings MyDbConnection='Server=tcp:<server_name>.database.windows.net,1433;Database=<db_name>;' --connection-string-type SQLAzure
```

## <a name="modify-aspnet-code"></a><span data-ttu-id="6c1b6-135">Modify ASP.NET code</span><span class="sxs-lookup"><span data-stu-id="6c1b6-135">Modify ASP.NET code</span></span>

<span data-ttu-id="6c1b6-136">In your **DotNetAppSqlDb** project in Visual Studio, open _packages.config_ and add the following line in the list of packages.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-136">In your **DotNetAppSqlDb** project in Visual Studio, open _packages.config_ and add the following line in the list of packages.</span></span>

```xml
<package id="Microsoft.Azure.Services.AppAuthentication" version="1.1.0-preview" targetFramework="net461" />
```

<span data-ttu-id="6c1b6-137">Open _Models\MyDatabaseContext.cs_ and add the following `using` statements to the top of the file:</span><span class="sxs-lookup"><span data-stu-id="6c1b6-137">Open _Models\MyDatabaseContext.cs_ and add the following `using` statements to the top of the file:</span></span>

```csharp
using System.Data.SqlClient;
using Microsoft.Azure.Services.AppAuthentication;
using System.Web.Configuration;
```

<span data-ttu-id="6c1b6-138">In the `MyDatabaseContext` class, add the following constructor:</span><span class="sxs-lookup"><span data-stu-id="6c1b6-138">In the `MyDatabaseContext` class, add the following constructor:</span></span>

```csharp
public MyDatabaseContext(SqlConnection conn) : base(conn, true)
{
    conn.ConnectionString = WebConfigurationManager.ConnectionStrings["MyDbConnection"].ConnectionString;
    // DataSource != LocalDB means app is running in Azure with the SQLDB connection string you configured
    if(conn.DataSource != "(localdb)\\MSSQLLocalDB")
        conn.AccessToken = (new AzureServiceTokenProvider()).GetAccessTokenAsync("https://database.windows.net/").Result;

    Database.SetInitializer<MyDatabaseContext>(null);
}
```

<span data-ttu-id="6c1b6-139">This constructor configures a custom SqlConnection object to use an access token for Azure SQL Database from App Service.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-139">This constructor configures a custom SqlConnection object to use an access token for Azure SQL Database from App Service.</span></span> <span data-ttu-id="6c1b6-140">With the access token, your App Service app authenticates with Azure SQL Database with its managed identity.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-140">With the access token, your App Service app authenticates with Azure SQL Database with its managed identity.</span></span> <span data-ttu-id="6c1b6-141">For more information, see [Obtaining tokens for Azure resources](app-service-managed-service-identity.md#obtaining-tokens-for-azure-resources).</span><span class="sxs-lookup"><span data-stu-id="6c1b6-141">For more information, see [Obtaining tokens for Azure resources](app-service-managed-service-identity.md#obtaining-tokens-for-azure-resources).</span></span> <span data-ttu-id="6c1b6-142">The `if` statement lets you continue to test your app locally with LocalDB.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-142">The `if` statement lets you continue to test your app locally with LocalDB.</span></span>

> [!NOTE]
> <span data-ttu-id="6c1b6-143">`SqlConnection.AccessToken` is currently supported only in .NET Framework 4.6 and above, not in [.NET Core](https://www.microsoft.com/net/learn/get-started/windows).</span><span class="sxs-lookup"><span data-stu-id="6c1b6-143">`SqlConnection.AccessToken` is currently supported only in .NET Framework 4.6 and above, not in [.NET Core](https://www.microsoft.com/net/learn/get-started/windows).</span></span>
>

<span data-ttu-id="6c1b6-144">To use this new constructor, open `Controllers\TodosController.cs` and find the line `private MyDatabaseContext db = new MyDatabaseContext();`.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-144">To use this new constructor, open `Controllers\TodosController.cs` and find the line `private MyDatabaseContext db = new MyDatabaseContext();`.</span></span> <span data-ttu-id="6c1b6-145">The existing code uses the default `MyDatabaseContext` controller to create a database using the standard connection string, which had username and password in clear text before [you changed it](#modify-connection-string).</span><span class="sxs-lookup"><span data-stu-id="6c1b6-145">The existing code uses the default `MyDatabaseContext` controller to create a database using the standard connection string, which had username and password in clear text before [you changed it](#modify-connection-string).</span></span>

<span data-ttu-id="6c1b6-146">Replace the entire line with the following code:</span><span class="sxs-lookup"><span data-stu-id="6c1b6-146">Replace the entire line with the following code:</span></span>

```csharp
private MyDatabaseContext db = new MyDatabaseContext(new SqlConnection());
```

### <a name="publish-your-changes"></a><span data-ttu-id="6c1b6-147">Publish your changes</span><span class="sxs-lookup"><span data-stu-id="6c1b6-147">Publish your changes</span></span>

<span data-ttu-id="6c1b6-148">All that's left now is to publish your changes to Azure.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-148">All that's left now is to publish your changes to Azure.</span></span>

<span data-ttu-id="6c1b6-149">In the **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-149">In the **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Publish from Solution Explorer](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="6c1b6-151">In the publish page, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-151">In the publish page, click **Publish**.</span></span> <span data-ttu-id="6c1b6-152">When the new webpage shows your to-do list, your app is connecting to the database using the managed identity.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-152">When the new webpage shows your to-do list, your app is connecting to the database using the managed identity.</span></span>

![Azure web app after Code First Migration](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="6c1b6-154">You should now be able to edit the to-do list as before.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-154">You should now be able to edit the to-do list as before.</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="grant-minimal-privileges-to-identity"></a><span data-ttu-id="6c1b6-155">Grant minimal privileges to identity</span><span class="sxs-lookup"><span data-stu-id="6c1b6-155">Grant minimal privileges to identity</span></span>

<span data-ttu-id="6c1b6-156">During the earlier steps, you probably noticed your managed identity is connected to SQL Server as the Azure AD administrator.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-156">During the earlier steps, you probably noticed your managed identity is connected to SQL Server as the Azure AD administrator.</span></span> <span data-ttu-id="6c1b6-157">To grant minimal privileges to your managed identity, you need to sign in to the Azure SQL Database server as the Azure AD administrator, and then add an Azure Active Directory group that contains the managed identity.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-157">To grant minimal privileges to your managed identity, you need to sign in to the Azure SQL Database server as the Azure AD administrator, and then add an Azure Active Directory group that contains the managed identity.</span></span> 

### <a name="add-managed-identity-to-an-azure-active-directory-group"></a><span data-ttu-id="6c1b6-158">Add managed identity to an Azure Active Directory group</span><span class="sxs-lookup"><span data-stu-id="6c1b6-158">Add managed identity to an Azure Active Directory group</span></span>

<span data-ttu-id="6c1b6-159">In the Cloud Shell, add the managed identity for your app into a new Azure Active Directory group called _myAzureSQLDBAccessGroup_, shown in the following script:</span><span class="sxs-lookup"><span data-stu-id="6c1b6-159">In the Cloud Shell, add the managed identity for your app into a new Azure Active Directory group called _myAzureSQLDBAccessGroup_, shown in the following script:</span></span>

```azurecli-interactive
groupid=$(az ad group create --display-name myAzureSQLDBAccessGroup --mail-nickname myAzureSQLDBAccessGroup --query objectId --output tsv)
msiobjectid=$(az webapp identity show --resource-group <group_name> --name <app_name> --query principalId --output tsv)
az ad group member add --group $groupid --member-id $msiobjectid
az ad group member list -g $groupid
```

<span data-ttu-id="6c1b6-160">If you want to see the full JSON output for each command, drop the parameters `--query objectId --output tsv`.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-160">If you want to see the full JSON output for each command, drop the parameters `--query objectId --output tsv`.</span></span>

### <a name="reconfigure-azure-ad-administrator"></a><span data-ttu-id="6c1b6-161">Reconfigure Azure AD administrator</span><span class="sxs-lookup"><span data-stu-id="6c1b6-161">Reconfigure Azure AD administrator</span></span>

<span data-ttu-id="6c1b6-162">Previously, you assigned the managed identity as the Azure AD administrator for your SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-162">Previously, you assigned the managed identity as the Azure AD administrator for your SQL Database.</span></span> <span data-ttu-id="6c1b6-163">You can't use this identity for interactive sign-in (to add database users), so you need to use your real Azure AD user.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-163">You can't use this identity for interactive sign-in (to add database users), so you need to use your real Azure AD user.</span></span> <span data-ttu-id="6c1b6-164">To add your Azure AD user, follow the steps at [Provision an Azure Active Directory administrator for your Azure SQL Database Server](../sql-database/sql-database-aad-authentication-configure.md#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server).</span><span class="sxs-lookup"><span data-stu-id="6c1b6-164">To add your Azure AD user, follow the steps at [Provision an Azure Active Directory administrator for your Azure SQL Database Server](../sql-database/sql-database-aad-authentication-configure.md#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server).</span></span> 

### <a name="grant-permissions-to-azure-active-directory-group"></a><span data-ttu-id="6c1b6-165">Grant permissions to Azure Active Directory group</span><span class="sxs-lookup"><span data-stu-id="6c1b6-165">Grant permissions to Azure Active Directory group</span></span>

<span data-ttu-id="6c1b6-166">In the Cloud Shell, sign in to SQL Database by using the SQLCMD command.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-166">In the Cloud Shell, sign in to SQL Database by using the SQLCMD command.</span></span> <span data-ttu-id="6c1b6-167">Replace _\<servername>_ with your SQL Database server name, and replace _\<AADusername>_ and _\<AADpassword>_ with your Azure AD user's credentials.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-167">Replace _\<servername>_ with your SQL Database server name, and replace _\<AADusername>_ and _\<AADpassword>_ with your Azure AD user's credentials.</span></span>

```azurecli-interactive
sqlcmd -S <server_name>.database.windows.net -U <AADuser_name> -P "<AADpassword>" -G -l 30
```

<span data-ttu-id="6c1b6-168">In the SQL prompt, run the following commands, which add the Azure Active Directory group you created earlier as a user.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-168">In the SQL prompt, run the following commands, which add the Azure Active Directory group you created earlier as a user.</span></span>

```sql
CREATE USER [myAzureSQLDBAccessGroup] FROM EXTERNAL PROVIDER;
GO
```

<span data-ttu-id="6c1b6-169">Type `EXIT` to return to the Cloud Shell prompt.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-169">Type `EXIT` to return to the Cloud Shell prompt.</span></span> <span data-ttu-id="6c1b6-170">Next, run SQLCMD again, but specify the database name in _\<dbname>_.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-170">Next, run SQLCMD again, but specify the database name in _\<dbname>_.</span></span>

```azurecli-interactive
sqlcmd -S <server_name>.database.windows.net -d <db_name> -U <AADuser_name> -P "<AADpassword>" -G -l 30
```

<span data-ttu-id="6c1b6-171">In the SQL prompt for the database you want, run the following commands to grant read and write permissions to the Azure Active Directory group.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-171">In the SQL prompt for the database you want, run the following commands to grant read and write permissions to the Azure Active Directory group.</span></span>

```sql
ALTER ROLE db_datareader ADD MEMBER [myAzureSQLDBAccessGroup];
ALTER ROLE db_datawriter ADD MEMBER [myAzureSQLDBAccessGroup];
GO
```

## <a name="next-steps"></a><span data-ttu-id="6c1b6-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c1b6-172">Next steps</span></span>

<span data-ttu-id="6c1b6-173">What you learned:</span><span class="sxs-lookup"><span data-stu-id="6c1b6-173">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6c1b6-174">Enable managed identities</span><span class="sxs-lookup"><span data-stu-id="6c1b6-174">Enable managed identities</span></span>
> * <span data-ttu-id="6c1b6-175">Grant SQL Database access to the managed identity</span><span class="sxs-lookup"><span data-stu-id="6c1b6-175">Grant SQL Database access to the managed identity</span></span>
> * <span data-ttu-id="6c1b6-176">Configure application code to authenticate with SQL Database using Azure Active Directory authentication</span><span class="sxs-lookup"><span data-stu-id="6c1b6-176">Configure application code to authenticate with SQL Database using Azure Active Directory authentication</span></span>
> * <span data-ttu-id="6c1b6-177">Grant minimal privileges to the managed identity in SQL Database</span><span class="sxs-lookup"><span data-stu-id="6c1b6-177">Grant minimal privileges to the managed identity in SQL Database</span></span>

<span data-ttu-id="6c1b6-178">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span><span class="sxs-lookup"><span data-stu-id="6c1b6-178">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6c1b6-179">Map an existing custom DNS name to Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="6c1b6-179">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
