---
title: Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service
description: Learn how to develop an ASP.NET MVC 5 app with a SQL Database back-end, add authentication and authorization, and deploy it to Azure.
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: ''
ms.assetid: c0de419d-db6f-4157-94ca-f75d0ba6c0e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2016
ms.author: riande
ms.openlocfilehash: 27564be9cc97169494d004a9c018aa372f92a0d0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551788"
---
# <a name="create-an-aspnet-mvc-app-with-auth-and-sql-db-and-deploy-to-azure-app-service"></a><span data-ttu-id="d333f-103">Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d333f-103">Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service</span></span>
<span data-ttu-id="d333f-104">This tutorial shows how to build a secure ASP.NET MVC 5 web app that lets users log in with credentials from Facebook or Google.</span><span class="sxs-lookup"><span data-stu-id="d333f-104">This tutorial shows how to build a secure ASP.NET MVC 5 web app that lets users log in with credentials from Facebook or Google.</span></span> <span data-ttu-id="d333f-105">The app is a simple contact list that uses the ADO.NET Entity Framework for database access.</span><span class="sxs-lookup"><span data-stu-id="d333f-105">The app is a simple contact list that uses the ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="d333f-106">You'll deploy the app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="d333f-106">You'll deploy the app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> 

<span data-ttu-id="d333f-107">On completing the tutorial, you'll have a secure data-driven web application up and running in the cloud and using a cloud database.</span><span class="sxs-lookup"><span data-stu-id="d333f-107">On completing the tutorial, you'll have a secure data-driven web application up and running in the cloud and using a cloud database.</span></span> <span data-ttu-id="d333f-108">The following illustration shows the login page for the completed application.</span><span class="sxs-lookup"><span data-stu-id="d333f-108">The following illustration shows the login page for the completed application.</span></span>

![login page][rxb]

<span data-ttu-id="d333f-110">You'll learn:</span><span class="sxs-lookup"><span data-stu-id="d333f-110">You'll learn:</span></span>

* <span data-ttu-id="d333f-111">How to create a secure ASP.NET MVC 5 web project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d333f-111">How to create a secure ASP.NET MVC 5 web project in Visual Studio.</span></span>
* <span data-ttu-id="d333f-112">How to authenticate and authorize users who log on with credentials from their Google or Facebook accounts (social provider authentication using [OAuth 2.0](http://oauth.net/2 "http://oauth.net/2")).</span><span class="sxs-lookup"><span data-stu-id="d333f-112">How to authenticate and authorize users who log on with credentials from their Google or Facebook accounts (social provider authentication using [OAuth 2.0](http://oauth.net/2 "http://oauth.net/2")).</span></span>
* <span data-ttu-id="d333f-113">How to authenticate and authorize users who register in a database managed by the application (local authentication using [ASP.NET Identity](http://asp.net/identity/)).</span><span class="sxs-lookup"><span data-stu-id="d333f-113">How to authenticate and authorize users who register in a database managed by the application (local authentication using [ASP.NET Identity](http://asp.net/identity/)).</span></span>
* <span data-ttu-id="d333f-114">How to use the ADO.NET Entity Framework 6 Code First to read and write data in a SQL database.</span><span class="sxs-lookup"><span data-stu-id="d333f-114">How to use the ADO.NET Entity Framework 6 Code First to read and write data in a SQL database.</span></span>
* <span data-ttu-id="d333f-115">How to use Entity Framework Code First Migrations to deploy a database.</span><span class="sxs-lookup"><span data-stu-id="d333f-115">How to use Entity Framework Code First Migrations to deploy a database.</span></span>
* <span data-ttu-id="d333f-116">How to store relational data in the cloud by using Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d333f-116">How to store relational data in the cloud by using Azure SQL Database.</span></span>
* <span data-ttu-id="d333f-117">How to deploy a web project that uses a database to a [web app](http://go.microsoft.com/fwlink/?LinkId=529714) in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="d333f-117">How to deploy a web project that uses a database to a [web app](http://go.microsoft.com/fwlink/?LinkId=529714) in Azure App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="d333f-118">This is a long tutorial.</span><span class="sxs-lookup"><span data-stu-id="d333f-118">This is a long tutorial.</span></span> <span data-ttu-id="d333f-119">If you want a quick introduction to Azure App Service and Visual Studio web projects, see [Create an ASP.NET web app in Azure App Service](app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d333f-119">If you want a quick introduction to Azure App Service and Visual Studio web projects, see [Create an ASP.NET web app in Azure App Service](app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="d333f-120">For troubleshooting info, see the [Troubleshooting](#troubleshooting) section.</span><span class="sxs-lookup"><span data-stu-id="d333f-120">For troubleshooting info, see the [Troubleshooting](#troubleshooting) section.</span></span>
> 
> <span data-ttu-id="d333f-121">Or if you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="d333f-121">Or if you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d333f-122">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="d333f-122">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d333f-123">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d333f-123">Prerequisites</span></span>
<span data-ttu-id="d333f-124">To complete this tutorial, you need a Microsoft Azure account.</span><span class="sxs-lookup"><span data-stu-id="d333f-124">To complete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="d333f-125">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="d333f-125">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="d333f-126">To set up your development environment, you must install [Visual Studio 2013 Update 5](http://go.microsoft.com/fwlink/?LinkId=390521) or higher, and the latest version of the [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="d333f-126">To set up your development environment, you must install [Visual Studio 2013 Update 5](http://go.microsoft.com/fwlink/?LinkId=390521) or higher, and the latest version of the [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409).</span></span> <span data-ttu-id="d333f-127">This article was written for Visual Studio Update 4 and SDK 2.8.1.</span><span class="sxs-lookup"><span data-stu-id="d333f-127">This article was written for Visual Studio Update 4 and SDK 2.8.1.</span></span> <span data-ttu-id="d333f-128">The same instructions work for Visual Studio 2015 with the latest [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409) installed, but some screens will look different from the illustrations.</span><span class="sxs-lookup"><span data-stu-id="d333f-128">The same instructions work for Visual Studio 2015 with the latest [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409) installed, but some screens will look different from the illustrations.</span></span>

## <a name="create-an-aspnet-mvc-5-application"></a><span data-ttu-id="d333f-129">Create an ASP.NET MVC 5 application</span><span class="sxs-lookup"><span data-stu-id="d333f-129">Create an ASP.NET MVC 5 application</span></span>
### <a name="create-the-project"></a><span data-ttu-id="d333f-130">Create the project</span><span class="sxs-lookup"><span data-stu-id="d333f-130">Create the project</span></span>
1. <span data-ttu-id="d333f-131">From the **File** menu, click **New Project**.</span><span class="sxs-lookup"><span data-stu-id="d333f-131">From the **File** menu, click **New Project**.</span></span>
   
    ![New Project in File menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/gs13newproj.png)
2. <span data-ttu-id="d333f-133">In the **New Project** dialog box, expand **C#** and select **Web** under **Installed Templates**, and then select **ASP.NET Web Application**.</span><span class="sxs-lookup"><span data-stu-id="d333f-133">In the **New Project** dialog box, expand **C#** and select **Web** under **Installed Templates**, and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="d333f-134">Name the application **ContactManager**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d333f-134">Name the application **ContactManager**, and then click **OK**.</span></span>
   
    ![New Project dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/GS13newprojdb.png)
   
    <span data-ttu-id="d333f-136">**Note:** Make sure you enter "ContactManager".</span><span class="sxs-lookup"><span data-stu-id="d333f-136">**Note:** Make sure you enter "ContactManager".</span></span> <span data-ttu-id="d333f-137">Code blocks that you'll be copying later assume that the project name is ContactManager.</span><span class="sxs-lookup"><span data-stu-id="d333f-137">Code blocks that you'll be copying later assume that the project name is ContactManager.</span></span> 
3. <span data-ttu-id="d333f-138">In the **New ASP.NET Project** dialog box, select the **MVC** template.</span><span class="sxs-lookup"><span data-stu-id="d333f-138">In the **New ASP.NET Project** dialog box, select the **MVC** template.</span></span> <span data-ttu-id="d333f-139">Verify **Authentication** is set to **Individual User Accounts**, **Host in the cloud** is checked, and **App Service** is selected.</span><span class="sxs-lookup"><span data-stu-id="d333f-139">Verify **Authentication** is set to **Individual User Accounts**, **Host in the cloud** is checked, and **App Service** is selected.</span></span>
   
    ![New ASP.NET Project dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/newproject.png)
4. <span data-ttu-id="d333f-141">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d333f-141">Click **OK**.</span></span>
5. <span data-ttu-id="d333f-142">The **Configure Microsoft Azure Web App Settings** dialog appears.</span><span class="sxs-lookup"><span data-stu-id="d333f-142">The **Configure Microsoft Azure Web App Settings** dialog appears.</span></span> <span data-ttu-id="d333f-143">You may need to sign in if you have not already done so, or reenter your credentials if your login is expired.</span><span class="sxs-lookup"><span data-stu-id="d333f-143">You may need to sign in if you have not already done so, or reenter your credentials if your login is expired.</span></span>
6. <span data-ttu-id="d333f-144">Optional - change the value in the **Web App name** box (see image below).</span><span class="sxs-lookup"><span data-stu-id="d333f-144">Optional - change the value in the **Web App name** box (see image below).</span></span>
   
    <span data-ttu-id="d333f-145">The URL of the web app will be {name}.azurewebsites.net, so the name has to be unique in the azurewebsites.net domain.</span><span class="sxs-lookup"><span data-stu-id="d333f-145">The URL of the web app will be {name}.azurewebsites.net, so the name has to be unique in the azurewebsites.net domain.</span></span> <span data-ttu-id="d333f-146">The configuration wizard suggests a unique name by appending a number to the project name "ContactManager", and that's fine for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d333f-146">The configuration wizard suggests a unique name by appending a number to the project name "ContactManager", and that's fine for this tutorial.</span></span>
7. <span data-ttu-id="d333f-147">In the **Resource group** drop-down select an existing group or **Create new resource group**(see image below).</span><span class="sxs-lookup"><span data-stu-id="d333f-147">In the **Resource group** drop-down select an existing group or **Create new resource group**(see image below).</span></span> 
   
    <span data-ttu-id="d333f-148">If you prefer, you can select a resource group that you already have.</span><span class="sxs-lookup"><span data-stu-id="d333f-148">If you prefer, you can select a resource group that you already have.</span></span> <span data-ttu-id="d333f-149">But if you create a new resource group and only use it for this tutorial, it will be easy to delete all Azure resources you created for the tutorial when you're done with them.</span><span class="sxs-lookup"><span data-stu-id="d333f-149">But if you create a new resource group and only use it for this tutorial, it will be easy to delete all Azure resources you created for the tutorial when you're done with them.</span></span> <span data-ttu-id="d333f-150">For information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d333f-150">For information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span> 
8. <span data-ttu-id="d333f-151">In the **App Service plan** drop-down select select an existing plan or **Create new App Service plan**(see image below).</span><span class="sxs-lookup"><span data-stu-id="d333f-151">In the **App Service plan** drop-down select select an existing plan or **Create new App Service plan**(see image below).</span></span>
   
    <span data-ttu-id="d333f-152">If you prefer, you can select an App Service plan that you already have.</span><span class="sxs-lookup"><span data-stu-id="d333f-152">If you prefer, you can select an App Service plan that you already have.</span></span> <span data-ttu-id="d333f-153">For information about App Service plans, see [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d333f-153">For information about App Service plans, see [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 
9. <span data-ttu-id="d333f-154">Tap **Explore additional Azure services** to add a SQL database.</span><span class="sxs-lookup"><span data-stu-id="d333f-154">Tap **Explore additional Azure services** to add a SQL database.</span></span>
   
    ![Add new services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/n2.png)
10. <span data-ttu-id="d333f-156">Tap the **+** icon to add a SQL database.</span><span class="sxs-lookup"><span data-stu-id="d333f-156">Tap the **+** icon to add a SQL database.</span></span>
    
     ![New SQL DB](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/nsql.png)
11. <span data-ttu-id="d333f-158">Tap **New** on the  **Configure SQL Database** dialog:</span><span class="sxs-lookup"><span data-stu-id="d333f-158">Tap **New** on the  **Configure SQL Database** dialog:</span></span>
    
     ![SQL admin name and pw](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/nc.png)
12. <span data-ttu-id="d333f-160">Enter a name for the administrator and a strong password.</span><span class="sxs-lookup"><span data-stu-id="d333f-160">Enter a name for the administrator and a strong password.</span></span>
    
     ![New SQL DB](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/np.png)
    
     <span data-ttu-id="d333f-162">The server name must be unique.</span><span class="sxs-lookup"><span data-stu-id="d333f-162">The server name must be unique.</span></span> <span data-ttu-id="d333f-163">It can contain lower-case letters, numeric digits, and hyphens.</span><span class="sxs-lookup"><span data-stu-id="d333f-163">It can contain lower-case letters, numeric digits, and hyphens.</span></span> <span data-ttu-id="d333f-164">It cannot contain a trailing hyphen.</span><span class="sxs-lookup"><span data-stu-id="d333f-164">It cannot contain a trailing hyphen.</span></span> <span data-ttu-id="d333f-165">The user name and password are new credentials you're creating for the new server.</span><span class="sxs-lookup"><span data-stu-id="d333f-165">The user name and password are new credentials you're creating for the new server.</span></span> 
    
     <span data-ttu-id="d333f-166">If you already have a database server, you can select that instead of creating one.</span><span class="sxs-lookup"><span data-stu-id="d333f-166">If you already have a database server, you can select that instead of creating one.</span></span> <span data-ttu-id="d333f-167">Database servers are a precious resource, and you generally want to create multiple databases on the same server for testing and development rather than creating a database server per database.</span><span class="sxs-lookup"><span data-stu-id="d333f-167">Database servers are a precious resource, and you generally want to create multiple databases on the same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="d333f-168">However, for this tutorial you only need the server temporarily, and by creating the server in the same resource group as the web site you make it easy to delete both web app and database resources by deleting the resource group when you're done with the tutorial.</span><span class="sxs-lookup"><span data-stu-id="d333f-168">However, for this tutorial you only need the server temporarily, and by creating the server in the same resource group as the web site you make it easy to delete both web app and database resources by deleting the resource group when you're done with the tutorial.</span></span> 
    
     <span data-ttu-id="d333f-169">If you select an existing database server, make sure your web app and database are in the same region.</span><span class="sxs-lookup"><span data-stu-id="d333f-169">If you select an existing database server, make sure your web app and database are in the same region.</span></span>
    
     ![Use new database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/newdb.png)
13. <span data-ttu-id="d333f-171">Tap **Create**.</span><span class="sxs-lookup"><span data-stu-id="d333f-171">Tap **Create**.</span></span>
    
     <span data-ttu-id="d333f-172">Visual Studio creates the ContactManager web project, creates the resource group and App Service plan that you specified, and creates a web app in Azure App Service with the name you specified.</span><span class="sxs-lookup"><span data-stu-id="d333f-172">Visual Studio creates the ContactManager web project, creates the resource group and App Service plan that you specified, and creates a web app in Azure App Service with the name you specified.</span></span>

### <a name="set-the-page-header-and-footer"></a><span data-ttu-id="d333f-173">Set the page header and footer</span><span class="sxs-lookup"><span data-stu-id="d333f-173">Set the page header and footer</span></span>
1. <span data-ttu-id="d333f-174">In **Solution Explorer** open the *Layout.cshtml* file in the *Views\Shared* folder.</span><span class="sxs-lookup"><span data-stu-id="d333f-174">In **Solution Explorer** open the *Layout.cshtml* file in the *Views\Shared* folder.</span></span>
   
    ![_Layout.cshtml in Solution Explorer][newapp004]
2. <span data-ttu-id="d333f-176">Replace the ActionLink in the *Layout.cshtml* file with the following code.</span><span class="sxs-lookup"><span data-stu-id="d333f-176">Replace the ActionLink in the *Layout.cshtml* file with the following code.</span></span>

```
   @Html.ActionLink("CM Demo", "Index", "Contacts", new { area = "" }, new { @class = "navbar-brand" })
```
   <span data-ttu-id="d333f-177">Make sure you change the third parameter from "Home" to "Contacts".</span><span class="sxs-lookup"><span data-stu-id="d333f-177">Make sure you change the third parameter from "Home" to "Contacts".</span></span> <span data-ttu-id="d333f-178">The markup above will create a "Contacts" link on each page to the Index method of the Contacts controller.</span><span class="sxs-lookup"><span data-stu-id="d333f-178">The markup above will create a "Contacts" link on each page to the Index method of the Contacts controller.</span></span> <span data-ttu-id="d333f-179">Change the application name in the header and the footer from "My ASP.NET Application" and "Application name" to "Contact Manager" and "CM Demo".</span><span class="sxs-lookup"><span data-stu-id="d333f-179">Change the application name in the header and the footer from "My ASP.NET Application" and "Application name" to "Contact Manager" and "CM Demo".</span></span> 

### <a name="run-the-application-locally"></a><span data-ttu-id="d333f-180">Run the application locally</span><span class="sxs-lookup"><span data-stu-id="d333f-180">Run the application locally</span></span>
1. <span data-ttu-id="d333f-181">Press CTRL+F5 to run the app.</span><span class="sxs-lookup"><span data-stu-id="d333f-181">Press CTRL+F5 to run the app.</span></span>
   
    <span data-ttu-id="d333f-182">The application home page appears in the default browser.</span><span class="sxs-lookup"><span data-stu-id="d333f-182">The application home page appears in the default browser.</span></span>
   
    ![Web app running locally](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/rr2.png)

<span data-ttu-id="d333f-184">This is all you need to do for now to create the application that you'll deploy to Azure.</span><span class="sxs-lookup"><span data-stu-id="d333f-184">This is all you need to do for now to create the application that you'll deploy to Azure.</span></span> 

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="d333f-185">Deploy the application to Azure</span><span class="sxs-lookup"><span data-stu-id="d333f-185">Deploy the application to Azure</span></span>
1. <span data-ttu-id="d333f-186">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="d333f-186">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
   
    ![Publish in project context menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/GS13publish.png)
   
    <span data-ttu-id="d333f-188">The **Publish Web** wizard opens.</span><span class="sxs-lookup"><span data-stu-id="d333f-188">The **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="d333f-189">In the **Publish Web** dialog box, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="d333f-189">In the **Publish Web** dialog box, click **Publish**.</span></span>
   
    ![Publish](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/rr3.png)
   
    <span data-ttu-id="d333f-191">The application you created is now running in the cloud.</span><span class="sxs-lookup"><span data-stu-id="d333f-191">The application you created is now running in the cloud.</span></span> <span data-ttu-id="d333f-192">The next time you deploy the application, only the changed (or new) files will be deployed.</span><span class="sxs-lookup"><span data-stu-id="d333f-192">The next time you deploy the application, only the changed (or new) files will be deployed.</span></span>
   
    ![Running in Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/ss4.PNG)

## <a name="enable-ssl-for-the-project"></a><span data-ttu-id="d333f-194">Enable SSL for the Project</span><span class="sxs-lookup"><span data-stu-id="d333f-194">Enable SSL for the Project</span></span>
1. <span data-ttu-id="d333f-195">In **Solution Explorer**, click the **ContactManager** project, then click F4 to open the **Properties** window.</span><span class="sxs-lookup"><span data-stu-id="d333f-195">In **Solution Explorer**, click the **ContactManager** project, then click F4 to open the **Properties** window.</span></span>
2. <span data-ttu-id="d333f-196">Change **SSL Enabled** to **True**.</span><span class="sxs-lookup"><span data-stu-id="d333f-196">Change **SSL Enabled** to **True**.</span></span> 
3. <span data-ttu-id="d333f-197">Copy the **SSL URL**.</span><span class="sxs-lookup"><span data-stu-id="d333f-197">Copy the **SSL URL**.</span></span>
   
    <span data-ttu-id="d333f-198">The SSL URL will be https://localhost:44300/ unless you've previously created SSL web apps.</span><span class="sxs-lookup"><span data-stu-id="d333f-198">The SSL URL will be https://localhost:44300/ unless you've previously created SSL web apps.</span></span>
   
    ![enable SSL][rxSSL]
4. <span data-ttu-id="d333f-200">In **Solution Explorer**, right click the **Contact Manager** project and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="d333f-200">In **Solution Explorer**, right click the **Contact Manager** project and click **Properties**.</span></span>
5. <span data-ttu-id="d333f-201">Click the **Web** tab.</span><span class="sxs-lookup"><span data-stu-id="d333f-201">Click the **Web** tab.</span></span>
6. <span data-ttu-id="d333f-202">Change the **Project Url** to use the **SSL URL** and save the page (Control S).</span><span class="sxs-lookup"><span data-stu-id="d333f-202">Change the **Project Url** to use the **SSL URL** and save the page (Control S).</span></span>
   
    ![enable SSL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/rrr1.png)
7. <span data-ttu-id="d333f-204">Verify that Internet Explorer is the browser that Visual Studio launches, as shown in the image below:</span><span class="sxs-lookup"><span data-stu-id="d333f-204">Verify that Internet Explorer is the browser that Visual Studio launches, as shown in the image below:</span></span>
   
    ![default browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/ss12.PNG)
   
    <span data-ttu-id="d333f-206">The browser selector lets you specify the browser Visual Studio launches.</span><span class="sxs-lookup"><span data-stu-id="d333f-206">The browser selector lets you specify the browser Visual Studio launches.</span></span> <span data-ttu-id="d333f-207">You can select multiple browsers and have Visual Studio update each browser when you make changes.</span><span class="sxs-lookup"><span data-stu-id="d333f-207">You can select multiple browsers and have Visual Studio update each browser when you make changes.</span></span> <span data-ttu-id="d333f-208">For more information see [Using Browser Link in Visual Studio 2013](http://www.asp.net/visual-studio/overview/2013/using-browser-link).</span><span class="sxs-lookup"><span data-stu-id="d333f-208">For more information see [Using Browser Link in Visual Studio 2013](http://www.asp.net/visual-studio/overview/2013/using-browser-link).</span></span>
   
     ![browser selector](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/ss13.png)
8. <span data-ttu-id="d333f-210">Press CTRL+F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="d333f-210">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="d333f-211">Click **Yes** to start the process of trusting the self-signed certificate that IIS Express has generated.</span><span class="sxs-lookup"><span data-stu-id="d333f-211">Click **Yes** to start the process of trusting the self-signed certificate that IIS Express has generated.</span></span>
   
     ![instructions to trust the self-signed certificate that IIS Express has generated](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/ss26.PNG)
9. <span data-ttu-id="d333f-213">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing  **localhost**.</span><span class="sxs-lookup"><span data-stu-id="d333f-213">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing  **localhost**.</span></span>
   
     ![<span data-ttu-id="d333f-214">localhost IIS Express certificate warning</span><span class="sxs-lookup"><span data-stu-id="d333f-214">localhost IIS Express certificate warning</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/ss27.PNG)
10. <span data-ttu-id="d333f-215">IE shows the *Home* page and there are no SSL warnings.</span><span class="sxs-lookup"><span data-stu-id="d333f-215">IE shows the *Home* page and there are no SSL warnings.</span></span>
    
      ![IE with localhost SSL and no warnings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/ss28.PNG)
    
      <span data-ttu-id="d333f-217">Internet Explorer is a good choice when you're using SSL because it accepts the certificate and shows HTTPS content without a warning.</span><span class="sxs-lookup"><span data-stu-id="d333f-217">Internet Explorer is a good choice when you're using SSL because it accepts the certificate and shows HTTPS content without a warning.</span></span> <span data-ttu-id="d333f-218">Microsoft Edge and Google Chrome also accept the certificate.</span><span class="sxs-lookup"><span data-stu-id="d333f-218">Microsoft Edge and Google Chrome also accept the certificate.</span></span> <span data-ttu-id="d333f-219">Firefox uses its own certificate store, so it displays a warning.</span><span class="sxs-lookup"><span data-stu-id="d333f-219">Firefox uses its own certificate store, so it displays a warning.</span></span>
    
      ![FireFox Cert Warning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/ss30.PNG)

## <a name="add-a-database-to-the-application"></a><span data-ttu-id="d333f-221">Add a database to the application</span><span class="sxs-lookup"><span data-stu-id="d333f-221">Add a database to the application</span></span>
<span data-ttu-id="d333f-222">Next, you'll update the app to add the ability to display and update contacts and store the data in a database.</span><span class="sxs-lookup"><span data-stu-id="d333f-222">Next, you'll update the app to add the ability to display and update contacts and store the data in a database.</span></span> <span data-ttu-id="d333f-223">The app will use the Entity Framework (EF) to create the database and to read and update data.</span><span class="sxs-lookup"><span data-stu-id="d333f-223">The app will use the Entity Framework (EF) to create the database and to read and update data.</span></span>

### <a name="add-data-model-classes-for-the-contacts"></a><span data-ttu-id="d333f-224">Add data model classes for the contacts</span><span class="sxs-lookup"><span data-stu-id="d333f-224">Add data model classes for the contacts</span></span>
<span data-ttu-id="d333f-225">You begin by creating a simple data model in code.</span><span class="sxs-lookup"><span data-stu-id="d333f-225">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="d333f-226">In **Solution Explorer**, right-click the Models folder, click **Add**, and then **Class**.</span><span class="sxs-lookup"><span data-stu-id="d333f-226">In **Solution Explorer**, right-click the Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Add Class in Models folder context menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/rr5.png)
2. <span data-ttu-id="d333f-228">In the **Add New Item** dialog box, name the new class file *Contact.cs*, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d333f-228">In the **Add New Item** dialog box, name the new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Add New Item dialog box][adddb002]
3. <span data-ttu-id="d333f-230">Replace the contents of the Contact.cs file with the following code.</span><span class="sxs-lookup"><span data-stu-id="d333f-230">Replace the contents of the Contact.cs file with the following code.</span></span>
   
        using System.ComponentModel.DataAnnotations;
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
            {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                [DataType(DataType.EmailAddress)]
                public string Email { get; set; }
            }
        }
   <span data-ttu-id="d333f-231">The **Contact** class defines the data that you will store for each contact, plus a primary key, *ContactID*, that is needed by the database.</span><span class="sxs-lookup"><span data-stu-id="d333f-231">The **Contact** class defines the data that you will store for each contact, plus a primary key, *ContactID*, that is needed by the database.</span></span>

### <a name="create-web-pages-that-enable-app-users-to-work-with-the-contacts"></a><span data-ttu-id="d333f-232">Create web pages that enable app users to work with the contacts</span><span class="sxs-lookup"><span data-stu-id="d333f-232">Create web pages that enable app users to work with the contacts</span></span>
<span data-ttu-id="d333f-233">The ASP.NET MVC scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span><span class="sxs-lookup"><span data-stu-id="d333f-233">The ASP.NET MVC scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span> 

1. <span data-ttu-id="d333f-234">Build the project **(Ctrl+Shift+B)**.</span><span class="sxs-lookup"><span data-stu-id="d333f-234">Build the project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="d333f-235">(You must build the project before using the scaffolding mechanism.)</span><span class="sxs-lookup"><span data-stu-id="d333f-235">(You must build the project before using the scaffolding mechanism.)</span></span>
2. <span data-ttu-id="d333f-236">In **Solution Explorer**, right-click the Controllers folder and click **Add**, and then click **Controller**.</span><span class="sxs-lookup"><span data-stu-id="d333f-236">In **Solution Explorer**, right-click the Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Add Controller in Controllers folder context menu][addcode001]
3. <span data-ttu-id="d333f-238">In the **Add Scaffold** dialog box, select **MVC 5 Controller with views, using EF** and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d333f-238">In the **Add Scaffold** dialog box, select **MVC 5 Controller with views, using EF** and then click **Add**.</span></span>
   
    ![Add Scaffold dlg](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/rr6.png)
4. <span data-ttu-id="d333f-240">In the **Model class** dropdown box, select **Contact (ContactManager.Models)**.</span><span class="sxs-lookup"><span data-stu-id="d333f-240">In the **Model class** dropdown box, select **Contact (ContactManager.Models)**.</span></span> <span data-ttu-id="d333f-241">(See the image below.)</span><span class="sxs-lookup"><span data-stu-id="d333f-241">(See the image below.)</span></span>
5. <span data-ttu-id="d333f-242">In the **Data context class**, select **ApplicationDbContext (ContactManager.Models)**.</span><span class="sxs-lookup"><span data-stu-id="d333f-242">In the **Data context class**, select **ApplicationDbContext (ContactManager.Models)**.</span></span> <span data-ttu-id="d333f-243">The **ApplicationDbContext** will be used for both the membership DB and our contact data.</span><span class="sxs-lookup"><span data-stu-id="d333f-243">The **ApplicationDbContext** will be used for both the membership DB and our contact data.</span></span>

    ![New data ctx dlg](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/ss5.PNG)

1. <span data-ttu-id="d333f-245">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d333f-245">Click **Add**.</span></span>
   
   <span data-ttu-id="d333f-246">Visual Studio creates a controller with methods and views for CRUD database operations for **Contact** objects.</span><span class="sxs-lookup"><span data-stu-id="d333f-246">Visual Studio creates a controller with methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-the-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="d333f-247">Enable Migrations, create the database, add sample data and a data initializer</span><span class="sxs-lookup"><span data-stu-id="d333f-247">Enable Migrations, create the database, add sample data and a data initializer</span></span>
<span data-ttu-id="d333f-248">The next task is to enable the [Code First Migrations](http://msdn.microsoft.com/library/hh770484.aspx) feature in order to create database tables based on the data model that you created.</span><span class="sxs-lookup"><span data-stu-id="d333f-248">The next task is to enable the [Code First Migrations](http://msdn.microsoft.com/library/hh770484.aspx) feature in order to create database tables based on the data model that you created.</span></span>

1. <span data-ttu-id="d333f-249">In the **Tools** menu, select **NuGet Package Manager** and then **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="d333f-249">In the **Tools** menu, select **NuGet Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Package Manager Console in Tools menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/SS6.png)
2. <span data-ttu-id="d333f-251">In the **Package Manager Console** window, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="d333f-251">In the **Package Manager Console** window, enter the following command:</span></span>
   
        enable-migrations
   
    <span data-ttu-id="d333f-252">The **enable-migrations** command creates a *Migrations* folder, and it puts in that folder a *Configuration.cs* file that you can edit to seed the database and configure Migrations.</span><span class="sxs-lookup"><span data-stu-id="d333f-252">The **enable-migrations** command creates a *Migrations* folder, and it puts in that folder a *Configuration.cs* file that you can edit to seed the database and configure Migrations.</span></span> 
3. <span data-ttu-id="d333f-253">In the **Package Manager Console** window, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="d333f-253">In the **Package Manager Console** window, enter the following command:</span></span>
   
        add-migration Initial

    <span data-ttu-id="d333f-254">The **add-migration Initial** command generates a file named **&lt;date_stamp&gt;Initial** in the *Migrations* folder.</span><span class="sxs-lookup"><span data-stu-id="d333f-254">The **add-migration Initial** command generates a file named **&lt;date_stamp&gt;Initial** in the *Migrations* folder.</span></span> <span data-ttu-id="d333f-255">The code in this file creates the database tables.</span><span class="sxs-lookup"><span data-stu-id="d333f-255">The code in this file creates the database tables.</span></span> <span data-ttu-id="d333f-256">The first parameter ( **Initial** ) is used to create the name of the file.</span><span class="sxs-lookup"><span data-stu-id="d333f-256">The first parameter ( **Initial** ) is used to create the name of the file.</span></span> <span data-ttu-id="d333f-257">You can see the new class files in **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d333f-257">You can see the new class files in **Solution Explorer**.</span></span>

    <span data-ttu-id="d333f-258">In the **Initial** class, the **Up** method creates the Contacts table, and the **Down** method (used when you want to return to the previous state) drops it.</span><span class="sxs-lookup"><span data-stu-id="d333f-258">In the **Initial** class, the **Up** method creates the Contacts table, and the **Down** method (used when you want to return to the previous state) drops it.</span></span>

1. <span data-ttu-id="d333f-259">Open the *Migrations\Configuration.cs* file.</span><span class="sxs-lookup"><span data-stu-id="d333f-259">Open the *Migrations\Configuration.cs* file.</span></span> 
2. <span data-ttu-id="d333f-260">Add the following `using` statement.</span><span class="sxs-lookup"><span data-stu-id="d333f-260">Add the following `using` statement.</span></span> 
   
         using ContactManager.Models;
3. <span data-ttu-id="d333f-261">Replace the *Seed* method with the following code:</span><span class="sxs-lookup"><span data-stu-id="d333f-261">Replace the *Seed* method with the following code:</span></span>
   
        protected override void Seed(ContactManager.Models.ApplicationDbContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                }
                );
        }
   
    <span data-ttu-id="d333f-262">This code initializes (seeds) the database with contact information.</span><span class="sxs-lookup"><span data-stu-id="d333f-262">This code initializes (seeds) the database with contact information.</span></span> <span data-ttu-id="d333f-263">For more information on seeding the database, see [Seeding and Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="d333f-263">For more information on seeding the database, see [Seeding and Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span> <span data-ttu-id="d333f-264">Build the project to verify there are no compile errors.</span><span class="sxs-lookup"><span data-stu-id="d333f-264">Build the project to verify there are no compile errors.</span></span>
4. <span data-ttu-id="d333f-265">In the **Package Manager Console** enter the command:</span><span class="sxs-lookup"><span data-stu-id="d333f-265">In the **Package Manager Console** enter the command:</span></span>
   
        update-database
   
    ![Package Manager Console commands][addcode009]
   
    <span data-ttu-id="d333f-267">The **update-database** runs the first migration which creates the database.</span><span class="sxs-lookup"><span data-stu-id="d333f-267">The **update-database** runs the first migration which creates the database.</span></span> <span data-ttu-id="d333f-268">By default, the database is created as a SQL Server Express LocalDB database.</span><span class="sxs-lookup"><span data-stu-id="d333f-268">By default, the database is created as a SQL Server Express LocalDB database.</span></span> 
5. <span data-ttu-id="d333f-269">Press CTRL+F5 to run the application, and then click the **CM Demo** link; or navigate to https://localhost:(port#)/Cm.</span><span class="sxs-lookup"><span data-stu-id="d333f-269">Press CTRL+F5 to run the application, and then click the **CM Demo** link; or navigate to https://localhost:(port#)/Cm.</span></span> 
   
    <span data-ttu-id="d333f-270">The application shows the seed data and provides edit, details and delete links.</span><span class="sxs-lookup"><span data-stu-id="d333f-270">The application shows the seed data and provides edit, details and delete links.</span></span> <span data-ttu-id="d333f-271">You can create, edit, delete and view data.</span><span class="sxs-lookup"><span data-stu-id="d333f-271">You can create, edit, delete and view data.</span></span>
   
    ![MVC view of data][rx2]

## <a name="add-an-oauth2-provider"></a><span data-ttu-id="d333f-273">Add an OAuth2 Provider</span><span class="sxs-lookup"><span data-stu-id="d333f-273">Add an OAuth2 Provider</span></span>
> [!NOTE]
> <span data-ttu-id="d333f-274">For detailed instructions on how to use the Google and Facebook developer portal sites, this tutorial links to tutorials on the ASP.NET site.</span><span class="sxs-lookup"><span data-stu-id="d333f-274">For detailed instructions on how to use the Google and Facebook developer portal sites, this tutorial links to tutorials on the ASP.NET site.</span></span> <span data-ttu-id="d333f-275">However, Google and Facebook change their sites more frequently than those tutorials are updated, and they are now out of date.</span><span class="sxs-lookup"><span data-stu-id="d333f-275">However, Google and Facebook change their sites more frequently than those tutorials are updated, and they are now out of date.</span></span> <span data-ttu-id="d333f-276">If you have trouble following the directions, see the featured Disqus comment at the end of this tutorial for a list of what has changed.</span><span class="sxs-lookup"><span data-stu-id="d333f-276">If you have trouble following the directions, see the featured Disqus comment at the end of this tutorial for a list of what has changed.</span></span> 
> 
> 

<span data-ttu-id="d333f-277">[OAuth](http://oauth.net/ "http://oauth.net/") is an open protocol that allows secure authorization in a simple and standard method from web, mobile, and desktop applications.</span><span class="sxs-lookup"><span data-stu-id="d333f-277">[OAuth](http://oauth.net/ "http://oauth.net/") is an open protocol that allows secure authorization in a simple and standard method from web, mobile, and desktop applications.</span></span> <span data-ttu-id="d333f-278">The ASP.NET MVC internet template uses OAuth to expose Facebook, Twitter, Google and Microsoft as authentication providers.</span><span class="sxs-lookup"><span data-stu-id="d333f-278">The ASP.NET MVC internet template uses OAuth to expose Facebook, Twitter, Google and Microsoft as authentication providers.</span></span> <span data-ttu-id="d333f-279">Although this tutorial uses only Google as the authentication provider, you can easily modify the code to use any of these providers.</span><span class="sxs-lookup"><span data-stu-id="d333f-279">Although this tutorial uses only Google as the authentication provider, you can easily modify the code to use any of these providers.</span></span> <span data-ttu-id="d333f-280">The steps to implement other providers are very similar to the steps you see in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d333f-280">The steps to implement other providers are very similar to the steps you see in this tutorial.</span></span> <span data-ttu-id="d333f-281">To use Facebook as an authentication provider, see [MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on ](http://www.asp.net/mvc/tutorials/mvc-5/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on).</span><span class="sxs-lookup"><span data-stu-id="d333f-281">To use Facebook as an authentication provider, see [MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on ](http://www.asp.net/mvc/tutorials/mvc-5/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on).</span></span>

<span data-ttu-id="d333f-282">In addition to authentication, this tutorial uses roles to implement authorization.</span><span class="sxs-lookup"><span data-stu-id="d333f-282">In addition to authentication, this tutorial uses roles to implement authorization.</span></span> <span data-ttu-id="d333f-283">Only those users that you add to the *canEdit* role are able to change data (that is, create, edit, or delete contacts).</span><span class="sxs-lookup"><span data-stu-id="d333f-283">Only those users that you add to the *canEdit* role are able to change data (that is, create, edit, or delete contacts).</span></span>

1. <span data-ttu-id="d333f-284">Follow the instructions in [MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on ](http://www.asp.net/mvc/tutorials/mvc-5/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on#goog)  under **Creating a Google app for OAuth 2 to set up a Google app for OAuth2**.</span><span class="sxs-lookup"><span data-stu-id="d333f-284">Follow the instructions in [MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on ](http://www.asp.net/mvc/tutorials/mvc-5/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on#goog)  under **Creating a Google app for OAuth 2 to set up a Google app for OAuth2**.</span></span>
2. <span data-ttu-id="d333f-285">Run and test the app to verify that you can log on using Google authentication.</span><span class="sxs-lookup"><span data-stu-id="d333f-285">Run and test the app to verify that you can log on using Google authentication.</span></span>
3. <span data-ttu-id="d333f-286">If you want to create social login buttons with provider-specific icons, see [Pretty social login buttons for ASP.NET MVC 5](http://www.jerriepelser.com/blog/pretty-social-login-buttons-for-asp-net-mvc-5)</span><span class="sxs-lookup"><span data-stu-id="d333f-286">If you want to create social login buttons with provider-specific icons, see [Pretty social login buttons for ASP.NET MVC 5](http://www.jerriepelser.com/blog/pretty-social-login-buttons-for-asp-net-mvc-5)</span></span>

## <a name="using-the-membership-api"></a><span data-ttu-id="d333f-287">Using the Membership API</span><span class="sxs-lookup"><span data-stu-id="d333f-287">Using the Membership API</span></span>
<span data-ttu-id="d333f-288">In this section you will add a local user and the *canEdit* role to the membership database.</span><span class="sxs-lookup"><span data-stu-id="d333f-288">In this section you will add a local user and the *canEdit* role to the membership database.</span></span> <span data-ttu-id="d333f-289">Only those users in the *canEdit* role will be able to edit data.</span><span class="sxs-lookup"><span data-stu-id="d333f-289">Only those users in the *canEdit* role will be able to edit data.</span></span> <span data-ttu-id="d333f-290">A best practice is to name roles by the actions they can perform, so *canEdit* is preferred over a role called *admin*. When your application evolves, you can add new roles such as *canDeleteMembers* rather than the less descriptive *superAdmin*.</span><span class="sxs-lookup"><span data-stu-id="d333f-290">A best practice is to name roles by the actions they can perform, so *canEdit* is preferred over a role called *admin*. When your application evolves, you can add new roles such as *canDeleteMembers* rather than the less descriptive *superAdmin*.</span></span>

1. <span data-ttu-id="d333f-291">Open the *migrations\configuration.cs* file and add the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="d333f-291">Open the *migrations\configuration.cs* file and add the following `using` statements:</span></span>
   
        using Microsoft.AspNet.Identity;
        using Microsoft.AspNet.Identity.EntityFramework;
2. <span data-ttu-id="d333f-292">Add the following **AddUserAndRole** method to the class:</span><span class="sxs-lookup"><span data-stu-id="d333f-292">Add the following **AddUserAndRole** method to the class:</span></span>
   
        bool AddUserAndRole(ContactManager.Models.ApplicationDbContext context)
        {
            IdentityResult ir;
            var rm = new RoleManager<IdentityRole>
                (new RoleStore<IdentityRole>(context));
            ir = rm.Create(new IdentityRole("canEdit"));
            var um = new UserManager<ApplicationUser>(
                new UserStore<ApplicationUser>(context));
            var user = new ApplicationUser()
            {
                UserName = "user1@contoso.com",
            };
            ir = um.Create(user, "P_assw0rd1");
            if (ir.Succeeded == false)
                return ir.Succeeded;
            ir = um.AddToRole(user.Id, "canEdit");
            return ir.Succeeded;
        }
3. <span data-ttu-id="d333f-293">Call the new method from the **Seed** method:</span><span class="sxs-lookup"><span data-stu-id="d333f-293">Call the new method from the **Seed** method:</span></span>
   
        protected override void Seed(ContactManager.Models.ApplicationDbContext context)
        {
            AddUserAndRole(context);
            context.Contacts.AddOrUpdate(p => p.Name,
                // Code removed for brevity
        }
   
    <span data-ttu-id="d333f-294">The following images shows the changes to *Seed* method:</span><span class="sxs-lookup"><span data-stu-id="d333f-294">The following images shows the changes to *Seed* method:</span></span>
   
    ![code image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/ss24.PNG)
   
    <span data-ttu-id="d333f-296">This code creates a new role called *canEdit*, creates a new local user *user1@contoso.com*, and adds *user1@contoso.com* to the *canEdit* role.</span><span class="sxs-lookup"><span data-stu-id="d333f-296">This code creates a new role called *canEdit*, creates a new local user *user1@contoso.com*, and adds *user1@contoso.com* to the *canEdit* role.</span></span> <span data-ttu-id="d333f-297">For more information, see the [ASP.NET Identity tutorials](http://www.asp.net/identity/overview/features-api) on the ASP.NET site.</span><span class="sxs-lookup"><span data-stu-id="d333f-297">For more information, see the [ASP.NET Identity tutorials](http://www.asp.net/identity/overview/features-api) on the ASP.NET site.</span></span>

## <a name="use-temporary-code-to-add-new-social-login-users-to-the-canedit-role"></a><span data-ttu-id="d333f-298">Use Temporary Code to Add New Social Login Users to the canEdit Role</span><span class="sxs-lookup"><span data-stu-id="d333f-298">Use Temporary Code to Add New Social Login Users to the canEdit Role</span></span>
<span data-ttu-id="d333f-299">In this section you will temporarily modify the **ExternalLoginConfirmation** method in the Account controller to add new users registering with an OAuth provider to the *canEdit* role.</span><span class="sxs-lookup"><span data-stu-id="d333f-299">In this section you will temporarily modify the **ExternalLoginConfirmation** method in the Account controller to add new users registering with an OAuth provider to the *canEdit* role.</span></span> <span data-ttu-id="d333f-300">We hope to provide a tool similar to [WSAT](http://msdn.microsoft.com/library/ms228053.aspx) in the future which will allow you to create and edit user accounts and roles.</span><span class="sxs-lookup"><span data-stu-id="d333f-300">We hope to provide a tool similar to [WSAT](http://msdn.microsoft.com/library/ms228053.aspx) in the future which will allow you to create and edit user accounts and roles.</span></span> <span data-ttu-id="d333f-301">Until then, you can accomplish the same function by using temporary code.</span><span class="sxs-lookup"><span data-stu-id="d333f-301">Until then, you can accomplish the same function by using temporary code.</span></span>

1. <span data-ttu-id="d333f-302">Open the **Controllers\AccountController.cs** file and navigate to the **ExternalLoginConfirmation** method.</span><span class="sxs-lookup"><span data-stu-id="d333f-302">Open the **Controllers\AccountController.cs** file and navigate to the **ExternalLoginConfirmation** method.</span></span>
2. <span data-ttu-id="d333f-303">Add the following call to **AddToRoleAsync** just before the **SignInAsync** call.</span><span class="sxs-lookup"><span data-stu-id="d333f-303">Add the following call to **AddToRoleAsync** just before the **SignInAsync** call.</span></span>
   
        await UserManager.AddToRoleAsync(user.Id, "canEdit");
   
   <span data-ttu-id="d333f-304">The code above adds the newly registered user to the "canEdit" role, which gives them access to action methods that change (edit) data.</span><span class="sxs-lookup"><span data-stu-id="d333f-304">The code above adds the newly registered user to the "canEdit" role, which gives them access to action methods that change (edit) data.</span></span> <span data-ttu-id="d333f-305">The following snippet shows the new line of code in context.</span><span class="sxs-lookup"><span data-stu-id="d333f-305">The following snippet shows the new line of code in context.</span></span>
   
          // POST: /Account/ExternalLoginConfirmation
          [HttpPost]
          [AllowAnonymous]
          [ValidateAntiForgeryToken]
          public async Task ExternalLoginConfirmation(ExternalLoginConfirmationViewModel model, string returnUrl)
          {
             if (User.Identity.IsAuthenticated)
             {
                return RedirectToAction("Index", "Manage");
             }
             if (ModelState.IsValid)
             {
                // Get the information about the user from the external login provider
                var info = await AuthenticationManager.GetExternalLoginInfoAsync();
                if (info == null)
                {
                   return View("ExternalLoginFailure");
                }
                var user = new ApplicationUser { UserName = model.Email, Email = model.Email };
                var result = await UserManager.CreateAsync(user);
                if (result.Succeeded)
                {
                   result = await UserManager.AddLoginAsync(user.Id, info.Login);
                   if (result.Succeeded)
                   {
                      await UserManager.AddToRoleAsync(user.Id, "canEdit");
                      await SignInManager.SignInAsync(user, isPersistent: false, rememberBrowser: false);
                      return RedirectToLocal(returnUrl);
                   }
                }
                AddErrors(result);
             }
             ViewBag.ReturnUrl = returnUrl;
             return View(model);
          }

<span data-ttu-id="d333f-306">Later in the tutorial you will deploy the application to Azure, where you will log-on with Google or another third party authentication provider.</span><span class="sxs-lookup"><span data-stu-id="d333f-306">Later in the tutorial you will deploy the application to Azure, where you will log-on with Google or another third party authentication provider.</span></span> <span data-ttu-id="d333f-307">This will add your newly registered account to the *canEdit* role.</span><span class="sxs-lookup"><span data-stu-id="d333f-307">This will add your newly registered account to the *canEdit* role.</span></span> <span data-ttu-id="d333f-308">Anyone who finds your web app's URL and has a Google ID can then register and update your database.</span><span class="sxs-lookup"><span data-stu-id="d333f-308">Anyone who finds your web app's URL and has a Google ID can then register and update your database.</span></span> <span data-ttu-id="d333f-309">To prevent other people from doing that, you can stop the site.</span><span class="sxs-lookup"><span data-stu-id="d333f-309">To prevent other people from doing that, you can stop the site.</span></span> <span data-ttu-id="d333f-310">You'll be able to verify who is in the *canEdit* role by examining the database.</span><span class="sxs-lookup"><span data-stu-id="d333f-310">You'll be able to verify who is in the *canEdit* role by examining the database.</span></span>

<span data-ttu-id="d333f-311">In the **Package Manager Console** hit the up arrow key to bring up the following command:</span><span class="sxs-lookup"><span data-stu-id="d333f-311">In the **Package Manager Console** hit the up arrow key to bring up the following command:</span></span>

        Update-Database

<span data-ttu-id="d333f-312">The **Update-Database** command runs the **Seed** method, and that runs the **AddUserAndRole** method you added earlier.</span><span class="sxs-lookup"><span data-stu-id="d333f-312">The **Update-Database** command runs the **Seed** method, and that runs the **AddUserAndRole** method you added earlier.</span></span> <span data-ttu-id="d333f-313">The **AddUserAndRole** method creates the user *user1@contoso.com* and adds her to the *canEdit* role.</span><span class="sxs-lookup"><span data-stu-id="d333f-313">The **AddUserAndRole** method creates the user *user1@contoso.com* and adds her to the *canEdit* role.</span></span>

## <a name="protect-the-application-with-ssl-and-the-authorize-attribute"></a><span data-ttu-id="d333f-314">Protect the Application with SSL and the Authorize Attribute</span><span class="sxs-lookup"><span data-stu-id="d333f-314">Protect the Application with SSL and the Authorize Attribute</span></span>
<span data-ttu-id="d333f-315">In this section you apply the [Authorize](http://msdn.microsoft.com/library/system.web.mvc.authorizeattribute.aspx) attribute to restrict access to the action methods.</span><span class="sxs-lookup"><span data-stu-id="d333f-315">In this section you apply the [Authorize](http://msdn.microsoft.com/library/system.web.mvc.authorizeattribute.aspx) attribute to restrict access to the action methods.</span></span> <span data-ttu-id="d333f-316">Anonymous users will be able to view only the **Index** action method of the home controller.</span><span class="sxs-lookup"><span data-stu-id="d333f-316">Anonymous users will be able to view only the **Index** action method of the home controller.</span></span> <span data-ttu-id="d333f-317">Registered users will be able to see contact data (The **Index** and **Details** pages of the Cm controller), the About page, and the Contact page.</span><span class="sxs-lookup"><span data-stu-id="d333f-317">Registered users will be able to see contact data (The **Index** and **Details** pages of the Cm controller), the About page, and the Contact page.</span></span> <span data-ttu-id="d333f-318">Only users in the *canEdit* role will be able to access action methods that change data.</span><span class="sxs-lookup"><span data-stu-id="d333f-318">Only users in the *canEdit* role will be able to access action methods that change data.</span></span>

1. <span data-ttu-id="d333f-319">Open the *App_Start\FilterConfig.cs* file and replace the *RegisterGlobalFilters* method with the following (which adds the two filters):</span><span class="sxs-lookup"><span data-stu-id="d333f-319">Open the *App_Start\FilterConfig.cs* file and replace the *RegisterGlobalFilters* method with the following (which adds the two filters):</span></span>
   
        public static void RegisterGlobalFilters(GlobalFilterCollection filters)
        {
            filters.Add(new HandleErrorAttribute());
            filters.Add(new System.Web.Mvc.AuthorizeAttribute());
            filters.Add(new RequireHttpsAttribute());
        }
   
    <span data-ttu-id="d333f-320">This code adds the [Authorize](http://msdn.microsoft.com/library/system.web.mvc.authorizeattribute.aspx) filter and the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span><span class="sxs-lookup"><span data-stu-id="d333f-320">This code adds the [Authorize](http://msdn.microsoft.com/library/system.web.mvc.authorizeattribute.aspx) filter and the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="d333f-321">The [Authorize](http://msdn.microsoft.com/library/system.web.mvc.authorizeattribute.aspx) filter prevents anonymous users from accessing any methods in the application.</span><span class="sxs-lookup"><span data-stu-id="d333f-321">The [Authorize](http://msdn.microsoft.com/library/system.web.mvc.authorizeattribute.aspx) filter prevents anonymous users from accessing any methods in the application.</span></span> <span data-ttu-id="d333f-322">You will use the [AllowAnonymous](http://blogs.msdn.com/b/rickandy/archive/2012/03/23/securing-your-asp-net-mvc-4-app-and-the-new-allowanonymous-attribute.aspx) attribute to opt out of the authorization requirement in a couple methods, so anonymous users can log in and can view the home page.</span><span class="sxs-lookup"><span data-stu-id="d333f-322">You will use the [AllowAnonymous](http://blogs.msdn.com/b/rickandy/archive/2012/03/23/securing-your-asp-net-mvc-4-app-and-the-new-allowanonymous-attribute.aspx) attribute to opt out of the authorization requirement in a couple methods, so anonymous users can log in and can view the home page.</span></span> <span data-ttu-id="d333f-323">The  [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) requires that all access to the web app be through HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d333f-323">The  [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) requires that all access to the web app be through HTTPS.</span></span>
   
    <span data-ttu-id="d333f-324">An alternative approach is to add the [Authorize](http://msdn.microsoft.com/library/system.web.mvc.authorizeattribute.aspx) attribute and the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to each controller, but it's considered a security best practice to apply them to the entire application.</span><span class="sxs-lookup"><span data-stu-id="d333f-324">An alternative approach is to add the [Authorize](http://msdn.microsoft.com/library/system.web.mvc.authorizeattribute.aspx) attribute and the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to each controller, but it's considered a security best practice to apply them to the entire application.</span></span> <span data-ttu-id="d333f-325">By adding them globally, every new controller and action method you add is automatically protected -- you don't need to remember to apply them.</span><span class="sxs-lookup"><span data-stu-id="d333f-325">By adding them globally, every new controller and action method you add is automatically protected -- you don't need to remember to apply them.</span></span> <span data-ttu-id="d333f-326">For more information see [Securing your ASP.NET MVC  App and the new AllowAnonymous Attribute](http://blogs.msdn.com/b/rickandy/archive/2012/03/23/securing-your-asp-net-mvc-4-app-and-the-new-allowanonymous-attribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="d333f-326">For more information see [Securing your ASP.NET MVC  App and the new AllowAnonymous Attribute](http://blogs.msdn.com/b/rickandy/archive/2012/03/23/securing-your-asp-net-mvc-4-app-and-the-new-allowanonymous-attribute.aspx).</span></span> 
2. <span data-ttu-id="d333f-327">Add the [AllowAnonymous](http://blogs.msdn.com/b/rickandy/archive/2012/03/23/securing-your-asp-net-mvc-4-app-and-the-new-allowanonymous-attribute.aspx) attribute to the **Index** method of the Home controller.</span><span class="sxs-lookup"><span data-stu-id="d333f-327">Add the [AllowAnonymous](http://blogs.msdn.com/b/rickandy/archive/2012/03/23/securing-your-asp-net-mvc-4-app-and-the-new-allowanonymous-attribute.aspx) attribute to the **Index** method of the Home controller.</span></span> <span data-ttu-id="d333f-328">The [AllowAnonymous](http://blogs.msdn.com/b/rickandy/archive/2012/03/23/securing-your-asp-net-mvc-4-app-and-the-new-allowanonymous-attribute.aspx) attribute enables you to white-list the methods you want to opt out of authorization.</span><span class="sxs-lookup"><span data-stu-id="d333f-328">The [AllowAnonymous](http://blogs.msdn.com/b/rickandy/archive/2012/03/23/securing-your-asp-net-mvc-4-app-and-the-new-allowanonymous-attribute.aspx) attribute enables you to white-list the methods you want to opt out of authorization.</span></span> 
   
        public class HomeController : Controller
        {
          [AllowAnonymous]
          public ActionResult Index()
          {
             return View();
          }
   
    <span data-ttu-id="d333f-329">If you do a global search for *AllowAnonymous*, you'll see that it is used in the login and registration methods of the Account controller.</span><span class="sxs-lookup"><span data-stu-id="d333f-329">If you do a global search for *AllowAnonymous*, you'll see that it is used in the login and registration methods of the Account controller.</span></span>
3. <span data-ttu-id="d333f-330">In *ContactsController.cs*, add `[Authorize(Roles = "canEdit")]` to the HttpGet and HttpPost methods that change data (Create, Edit, Delete, every action method except Index and Details) in the *Cm* controller.</span><span class="sxs-lookup"><span data-stu-id="d333f-330">In *ContactsController.cs*, add `[Authorize(Roles = "canEdit")]` to the HttpGet and HttpPost methods that change data (Create, Edit, Delete, every action method except Index and Details) in the *Cm* controller.</span></span> <span data-ttu-id="d333f-331">A portion of the completed code is shown below:</span><span class="sxs-lookup"><span data-stu-id="d333f-331">A portion of the completed code is shown below:</span></span> 
   
        // GET: Cm/Create
        [Authorize(Roles = "canEdit")]
        public ActionResult Create()
        {
           return View(new Contact { Address = "123 N 456 W",
            City="Great Falls", Email = "ab@cd.com", Name="Joe Smith", State="MT",
           Zip = "59405"});
        }
        // POST: Cm/Create
        // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
        // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
        [HttpPost]
        [ValidateAntiForgeryToken]
         [Authorize(Roles = "canEdit")]
        public ActionResult Create([Bind(Include = "ContactId,Name,Address,City,State,Zip,Email")] Contact contact)
        {
            if (ModelState.IsValid)
            {
                db.Contacts.Add(contact);
                db.SaveChanges();
                return RedirectToAction("Index");
            }
            return View(contact);
        }
        // GET: Cm/Edit/5
        [Authorize(Roles = "canEdit")]
        public ActionResult Edit(int? id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
            Contact contact = db.Contacts.Find(id);
            if (contact == null)
            {
                return HttpNotFound();
            }
            return View(contact);
        }
4. <span data-ttu-id="d333f-332">Press CTRL+F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="d333f-332">Press CTRL+F5 to run the application.</span></span>
5. <span data-ttu-id="d333f-333">If you are still logged in from a previous session, hit the **Log out** link.</span><span class="sxs-lookup"><span data-stu-id="d333f-333">If you are still logged in from a previous session, hit the **Log out** link.</span></span>
6. <span data-ttu-id="d333f-334">Click on the **About** or **Contact** links.</span><span class="sxs-lookup"><span data-stu-id="d333f-334">Click on the **About** or **Contact** links.</span></span> <span data-ttu-id="d333f-335">You are redirected to the login page because anonymous users cannot view those pages.</span><span class="sxs-lookup"><span data-stu-id="d333f-335">You are redirected to the login page because anonymous users cannot view those pages.</span></span>
7. <span data-ttu-id="d333f-336">Click the **Register as a new user** link and add a local user with email *joe@contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="d333f-336">Click the **Register as a new user** link and add a local user with email *joe@contoso.com*.</span></span> <span data-ttu-id="d333f-337">Verify *Joe* can view the Home, About and Contact pages.</span><span class="sxs-lookup"><span data-stu-id="d333f-337">Verify *Joe* can view the Home, About and Contact pages.</span></span> 
   
    ![login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/ss14.PNG)
8. <span data-ttu-id="d333f-339">Click the *CM Demo* link and verify that you see the data.</span><span class="sxs-lookup"><span data-stu-id="d333f-339">Click the *CM Demo* link and verify that you see the data.</span></span>
9. <span data-ttu-id="d333f-340">Click an edit link on the page, you will be redirected to the login page (because a new local user is not added to the *canEdit* role).</span><span class="sxs-lookup"><span data-stu-id="d333f-340">Click an edit link on the page, you will be redirected to the login page (because a new local user is not added to the *canEdit* role).</span></span>
10. <span data-ttu-id="d333f-341">Log in as *user1@contoso.com* with password of "P_assw0rd1" (the "0" in "word" is a zero).</span><span class="sxs-lookup"><span data-stu-id="d333f-341">Log in as *user1@contoso.com* with password of "P_assw0rd1" (the "0" in "word" is a zero).</span></span> <span data-ttu-id="d333f-342">You are redirected to the edit page you previously selected.</span><span class="sxs-lookup"><span data-stu-id="d333f-342">You are redirected to the edit page you previously selected.</span></span> 
11.  <span data-ttu-id="d333f-343">If you can't log in with that account and password, try copying the password from the source code and pasting it.</span><span class="sxs-lookup"><span data-stu-id="d333f-343">If you can't log in with that account and password, try copying the password from the source code and pasting it.</span></span> <span data-ttu-id="d333f-344">If you still can't log in, check the **UserName** column of the **AspNetUsers** table to verify *user1@contoso.com* was added.</span><span class="sxs-lookup"><span data-stu-id="d333f-344">If you still can't log in, check the **UserName** column of the **AspNetUsers** table to verify *user1@contoso.com* was added.</span></span> 
12. <span data-ttu-id="d333f-345">Verify you can make data changes.</span><span class="sxs-lookup"><span data-stu-id="d333f-345">Verify you can make data changes.</span></span>

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="d333f-346">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="d333f-346">Deploy the app to Azure</span></span>
1. <span data-ttu-id="d333f-347">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="d333f-347">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
   
    ![Publish in project context menu][firsdeploy003]
   
    <span data-ttu-id="d333f-349">The **Publish Web** wizard opens.</span><span class="sxs-lookup"><span data-stu-id="d333f-349">The **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="d333f-350">Click the **Settings** tab on the left side of the **Publish Web** dialog box.</span><span class="sxs-lookup"><span data-stu-id="d333f-350">Click the **Settings** tab on the left side of the **Publish Web** dialog box.</span></span> 
3. <span data-ttu-id="d333f-351">Under **ApplicationDbContext**  select the database that you created when you created the project.</span><span class="sxs-lookup"><span data-stu-id="d333f-351">Under **ApplicationDbContext**  select the database that you created when you created the project.</span></span>
4. <span data-ttu-id="d333f-352">Under **ContactManagerContext**, select **Execute Code First Migrations**.</span><span class="sxs-lookup"><span data-stu-id="d333f-352">Under **ContactManagerContext**, select **Execute Code First Migrations**.</span></span>
   
    ![settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/rrc2.png)
5. <span data-ttu-id="d333f-354">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="d333f-354">Click **Publish**.</span></span>
6. <span data-ttu-id="d333f-355">Log in as *user1@contoso.com* (with password of "P_assw0rd1") and verify you can edit data.</span><span class="sxs-lookup"><span data-stu-id="d333f-355">Log in as *user1@contoso.com* (with password of "P_assw0rd1") and verify you can edit data.</span></span>
7. <span data-ttu-id="d333f-356">Log out.</span><span class="sxs-lookup"><span data-stu-id="d333f-356">Log out.</span></span>
8. <span data-ttu-id="d333f-357">Go to the [Google Developers Console](https://console.developers.google.com/) and on the **Credentials** tab update the redirect URIS and JavaScript Orgins to use the Azure URL.</span><span class="sxs-lookup"><span data-stu-id="d333f-357">Go to the [Google Developers Console](https://console.developers.google.com/) and on the **Credentials** tab update the redirect URIS and JavaScript Orgins to use the Azure URL.</span></span>
9. <span data-ttu-id="d333f-358">Log in using Google or Facebook.</span><span class="sxs-lookup"><span data-stu-id="d333f-358">Log in using Google or Facebook.</span></span> <span data-ttu-id="d333f-359">That will add the Google or Facebook account to the **canEdit** role.</span><span class="sxs-lookup"><span data-stu-id="d333f-359">That will add the Google or Facebook account to the **canEdit** role.</span></span> <span data-ttu-id="d333f-360">If you get an HTTP 400 error with the message *The redirect URI in the request: https://contactmanager{my version}.azurewebsites.net/signin-google did not match a registered redirect URI.*, you'll have to wait until the changes you made are propagated.</span><span class="sxs-lookup"><span data-stu-id="d333f-360">If you get an HTTP 400 error with the message *The redirect URI in the request: https://contactmanager{my version}.azurewebsites.net/signin-google did not match a registered redirect URI.*, you'll have to wait until the changes you made are propagated.</span></span> <span data-ttu-id="d333f-361">If you get this error after more than a few minutes, verify the URIs are correct.</span><span class="sxs-lookup"><span data-stu-id="d333f-361">If you get this error after more than a few minutes, verify the URIs are correct.</span></span>

### <a name="stop-the-web-app-to-prevent-other-people-from-registering"></a><span data-ttu-id="d333f-362">Stop the web app to prevent other people from registering</span><span class="sxs-lookup"><span data-stu-id="d333f-362">Stop the web app to prevent other people from registering</span></span>
1. <span data-ttu-id="d333f-363">In **Server Explorer**, navigate to **Azure > App Service > {your resource group} > {your web app}**.</span><span class="sxs-lookup"><span data-stu-id="d333f-363">In **Server Explorer**, navigate to **Azure > App Service > {your resource group} > {your web app}**.</span></span>
2. <span data-ttu-id="d333f-364">Right-click the web app and select **Stop**.</span><span class="sxs-lookup"><span data-stu-id="d333f-364">Right-click the web app and select **Stop**.</span></span> 
   
    <span data-ttu-id="d333f-365">Alternatively, from the [Azure Portal](https://portal.azure.com/), you can go to the web app's blade, then click the **Stop** icon at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="d333f-365">Alternatively, from the [Azure Portal](https://portal.azure.com/), you can go to the web app's blade, then click the **Stop** icon at the top of the blade.</span></span>
   
    ![stop web app portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/stopweb.png)

### <a name="remove-addtoroleasync-publish-and-test"></a><span data-ttu-id="d333f-367">Remove AddToRoleAsync, Publish, and Test</span><span class="sxs-lookup"><span data-stu-id="d333f-367">Remove AddToRoleAsync, Publish, and Test</span></span>
1. <span data-ttu-id="d333f-368">Comment out or remove the following code from the **ExternalLoginConfirmation** method in the Account controller:</span><span class="sxs-lookup"><span data-stu-id="d333f-368">Comment out or remove the following code from the **ExternalLoginConfirmation** method in the Account controller:</span></span>
   
        await UserManager.AddToRoleAsync(user.Id, "canEdit");
2. <span data-ttu-id="d333f-369">Build the project (which saves the file changes and verifies you don't have any compile errors).</span><span class="sxs-lookup"><span data-stu-id="d333f-369">Build the project (which saves the file changes and verifies you don't have any compile errors).</span></span>
3. <span data-ttu-id="d333f-370">Right-click the project in **Solution Explorer** and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="d333f-370">Right-click the project in **Solution Explorer** and select **Publish**.</span></span>
   
       ![Publish in project context menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/GS13publish.png)
4. <span data-ttu-id="d333f-371">Click the **Start Preview** button.</span><span class="sxs-lookup"><span data-stu-id="d333f-371">Click the **Start Preview** button.</span></span> <span data-ttu-id="d333f-372">Only the files that need to be updated are deployed.</span><span class="sxs-lookup"><span data-stu-id="d333f-372">Only the files that need to be updated are deployed.</span></span>
5. <span data-ttu-id="d333f-373">Start the web app from Visual Studio or from the Portal.</span><span class="sxs-lookup"><span data-stu-id="d333f-373">Start the web app from Visual Studio or from the Portal.</span></span> <span data-ttu-id="d333f-374">**You won't be able to publish while the web app is stopped**.</span><span class="sxs-lookup"><span data-stu-id="d333f-374">**You won't be able to publish while the web app is stopped**.</span></span>
   
    ![start web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/ss15.png)
6. <span data-ttu-id="d333f-376">Go back to Visual Studio and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="d333f-376">Go back to Visual Studio and click **Publish**.</span></span>
7. <span data-ttu-id="d333f-377">Your Azure App opens up in your default browser.</span><span class="sxs-lookup"><span data-stu-id="d333f-377">Your Azure App opens up in your default browser.</span></span> <span data-ttu-id="d333f-378">If you are logged in, log out so you can view the home page as an anonymous user.</span><span class="sxs-lookup"><span data-stu-id="d333f-378">If you are logged in, log out so you can view the home page as an anonymous user.</span></span>  
8. <span data-ttu-id="d333f-379">Click the **About** link.</span><span class="sxs-lookup"><span data-stu-id="d333f-379">Click the **About** link.</span></span> <span data-ttu-id="d333f-380">You'll be redirected to the Log in page.</span><span class="sxs-lookup"><span data-stu-id="d333f-380">You'll be redirected to the Log in page.</span></span>
9. <span data-ttu-id="d333f-381">Click the **Register** link on the Log in page and create local account.</span><span class="sxs-lookup"><span data-stu-id="d333f-381">Click the **Register** link on the Log in page and create local account.</span></span> <span data-ttu-id="d333f-382">We will use this local account to verify you can access the read only pages but you cannot access pages that change data (which are protected by the *canEdit* role).</span><span class="sxs-lookup"><span data-stu-id="d333f-382">We will use this local account to verify you can access the read only pages but you cannot access pages that change data (which are protected by the *canEdit* role).</span></span> <span data-ttu-id="d333f-383">Later on in the tutorial you will remove local account access.</span><span class="sxs-lookup"><span data-stu-id="d333f-383">Later on in the tutorial you will remove local account access.</span></span> 
   
    ![Register](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/ss16.PNG)
10. <span data-ttu-id="d333f-385">Verify that you can navigate to the *About* and *Contact* pages.</span><span class="sxs-lookup"><span data-stu-id="d333f-385">Verify that you can navigate to the *About* and *Contact* pages.</span></span>
    
     ![Log off](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/ss17.PNG)
11. <span data-ttu-id="d333f-387">Click the **CM Demo** link to navigate to the **Cm** controller.</span><span class="sxs-lookup"><span data-stu-id="d333f-387">Click the **CM Demo** link to navigate to the **Cm** controller.</span></span> <span data-ttu-id="d333f-388">Alternatively, you can append *Cm* to the URL.</span><span class="sxs-lookup"><span data-stu-id="d333f-388">Alternatively, you can append *Cm* to the URL.</span></span> 
    
     ![CM page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/rrr4.png)
12. <span data-ttu-id="d333f-390">Click an Edit link.</span><span class="sxs-lookup"><span data-stu-id="d333f-390">Click an Edit link.</span></span> 
    
     <span data-ttu-id="d333f-391">You are redirected to the login page.</span><span class="sxs-lookup"><span data-stu-id="d333f-391">You are redirected to the login page.</span></span> 
13. <span data-ttu-id="d333f-392">Under **Use another service to log in**, Click Google or Facebook and log in with the account you previously registered.</span><span class="sxs-lookup"><span data-stu-id="d333f-392">Under **Use another service to log in**, Click Google or Facebook and log in with the account you previously registered.</span></span> <span data-ttu-id="d333f-393">(If you're working quickly and your session cookie has not timed out, you will be automatically logged in with the Google or Facebook account you previously used.)</span><span class="sxs-lookup"><span data-stu-id="d333f-393">(If you're working quickly and your session cookie has not timed out, you will be automatically logged in with the Google or Facebook account you previously used.)</span></span>
14. <span data-ttu-id="d333f-394">Verify that you can edit data while logged into that account.</span><span class="sxs-lookup"><span data-stu-id="d333f-394">Verify that you can edit data while logged into that account.</span></span>
    
     <span data-ttu-id="d333f-395">**Note:** You cannot log out of Google from this app and log into a different google account with the same browser.</span><span class="sxs-lookup"><span data-stu-id="d333f-395">**Note:** You cannot log out of Google from this app and log into a different google account with the same browser.</span></span> <span data-ttu-id="d333f-396">If you are using one browser, you will have to navigate to Google and log out. You can log on with another account from the same third party authenticator (such as Google) by using a different browser.</span><span class="sxs-lookup"><span data-stu-id="d333f-396">If you are using one browser, you will have to navigate to Google and log out. You can log on with another account from the same third party authenticator (such as Google) by using a different browser.</span></span>
    
     <span data-ttu-id="d333f-397">If you have not filled out the first and last name of your Google account information, a NullReferenceException will occur.</span><span class="sxs-lookup"><span data-stu-id="d333f-397">If you have not filled out the first and last name of your Google account information, a NullReferenceException will occur.</span></span>

## <a name="examine-the-sql-azure-db"></a><span data-ttu-id="d333f-398">Examine the SQL Azure DB</span><span class="sxs-lookup"><span data-stu-id="d333f-398">Examine the SQL Azure DB</span></span>
1. <span data-ttu-id="d333f-399">In **Server Explorer**, navigate to **Azure > SQL Databases > {your database}**</span><span class="sxs-lookup"><span data-stu-id="d333f-399">In **Server Explorer**, navigate to **Azure > SQL Databases > {your database}**</span></span>
2. <span data-ttu-id="d333f-400">Right click your database, and then select **Open in SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d333f-400">Right click your database, and then select **Open in SQL Server Object Explorer**.</span></span>
   
    ![open in SSOX](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/rrr12.png)
3. <span data-ttu-id="d333f-402">If you haven't connected to this database previously, you may be prompted to add a firewall rule to enable access for your current IP address.</span><span class="sxs-lookup"><span data-stu-id="d333f-402">If you haven't connected to this database previously, you may be prompted to add a firewall rule to enable access for your current IP address.</span></span> <span data-ttu-id="d333f-403">The IP address will be pre-filled.</span><span class="sxs-lookup"><span data-stu-id="d333f-403">The IP address will be pre-filled.</span></span> <span data-ttu-id="d333f-404">Simply click **Add Firewall Rule** to enable access.</span><span class="sxs-lookup"><span data-stu-id="d333f-404">Simply click **Add Firewall Rule** to enable access.</span></span>
   
    ![add firewall rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/addfirewallrule.png)
4. <span data-ttu-id="d333f-406">Log in to the database with the user name and password that you specified when you created the database server.</span><span class="sxs-lookup"><span data-stu-id="d333f-406">Log in to the database with the user name and password that you specified when you created the database server.</span></span> 
5. <span data-ttu-id="d333f-407">Right click the **AspNetUsers** table and select **View Data**.</span><span class="sxs-lookup"><span data-stu-id="d333f-407">Right click the **AspNetUsers** table and select **View Data**.</span></span>
   
    ![CM page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/rrr8.png)
6. <span data-ttu-id="d333f-409">Note the Id from the Google account you registered with to be in the **canEdit** role, and the Id of *user1@contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="d333f-409">Note the Id from the Google account you registered with to be in the **canEdit** role, and the Id of *user1@contoso.com*.</span></span> <span data-ttu-id="d333f-410">These should be the only users in the **canEdit** role.</span><span class="sxs-lookup"><span data-stu-id="d333f-410">These should be the only users in the **canEdit** role.</span></span> <span data-ttu-id="d333f-411">(You'll verify that in the next step.)</span><span class="sxs-lookup"><span data-stu-id="d333f-411">(You'll verify that in the next step.)</span></span>
   
    ![CM page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/s2.png)
7. <span data-ttu-id="d333f-413">In **SQL Server Object Explorer**, right click on **AspNetUserRoles** and select **View Data**.</span><span class="sxs-lookup"><span data-stu-id="d333f-413">In **SQL Server Object Explorer**, right click on **AspNetUserRoles** and select **View Data**.</span></span>
   
    ![CM page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/rs1.png)
8. <span data-ttu-id="d333f-415">Verify that the **UserId** is from *user1@contoso.com* and the Google account you registered.</span><span class="sxs-lookup"><span data-stu-id="d333f-415">Verify that the **UserId** is from *user1@contoso.com* and the Google account you registered.</span></span> 

## <a name="troubleshooting"></a><span data-ttu-id="d333f-416">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="d333f-416">Troubleshooting</span></span>
<span data-ttu-id="d333f-417">If you run into problems, here are some suggestions for what to try.</span><span class="sxs-lookup"><span data-stu-id="d333f-417">If you run into problems, here are some suggestions for what to try.</span></span>

* <span data-ttu-id="d333f-418">Errors provisioning SQL Database - Make sure you have the current SDK installed.</span><span class="sxs-lookup"><span data-stu-id="d333f-418">Errors provisioning SQL Database - Make sure you have the current SDK installed.</span></span> <span data-ttu-id="d333f-419">Versions before 2.8.1 have a bug that in some scenarios causes errors when VS tries to create the database server or the database.</span><span class="sxs-lookup"><span data-stu-id="d333f-419">Versions before 2.8.1 have a bug that in some scenarios causes errors when VS tries to create the database server or the database.</span></span>
* <span data-ttu-id="d333f-420">Error message "operation is not supported for your subscription offer type" when creating Azure resources - Same as above.</span><span class="sxs-lookup"><span data-stu-id="d333f-420">Error message "operation is not supported for your subscription offer type" when creating Azure resources - Same as above.</span></span>
* <span data-ttu-id="d333f-421">Errors when deploying - Consider going through the [basic ASP.NET deployment](app-service-web-get-started-dotnet.md) article.</span><span class="sxs-lookup"><span data-stu-id="d333f-421">Errors when deploying - Consider going through the [basic ASP.NET deployment](app-service-web-get-started-dotnet.md) article.</span></span> <span data-ttu-id="d333f-422">That deployment scenario is simpler and if you have the same problem there it may be easier to isolate.</span><span class="sxs-lookup"><span data-stu-id="d333f-422">That deployment scenario is simpler and if you have the same problem there it may be easier to isolate.</span></span> <span data-ttu-id="d333f-423">For example, in some enterprise environments a corporate firewall may prevent Web Deploy from making the kinds of connections to Azure that it requires.</span><span class="sxs-lookup"><span data-stu-id="d333f-423">For example, in some enterprise environments a corporate firewall may prevent Web Deploy from making the kinds of connections to Azure that it requires.</span></span>
* <span data-ttu-id="d333f-424">No option to select connection string in the Publish Web wizard when you deploy - If you used a different method to create your Azure resources (for example, you are trying to deploy to  a web app and a SQL database created in the Portal), the SQL database may not be associated with the web app.</span><span class="sxs-lookup"><span data-stu-id="d333f-424">No option to select connection string in the Publish Web wizard when you deploy - If you used a different method to create your Azure resources (for example, you are trying to deploy to  a web app and a SQL database created in the Portal), the SQL database may not be associated with the web app.</span></span> <span data-ttu-id="d333f-425">The easiest solution is to create a new web app and database by using VS as shown in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="d333f-425">The easiest solution is to create a new web app and database by using VS as shown in the tutorial.</span></span> <span data-ttu-id="d333f-426">You don't have to start the tutorial over -- in the Publish Web wizard you can opt to create a new web app and you get the same Azure resource creation dialog that you get when you create the project.</span><span class="sxs-lookup"><span data-stu-id="d333f-426">You don't have to start the tutorial over -- in the Publish Web wizard you can opt to create a new web app and you get the same Azure resource creation dialog that you get when you create the project.</span></span>
* <span data-ttu-id="d333f-427">Directions for Google or Facebook developer portal are out of date - See the featured Disqus comment at the end of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d333f-427">Directions for Google or Facebook developer portal are out of date - See the featured Disqus comment at the end of this tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d333f-428">Next steps</span><span class="sxs-lookup"><span data-stu-id="d333f-428">Next steps</span></span>
<span data-ttu-id="d333f-429">You've created a basic ASP.NET MVC web application that authenticates users.</span><span class="sxs-lookup"><span data-stu-id="d333f-429">You've created a basic ASP.NET MVC web application that authenticates users.</span></span> <span data-ttu-id="d333f-430">For more information about common authentication tasks and how to keep sensitive data secure, see the following tutorials.</span><span class="sxs-lookup"><span data-stu-id="d333f-430">For more information about common authentication tasks and how to keep sensitive data secure, see the following tutorials.</span></span>

* [<span data-ttu-id="d333f-431">Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset</span><span class="sxs-lookup"><span data-stu-id="d333f-431">Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset</span></span>](http://www.asp.net/mvc/overview/getting-started/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset)
* [<span data-ttu-id="d333f-432">ASP.NET MVC 5 app with SMS and email Two-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="d333f-432">ASP.NET MVC 5 app with SMS and email Two-Factor Authentication</span></span>](http://www.asp.net/mvc/overview/getting-started/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication)
* [<span data-ttu-id="d333f-433">Best practices for deploying passwords and other sensitive data to ASP.NET and Azure</span><span class="sxs-lookup"><span data-stu-id="d333f-433">Best practices for deploying passwords and other sensitive data to ASP.NET and Azure</span></span>](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure) 
* <span data-ttu-id="d333f-434">[Create an ASP.NET MVC 5 App with Facebook and Google OAuth2](http://www.asp.net/mvc/tutorials/mvc-5/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on) This includes instructions on how to add profile data to the user registration DB and for detailed instructions on using Facebook as an authentication provider.</span><span class="sxs-lookup"><span data-stu-id="d333f-434">[Create an ASP.NET MVC 5 App with Facebook and Google OAuth2](http://www.asp.net/mvc/tutorials/mvc-5/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on) This includes instructions on how to add profile data to the user registration DB and for detailed instructions on using Facebook as an authentication provider.</span></span>
* [<span data-ttu-id="d333f-435">Getting Started with ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="d333f-435">Getting Started with ASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)

<span data-ttu-id="d333f-436">For a  more advanced tutorial about how to use the Entity Framework, see [Getting Started with EF and MVC](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="d333f-436">For a  more advanced tutorial about how to use the Entity Framework, see [Getting Started with EF and MVC](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

<span data-ttu-id="d333f-437">This tutorial was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="d333f-437">This tutorial was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="d333f-438">***Please leave feedback*** on what you liked or what you would like to see improved, not only about the tutorial itself but also about the products that it demonstrates.</span><span class="sxs-lookup"><span data-stu-id="d333f-438">***Please leave feedback*** on what you liked or what you would like to see improved, not only about the tutorial itself but also about the products that it demonstrates.</span></span> <span data-ttu-id="d333f-439">Your feedback will help us prioritize improvements.</span><span class="sxs-lookup"><span data-stu-id="d333f-439">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="d333f-440">You can also request and vote on new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span><span class="sxs-lookup"><span data-stu-id="d333f-440">You can also request and vote on new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="d333f-441">What's changed</span><span class="sxs-lookup"><span data-stu-id="d333f-441">What's changed</span></span>
* <span data-ttu-id="d333f-442">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d333f-442">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Using the Membership API]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update the Membership Database]:#ppd2

[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[deployapp11]: #bkmk_deploytowindowsazure11
[adddb]: #bkmk_addadatabase


<!-- images-->
[rx2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/rx2.png

[rx5]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/rx5.png
[rx6]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/rx6.png
[rx7]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/rx7.png
[rx8]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/rx8.png
[rx9]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/rx9.png

[rxb]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/rxb.png


[rxSSL]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/rxSSL.png

[rxNOT]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/rxNOT.png
[rxNOT2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/rxNOT2.png

[rxNOT]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/rxNOT.png
[rxNOT]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/rxNOT.png
[rxNOT]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/rxNOT.png
[rr1]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/rr1.png

[rxPrevDB]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/rxPrevDB.png

[rxWSnew]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/rxWSnew2.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/rxCreateWSwithDB.png

[setup007]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/dntutmobile-setup-azure-site-004.png

[newapp004]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/dntutmobile-createapp-004.png

[firsdeploy003]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/dntutmobile-deploy1-publish-001.png

[adddb002]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/dntutmobile-controller-add-context-menu.png

[addcode008]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/dntutmobile-migrations-package-manager-menu.png
[addcode009]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/dntutmobile-migrations-package-manager-console.png


[Important information about ASP.NET in Azure web apps]: #aspnetwindowsazureinfo
[Next steps]: #nextsteps

[ImportPublishSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database-vs2013/ImportPublishSettings.png














































