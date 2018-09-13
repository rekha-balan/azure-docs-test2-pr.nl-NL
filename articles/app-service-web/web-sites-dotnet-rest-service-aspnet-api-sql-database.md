---
title: Create a REST API in Azure with ASP.NET and SQL DB | Microsoft Docs
description: A tutorial that teaches you how to deploy an app that uses the ASP.NET Web API to an Azure web app by using Visual Studio.
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: ''
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 8313345574575a1143ed52cea971041adf891b4c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563900"
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="567cf-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="567cf-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="567cf-104">This tutorial shows how to deploy an ASP.NET web app to an [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using the Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="567cf-104">This tutorial shows how to deploy an ASP.NET web app to an [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using the Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="567cf-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, the SDK automatically installs Visual Studio 2013 for Web Express.</span><span class="sxs-lookup"><span data-stu-id="567cf-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, the SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="567cf-106">So you can start developing for Azure entirely for free.</span><span class="sxs-lookup"><span data-stu-id="567cf-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="567cf-107">This tutorial assumes that you have no prior experience using Azure.</span><span class="sxs-lookup"><span data-stu-id="567cf-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="567cf-108">On completing this tutorial, you'll have a simple web app up and running in the cloud.</span><span class="sxs-lookup"><span data-stu-id="567cf-108">On completing this tutorial, you'll have a simple web app up and running in the cloud.</span></span>

<span data-ttu-id="567cf-109">You'll learn:</span><span class="sxs-lookup"><span data-stu-id="567cf-109">You'll learn:</span></span>

* <span data-ttu-id="567cf-110">How to enable your machine for Azure development by installing the Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="567cf-110">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="567cf-111">How to create a Visual Studio ASP.NET MVC 5 project and publish it to an Azure app.</span><span class="sxs-lookup"><span data-stu-id="567cf-111">How to create a Visual Studio ASP.NET MVC 5 project and publish it to an Azure app.</span></span>
* <span data-ttu-id="567cf-112">How to use the ASP.NET Web API to enable Restful API calls.</span><span class="sxs-lookup"><span data-stu-id="567cf-112">How to use the ASP.NET Web API to enable Restful API calls.</span></span>
* <span data-ttu-id="567cf-113">How to use a SQL database to store data in Azure.</span><span class="sxs-lookup"><span data-stu-id="567cf-113">How to use a SQL database to store data in Azure.</span></span>
* <span data-ttu-id="567cf-114">How to publish application updates to Azure.</span><span class="sxs-lookup"><span data-stu-id="567cf-114">How to publish application updates to Azure.</span></span>

<span data-ttu-id="567cf-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses the ADO.NET Entity Framework for database access.</span><span class="sxs-lookup"><span data-stu-id="567cf-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses the ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="567cf-116">The following illustration shows the completed application:</span><span class="sxs-lookup"><span data-stu-id="567cf-116">The following illustration shows the completed application:</span></span>

![screenshot of web site][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-the-project"></a><span data-ttu-id="567cf-118">Create the project</span><span class="sxs-lookup"><span data-stu-id="567cf-118">Create the project</span></span>
1. <span data-ttu-id="567cf-119">Start Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="567cf-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="567cf-120">From the **File** menu click **New Project**.</span><span class="sxs-lookup"><span data-stu-id="567cf-120">From the **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="567cf-121">In the **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span><span class="sxs-lookup"><span data-stu-id="567cf-121">In the **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="567cf-122">Name the application **ContactManager** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="567cf-122">Name the application **ContactManager** and click **OK**.</span></span>
   
    ![New Project dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="567cf-124">In the **New ASP.NET Project** dialog box, select the **MVC** template, check **Web API** and then click **Change Authentication**.</span><span class="sxs-lookup"><span data-stu-id="567cf-124">In the **New ASP.NET Project** dialog box, select the **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="567cf-125">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="567cf-125">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![No Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="567cf-127">The sample application you're creating won't have features that require users to log in.</span><span class="sxs-lookup"><span data-stu-id="567cf-127">The sample application you're creating won't have features that require users to log in.</span></span> <span data-ttu-id="567cf-128">For information about how to implement authentication and authorization features, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="567cf-128">For information about how to implement authentication and authorization features, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
6. <span data-ttu-id="567cf-129">In the **New ASP.NET Project** dialog box, make sure the **Host in the Cloud** is checked and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="567cf-129">In the **New ASP.NET Project** dialog box, make sure the **Host in the Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="567cf-130">If you have not previously signed in to Azure, you will be prompted to sign in.</span><span class="sxs-lookup"><span data-stu-id="567cf-130">If you have not previously signed in to Azure, you will be prompted to sign in.</span></span>

1. <span data-ttu-id="567cf-131">The configuration wizard will suggest a unique name based on *ContactManager* (see the image below).</span><span class="sxs-lookup"><span data-stu-id="567cf-131">The configuration wizard will suggest a unique name based on *ContactManager* (see the image below).</span></span> <span data-ttu-id="567cf-132">Select a region near you.</span><span class="sxs-lookup"><span data-stu-id="567cf-132">Select a region near you.</span></span> <span data-ttu-id="567cf-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") to find the lowest latency data center.</span><span class="sxs-lookup"><span data-stu-id="567cf-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") to find the lowest latency data center.</span></span> 
2. <span data-ttu-id="567cf-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span><span class="sxs-lookup"><span data-stu-id="567cf-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Configure Azure Website](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="567cf-136">If you have a database server, use that to create a new database.</span><span class="sxs-lookup"><span data-stu-id="567cf-136">If you have a database server, use that to create a new database.</span></span> <span data-ttu-id="567cf-137">Database servers are a precious resource, and you generally want to create multiple databases on the same server for testing and development rather than creating a database server per database.</span><span class="sxs-lookup"><span data-stu-id="567cf-137">Database servers are a precious resource, and you generally want to create multiple databases on the same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="567cf-138">Make sure your web site and database are in the same region.</span><span class="sxs-lookup"><span data-stu-id="567cf-138">Make sure your web site and database are in the same region.</span></span>

![Configure Azure Website](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-the-page-header-and-footer"></a><span data-ttu-id="567cf-140">Set the page header and footer</span><span class="sxs-lookup"><span data-stu-id="567cf-140">Set the page header and footer</span></span>
1. <span data-ttu-id="567cf-141">In **Solution Explorer**, expand the *Views\Shared* folder and open the *_Layout.cshtml* file.</span><span class="sxs-lookup"><span data-stu-id="567cf-141">In **Solution Explorer**, expand the *Views\Shared* folder and open the *_Layout.cshtml* file.</span></span>
   
    ![_Layout.cshtml in Solution Explorer][newapp004]
2. <span data-ttu-id="567cf-143">Replace the contents of the *Views\Shared_Layout.cshtml* file with the following code:</span><span class="sxs-lookup"><span data-stu-id="567cf-143">Replace the contents of the *Views\Shared_Layout.cshtml* file with the following code:</span></span>

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

<span data-ttu-id="567cf-144">The markup above changes the app name from "My ASP.NET App" to "Contact Manager", and it removes the links to **Home**, **About** and **Contact**.</span><span class="sxs-lookup"><span data-stu-id="567cf-144">The markup above changes the app name from "My ASP.NET App" to "Contact Manager", and it removes the links to **Home**, **About** and **Contact**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="567cf-145">Run the application locally</span><span class="sxs-lookup"><span data-stu-id="567cf-145">Run the application locally</span></span>
1. <span data-ttu-id="567cf-146">Press CTRL+F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="567cf-146">Press CTRL+F5 to run the application.</span></span>
   <span data-ttu-id="567cf-147">The application home page appears in the default browser.</span><span class="sxs-lookup"><span data-stu-id="567cf-147">The application home page appears in the default browser.</span></span>
    <span data-ttu-id="567cf-148">![To Do List home page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="567cf-148">![To Do List home page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="567cf-149">This is all you need to do for now to create the application that you'll deploy to Azure.</span><span class="sxs-lookup"><span data-stu-id="567cf-149">This is all you need to do for now to create the application that you'll deploy to Azure.</span></span> <span data-ttu-id="567cf-150">Later you'll add database functionality.</span><span class="sxs-lookup"><span data-stu-id="567cf-150">Later you'll add database functionality.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="567cf-151">Deploy the application to Azure</span><span class="sxs-lookup"><span data-stu-id="567cf-151">Deploy the application to Azure</span></span>
1. <span data-ttu-id="567cf-152">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="567cf-152">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
   
    ![Publish in project context menu][PublishVSSolution]
   
    <span data-ttu-id="567cf-154">The **Publish Web** wizard opens.</span><span class="sxs-lookup"><span data-stu-id="567cf-154">The **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="567cf-155">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="567cf-155">Click **Publish**.</span></span>

![Settings tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="567cf-157">Visual Studio begins the process of copying the files to the Azure server.</span><span class="sxs-lookup"><span data-stu-id="567cf-157">Visual Studio begins the process of copying the files to the Azure server.</span></span> <span data-ttu-id="567cf-158">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span><span class="sxs-lookup"><span data-stu-id="567cf-158">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span>

1. <span data-ttu-id="567cf-159">The default browser automatically opens to the URL of the deployed site.</span><span class="sxs-lookup"><span data-stu-id="567cf-159">The default browser automatically opens to the URL of the deployed site.</span></span>
   
   <span data-ttu-id="567cf-160">The application you created is now running in the cloud.</span><span class="sxs-lookup"><span data-stu-id="567cf-160">The application you created is now running in the cloud.</span></span>
   
   ![To Do List home page running in Azure][rxz2]

## <a name="add-a-database-to-the-application"></a><span data-ttu-id="567cf-162">Add a database to the application</span><span class="sxs-lookup"><span data-stu-id="567cf-162">Add a database to the application</span></span>
<span data-ttu-id="567cf-163">Next, you'll update the MVC application to add the ability to display and update contacts and store the data in a database.</span><span class="sxs-lookup"><span data-stu-id="567cf-163">Next, you'll update the MVC application to add the ability to display and update contacts and store the data in a database.</span></span> <span data-ttu-id="567cf-164">The application will use the Entity Framework to create the database and to read and update data in the database.</span><span class="sxs-lookup"><span data-stu-id="567cf-164">The application will use the Entity Framework to create the database and to read and update data in the database.</span></span>

### <a name="add-data-model-classes-for-the-contacts"></a><span data-ttu-id="567cf-165">Add data model classes for the contacts</span><span class="sxs-lookup"><span data-stu-id="567cf-165">Add data model classes for the contacts</span></span>
<span data-ttu-id="567cf-166">You begin by creating a simple data model in code.</span><span class="sxs-lookup"><span data-stu-id="567cf-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="567cf-167">In **Solution Explorer**, right-click the Models folder, click **Add**, and then **Class**.</span><span class="sxs-lookup"><span data-stu-id="567cf-167">In **Solution Explorer**, right-click the Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Add Class in Models folder context menu][adddb001]
2. <span data-ttu-id="567cf-169">In the **Add New Item** dialog box, name the new class file *Contact.cs*, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="567cf-169">In the **Add New Item** dialog box, name the new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Add New Item dialog box][adddb002]
3. <span data-ttu-id="567cf-171">Replace the contents of the Contacts.cs file with the following code.</span><span class="sxs-lookup"><span data-stu-id="567cf-171">Replace the contents of the Contacts.cs file with the following code.</span></span>
   
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
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

<span data-ttu-id="567cf-172">The **Contact** class defines the data that you will store for each contact, plus a primary key, ContactID, that is needed by the database.</span><span class="sxs-lookup"><span data-stu-id="567cf-172">The **Contact** class defines the data that you will store for each contact, plus a primary key, ContactID, that is needed by the database.</span></span> <span data-ttu-id="567cf-173">You can get more information about data models in the [Next Steps](#nextsteps) section at the end of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="567cf-173">You can get more information about data models in the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-to-work-with-the-contacts"></a><span data-ttu-id="567cf-174">Create web pages that enable app users to work with the contacts</span><span class="sxs-lookup"><span data-stu-id="567cf-174">Create web pages that enable app users to work with the contacts</span></span>
<span data-ttu-id="567cf-175">The ASP.NET MVC the scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span><span class="sxs-lookup"><span data-stu-id="567cf-175">The ASP.NET MVC the scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-the-data"></a><span data-ttu-id="567cf-176">Add a Controller and a view for the data</span><span class="sxs-lookup"><span data-stu-id="567cf-176">Add a Controller and a view for the data</span></span>
1. <span data-ttu-id="567cf-177">In **Solution Explorer**, expand the Controllers folder.</span><span class="sxs-lookup"><span data-stu-id="567cf-177">In **Solution Explorer**, expand the Controllers folder.</span></span>
2. <span data-ttu-id="567cf-178">Build the project **(Ctrl+Shift+B)**.</span><span class="sxs-lookup"><span data-stu-id="567cf-178">Build the project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="567cf-179">(You must build the project before using scaffolding mechanism.)</span><span class="sxs-lookup"><span data-stu-id="567cf-179">(You must build the project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="567cf-180">Right-click the Controllers folder and click **Add**, and then click **Controller**.</span><span class="sxs-lookup"><span data-stu-id="567cf-180">Right-click the Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Add Controller in Controllers folder context menu][addcode001]
4. <span data-ttu-id="567cf-182">In the **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="567cf-182">In the **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Add controller](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="567cf-184">Set the controller name to **HomeController**.</span><span class="sxs-lookup"><span data-stu-id="567cf-184">Set the controller name to **HomeController**.</span></span> <span data-ttu-id="567cf-185">Select **Contact** as your model class.</span><span class="sxs-lookup"><span data-stu-id="567cf-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="567cf-186">Click the **New data context** button and accept the default "ContactManager.Models.ContactManagerContext" for the **New data context type**.</span><span class="sxs-lookup"><span data-stu-id="567cf-186">Click the **New data context** button and accept the default "ContactManager.Models.ContactManagerContext" for the **New data context type**.</span></span> <span data-ttu-id="567cf-187">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="567cf-187">Click **Add**.</span></span>

    <span data-ttu-id="567cf-188">A dialog box will prompt you: "A file with the name HomeController already exits.</span><span class="sxs-lookup"><span data-stu-id="567cf-188">A dialog box will prompt you: "A file with the name HomeController already exits.</span></span> <span data-ttu-id="567cf-189">Do you want to replace it?".</span><span class="sxs-lookup"><span data-stu-id="567cf-189">Do you want to replace it?".</span></span> <span data-ttu-id="567cf-190">Click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="567cf-190">Click **Yes**.</span></span> <span data-ttu-id="567cf-191">We are overwriting the Home Controller that was created with the new project.</span><span class="sxs-lookup"><span data-stu-id="567cf-191">We are overwriting the Home Controller that was created with the new project.</span></span> <span data-ttu-id="567cf-192">We will use the new Home Controller for our contact list.</span><span class="sxs-lookup"><span data-stu-id="567cf-192">We will use the new Home Controller for our contact list.</span></span>

    <span data-ttu-id="567cf-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span><span class="sxs-lookup"><span data-stu-id="567cf-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-the-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="567cf-194">Enable Migrations, create the database, add sample data and a data initializer</span><span class="sxs-lookup"><span data-stu-id="567cf-194">Enable Migrations, create the database, add sample data and a data initializer</span></span>
<span data-ttu-id="567cf-195">The next task is to enable the [Code First Migrations](http://curah.microsoft.com/55220) feature in order to create the database based on the data model you created.</span><span class="sxs-lookup"><span data-stu-id="567cf-195">The next task is to enable the [Code First Migrations](http://curah.microsoft.com/55220) feature in order to create the database based on the data model you created.</span></span>

1. <span data-ttu-id="567cf-196">In the **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="567cf-196">In the **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Package Manager Console in Tools menu][addcode008]
2. <span data-ttu-id="567cf-198">In the **Package Manager Console** window, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="567cf-198">In the **Package Manager Console** window, enter the following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="567cf-199">The **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit to configure Migrations.</span><span class="sxs-lookup"><span data-stu-id="567cf-199">The **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit to configure Migrations.</span></span> 
3. <span data-ttu-id="567cf-200">In the **Package Manager Console** window, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="567cf-200">In the **Package Manager Console** window, enter the following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="567cf-201">The **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates the database.</span><span class="sxs-lookup"><span data-stu-id="567cf-201">The **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates the database.</span></span> <span data-ttu-id="567cf-202">The first parameter ( *Initial* ) is arbitrary and used to create the name of the file.</span><span class="sxs-lookup"><span data-stu-id="567cf-202">The first parameter ( *Initial* ) is arbitrary and used to create the name of the file.</span></span> <span data-ttu-id="567cf-203">You can see the new class files in **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="567cf-203">You can see the new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="567cf-204">In the **Initial** class, the **Up** method creates the Contacts table, and the **Down** method (used when you want to return to the previous state) drops it.</span><span class="sxs-lookup"><span data-stu-id="567cf-204">In the **Initial** class, the **Up** method creates the Contacts table, and the **Down** method (used when you want to return to the previous state) drops it.</span></span>
4. <span data-ttu-id="567cf-205">Open the *Migrations\Configuration.cs* file.</span><span class="sxs-lookup"><span data-stu-id="567cf-205">Open the *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="567cf-206">Add the following namespaces.</span><span class="sxs-lookup"><span data-stu-id="567cf-206">Add the following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="567cf-207">Replace the *Seed* method with the following code:</span><span class="sxs-lookup"><span data-stu-id="567cf-207">Replace the *Seed* method with the following code:</span></span>
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
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
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    <span data-ttu-id="567cf-208">This code above will initialize the database with the contact information.</span><span class="sxs-lookup"><span data-stu-id="567cf-208">This code above will initialize the database with the contact information.</span></span> <span data-ttu-id="567cf-209">For more information on seeding the database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="567cf-209">For more information on seeding the database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="567cf-210">In the **Package Manager Console** enter the command:</span><span class="sxs-lookup"><span data-stu-id="567cf-210">In the **Package Manager Console** enter the command:</span></span>
   
        update-database
   
    ![Package Manager Console commands][addcode009]
   
    <span data-ttu-id="567cf-212">The **update-database** runs the first migration which creates the database.</span><span class="sxs-lookup"><span data-stu-id="567cf-212">The **update-database** runs the first migration which creates the database.</span></span> <span data-ttu-id="567cf-213">By default, the database is created as a SQL Server Express LocalDB database.</span><span class="sxs-lookup"><span data-stu-id="567cf-213">By default, the database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="567cf-214">Press CTRL+F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="567cf-214">Press CTRL+F5 to run the application.</span></span> 

<span data-ttu-id="567cf-215">The application shows the seed data and provides edit, details and delete links.</span><span class="sxs-lookup"><span data-stu-id="567cf-215">The application shows the seed data and provides edit, details and delete links.</span></span>

![MVC view of data][rxz3]

## <a name="edit-the-view"></a><span data-ttu-id="567cf-217">Edit the View</span><span class="sxs-lookup"><span data-stu-id="567cf-217">Edit the View</span></span>
1. <span data-ttu-id="567cf-218">Open the *Views\Home\Index.cshtml* file.</span><span class="sxs-lookup"><span data-stu-id="567cf-218">Open the *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="567cf-219">In the next step, we will replace the generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="567cf-219">In the next step, we will replace the generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="567cf-220">This new code retrieves the list of contacts from using web API and JSON and then binds the contact data to the UI using knockout.js.</span><span class="sxs-lookup"><span data-stu-id="567cf-220">This new code retrieves the list of contacts from using web API and JSON and then binds the contact data to the UI using knockout.js.</span></span> <span data-ttu-id="567cf-221">For more information, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="567cf-221">For more information, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
2. <span data-ttu-id="567cf-222">Replace the contents of the file with the following code.</span><span class="sxs-lookup"><span data-stu-id="567cf-222">Replace the contents of the file with the following code.</span></span>
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. <span data-ttu-id="567cf-223">Right-click the Content folder and click **Add**, and then click **New Item...**.</span><span class="sxs-lookup"><span data-stu-id="567cf-223">Right-click the Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Add style sheet in Content folder context menu][addcode005]
4. <span data-ttu-id="567cf-225">In the **Add New Item** dialog box, enter **Style** in the upper right search box and then select **Style Sheet**.</span><span class="sxs-lookup"><span data-stu-id="567cf-225">In the **Add New Item** dialog box, enter **Style** in the upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="567cf-226">![Add New Item dialog box][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="567cf-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="567cf-227">Name the file *Contacts.css* and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="567cf-227">Name the file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="567cf-228">Replace the contents of the file with the following code.</span><span class="sxs-lookup"><span data-stu-id="567cf-228">Replace the contents of the file with the following code.</span></span>
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    <span data-ttu-id="567cf-229">We will use this style sheet for the layout, colors and styles used in the contact manager app.</span><span class="sxs-lookup"><span data-stu-id="567cf-229">We will use this style sheet for the layout, colors and styles used in the contact manager app.</span></span>
6. <span data-ttu-id="567cf-230">Open the *App_Start\BundleConfig.cs* file.</span><span class="sxs-lookup"><span data-stu-id="567cf-230">Open the *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="567cf-231">Add the following code to register the [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span><span class="sxs-lookup"><span data-stu-id="567cf-231">Add the following code to register the [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="567cf-232">This sample using knockout to simplify dynamic JavaScript code that handles the screen templates.</span><span class="sxs-lookup"><span data-stu-id="567cf-232">This sample using knockout to simplify dynamic JavaScript code that handles the screen templates.</span></span>
8. <span data-ttu-id="567cf-233">Modify the contents/css entry to register the *contacts.css* style sheet.</span><span class="sxs-lookup"><span data-stu-id="567cf-233">Modify the contents/css entry to register the *contacts.css* style sheet.</span></span> <span data-ttu-id="567cf-234">Change the following line:</span><span class="sxs-lookup"><span data-stu-id="567cf-234">Change the following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="567cf-235">To:</span><span class="sxs-lookup"><span data-stu-id="567cf-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="567cf-236">In the Package Manager Console, run the following command to install Knockout.</span><span class="sxs-lookup"><span data-stu-id="567cf-236">In the Package Manager Console, run the following command to install Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-the-web-api-restful-interface"></a><span data-ttu-id="567cf-237">Add a controller for the Web API Restful interface</span><span class="sxs-lookup"><span data-stu-id="567cf-237">Add a controller for the Web API Restful interface</span></span>
1. <span data-ttu-id="567cf-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span><span class="sxs-lookup"><span data-stu-id="567cf-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="567cf-239">In the **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="567cf-239">In the **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![Add API controller](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="567cf-241">In the **Add Controller** dialog box, enter "ContactsController" as your controller name.</span><span class="sxs-lookup"><span data-stu-id="567cf-241">In the **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="567cf-242">Select "Contact (ContactManager.Models)" for the **Model class**.</span><span class="sxs-lookup"><span data-stu-id="567cf-242">Select "Contact (ContactManager.Models)" for the **Model class**.</span></span>  <span data-ttu-id="567cf-243">Keep the default value for the **Data context class**.</span><span class="sxs-lookup"><span data-stu-id="567cf-243">Keep the default value for the **Data context class**.</span></span> 
4. <span data-ttu-id="567cf-244">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="567cf-244">Click **Add**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="567cf-245">Run the application locally</span><span class="sxs-lookup"><span data-stu-id="567cf-245">Run the application locally</span></span>
1. <span data-ttu-id="567cf-246">Press CTRL+F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="567cf-246">Press CTRL+F5 to run the application.</span></span>
   
    ![Index page][intro001]
2. <span data-ttu-id="567cf-248">Enter a contact and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="567cf-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="567cf-249">The app returns to the home page and displays the contact you entered.</span><span class="sxs-lookup"><span data-stu-id="567cf-249">The app returns to the home page and displays the contact you entered.</span></span>
   
    ![Index page with to-do list items][addwebapi004]
3. <span data-ttu-id="567cf-251">In the browser, append **/api/contacts** to the URL.</span><span class="sxs-lookup"><span data-stu-id="567cf-251">In the browser, append **/api/contacts** to the URL.</span></span>
   
    <span data-ttu-id="567cf-252">The resulting URL will resemble http://localhost:1234/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="567cf-252">The resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="567cf-253">The RESTful web API you added returns the stored contacts.</span><span class="sxs-lookup"><span data-stu-id="567cf-253">The RESTful web API you added returns the stored contacts.</span></span> <span data-ttu-id="567cf-254">Firefox and Chrome will display the data in XML format.</span><span class="sxs-lookup"><span data-stu-id="567cf-254">Firefox and Chrome will display the data in XML format.</span></span>
   
    ![Index page with to-do list items][rxFFchrome]

    <span data-ttu-id="567cf-256">IE will prompt you to open or save the contacts.</span><span class="sxs-lookup"><span data-stu-id="567cf-256">IE will prompt you to open or save the contacts.</span></span>

    ![Web API save dialog][addwebapi006]


    <span data-ttu-id="567cf-258">You can open the returned contacts in notepad or a browser.</span><span class="sxs-lookup"><span data-stu-id="567cf-258">You can open the returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="567cf-259">This output can be consumed by another application such as mobile web page or application.</span><span class="sxs-lookup"><span data-stu-id="567cf-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Web API save dialog][addwebapi007]

    <span data-ttu-id="567cf-261">**Security Warning**: At this point, your application is insecure and vulnerable to CSRF attack.</span><span class="sxs-lookup"><span data-stu-id="567cf-261">**Security Warning**: At this point, your application is insecure and vulnerable to CSRF attack.</span></span> <span data-ttu-id="567cf-262">Later in the tutorial we will remove this vulnerability.</span><span class="sxs-lookup"><span data-stu-id="567cf-262">Later in the tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="567cf-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="567cf-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="567cf-264">Add XSRF Protection</span><span class="sxs-lookup"><span data-stu-id="567cf-264">Add XSRF Protection</span></span>
<span data-ttu-id="567cf-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence the interaction between a client browser and a website trusted by that browser.</span><span class="sxs-lookup"><span data-stu-id="567cf-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence the interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="567cf-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request to a website.</span><span class="sxs-lookup"><span data-stu-id="567cf-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request to a website.</span></span> <span data-ttu-id="567cf-267">The canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span><span class="sxs-lookup"><span data-stu-id="567cf-267">The canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="567cf-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span><span class="sxs-lookup"><span data-stu-id="567cf-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="567cf-269">An XSRF attack is distinct from a phishing attack.</span><span class="sxs-lookup"><span data-stu-id="567cf-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="567cf-270">Phishing attacks require interaction from the victim.</span><span class="sxs-lookup"><span data-stu-id="567cf-270">Phishing attacks require interaction from the victim.</span></span> <span data-ttu-id="567cf-271">In a phishing attack, a malicious website will mimic the target website, and the victim is fooled into providing sensitive information to the attacker.</span><span class="sxs-lookup"><span data-stu-id="567cf-271">In a phishing attack, a malicious website will mimic the target website, and the victim is fooled into providing sensitive information to the attacker.</span></span> <span data-ttu-id="567cf-272">In an XSRF attack, there is often no interaction necessary from the victim.</span><span class="sxs-lookup"><span data-stu-id="567cf-272">In an XSRF attack, there is often no interaction necessary from the victim.</span></span> <span data-ttu-id="567cf-273">Rather, the attacker is relying on the browser automatically sending all relevant cookies to the destination website.</span><span class="sxs-lookup"><span data-stu-id="567cf-273">Rather, the attacker is relying on the browser automatically sending all relevant cookies to the destination website.</span></span>

<span data-ttu-id="567cf-274">For more information, see the [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="567cf-274">For more information, see the [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="567cf-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="567cf-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="567cf-276">Name the file *ValidateHttpAntiForgeryTokenAttribute.cs* and add the following code:</span><span class="sxs-lookup"><span data-stu-id="567cf-276">Name the file *ValidateHttpAntiForgeryTokenAttribute.cs* and add the following code:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. <span data-ttu-id="567cf-277">Add the following *using* statement to the contracts controller so you have access to the **[ValidateHttpAntiForgeryToken]** attribute.</span><span class="sxs-lookup"><span data-stu-id="567cf-277">Add the following *using* statement to the contracts controller so you have access to the **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="567cf-278">Add the **[ValidateHttpAntiForgeryToken]** attribute to the Post methods of the **ContactsController** to protect it from XSRF threats.</span><span class="sxs-lookup"><span data-stu-id="567cf-278">Add the **[ValidateHttpAntiForgeryToken]** attribute to the Post methods of the **ContactsController** to protect it from XSRF threats.</span></span> <span data-ttu-id="567cf-279">You will add it to the "PutContact",  "PostContact" and **DeleteContact** action methods.</span><span class="sxs-lookup"><span data-stu-id="567cf-279">You will add it to the "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="567cf-280">Update the *Scripts* section of the *Views\Home\Index.cshtml* file to include code to get the XSRF tokens.</span><span class="sxs-lookup"><span data-stu-id="567cf-280">Update the *Scripts* section of the *Views\Home\Index.cshtml* file to include code to get the XSRF tokens.</span></span>
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-the-application-update-to-azure-and-sql-database"></a><span data-ttu-id="567cf-281">Publish the application update to Azure and SQL Database</span><span class="sxs-lookup"><span data-stu-id="567cf-281">Publish the application update to Azure and SQL Database</span></span>
<span data-ttu-id="567cf-282">To publish the application, you repeat the procedure you followed earlier.</span><span class="sxs-lookup"><span data-stu-id="567cf-282">To publish the application, you repeat the procedure you followed earlier.</span></span>

1. <span data-ttu-id="567cf-283">In **Solution Explorer**, right click the project and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="567cf-283">In **Solution Explorer**, right click the project and select **Publish**.</span></span>
   
    ![Publish][rxP]
2. <span data-ttu-id="567cf-285">Click the **Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="567cf-285">Click the **Settings** tab.</span></span>
3. <span data-ttu-id="567cf-286">Under **ContactsManagerContext(ContactsManagerContext)**, click the **v** icon to change *Remote connection string* to the connection string for the contact database.</span><span class="sxs-lookup"><span data-stu-id="567cf-286">Under **ContactsManagerContext(ContactsManagerContext)**, click the **v** icon to change *Remote connection string* to the connection string for the contact database.</span></span> <span data-ttu-id="567cf-287">Click **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="567cf-287">Click **ContactDB**.</span></span>
   
    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="567cf-289">Check the box for **Execute Code First Migrations (runs on application start)**.</span><span class="sxs-lookup"><span data-stu-id="567cf-289">Check the box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="567cf-290">Click **Next** and then click **Preview**.</span><span class="sxs-lookup"><span data-stu-id="567cf-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="567cf-291">Visual Studio displays a list of the files that will be added or updated.</span><span class="sxs-lookup"><span data-stu-id="567cf-291">Visual Studio displays a list of the files that will be added or updated.</span></span>
6. <span data-ttu-id="567cf-292">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="567cf-292">Click **Publish**.</span></span>
   <span data-ttu-id="567cf-293">After the deployment completes, the browser opens to the home page of the application.</span><span class="sxs-lookup"><span data-stu-id="567cf-293">After the deployment completes, the browser opens to the home page of the application.</span></span>
   
    ![Index page with no contacts][intro001]
   
    <span data-ttu-id="567cf-295">The Visual Studio publish process automatically configured the connection string in the deployed *Web.config* file to point to the SQL database.</span><span class="sxs-lookup"><span data-stu-id="567cf-295">The Visual Studio publish process automatically configured the connection string in the deployed *Web.config* file to point to the SQL database.</span></span> <span data-ttu-id="567cf-296">It also configured Code First Migrations to automatically upgrade the database to the latest version the first time the application accesses the database after deployment.</span><span class="sxs-lookup"><span data-stu-id="567cf-296">It also configured Code First Migrations to automatically upgrade the database to the latest version the first time the application accesses the database after deployment.</span></span>
   
    <span data-ttu-id="567cf-297">As a result of this configuration, Code First created the database by running the code in the **Initial** class that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="567cf-297">As a result of this configuration, Code First created the database by running the code in the **Initial** class that you created earlier.</span></span> <span data-ttu-id="567cf-298">It did this the first time the application tried to access the database after deployment.</span><span class="sxs-lookup"><span data-stu-id="567cf-298">It did this the first time the application tried to access the database after deployment.</span></span>
7. <span data-ttu-id="567cf-299">Enter a contact as you did when you ran the app locally, to verify that database deployment succeeded.</span><span class="sxs-lookup"><span data-stu-id="567cf-299">Enter a contact as you did when you ran the app locally, to verify that database deployment succeeded.</span></span>

<span data-ttu-id="567cf-300">When you see that the item you enter is saved and appears on the contact manager page, you know that it has been stored in the database.</span><span class="sxs-lookup"><span data-stu-id="567cf-300">When you see that the item you enter is saved and appears on the contact manager page, you know that it has been stored in the database.</span></span>

![Index page with contacts][addwebapi004]

<span data-ttu-id="567cf-302">The application is now running in the cloud, using SQL Database to store its data.</span><span class="sxs-lookup"><span data-stu-id="567cf-302">The application is now running in the cloud, using SQL Database to store its data.</span></span> <span data-ttu-id="567cf-303">After you finish testing the application in Azure, delete it.</span><span class="sxs-lookup"><span data-stu-id="567cf-303">After you finish testing the application in Azure, delete it.</span></span> <span data-ttu-id="567cf-304">The application is public and doesn't have a mechanism to limit access.</span><span class="sxs-lookup"><span data-stu-id="567cf-304">The application is public and doesn't have a mechanism to limit access.</span></span>

> [!NOTE]
> <span data-ttu-id="567cf-305">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="567cf-305">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="567cf-306">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="567cf-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="567cf-307">Next Steps</span><span class="sxs-lookup"><span data-stu-id="567cf-307">Next Steps</span></span>
<span data-ttu-id="567cf-308">A real application would require authentication and authorization, and you would use the membership database for that purpose.</span><span class="sxs-lookup"><span data-stu-id="567cf-308">A real application would require authentication and authorization, and you would use the membership database for that purpose.</span></span> <span data-ttu-id="567cf-309">The tutorial [Deploy a Secure ASP.NET MVC application with OAuth, Membership and SQL Database](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md) is based on this tutorial and shows how to deploy a web application with the membership database.</span><span class="sxs-lookup"><span data-stu-id="567cf-309">The tutorial [Deploy a Secure ASP.NET MVC application with OAuth, Membership and SQL Database](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md) is based on this tutorial and shows how to deploy a web application with the membership database.</span></span>

<span data-ttu-id="567cf-310">Another way to store data in an Azure application is to use Azure storage, which provide non-relational data storage in the form of blobs and tables.</span><span class="sxs-lookup"><span data-stu-id="567cf-310">Another way to store data in an Azure application is to use Azure storage, which provide non-relational data storage in the form of blobs and tables.</span></span> <span data-ttu-id="567cf-311">The following links provide more information on Web API, ASP.NET MVC and Window Azure.</span><span class="sxs-lookup"><span data-stu-id="567cf-311">The following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="567cf-312">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="567cf-312">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="567cf-313">Intro to ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="567cf-313">Intro to ASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="567cf-314">Your First ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="567cf-314">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="567cf-315">Debugging WAWS</span><span class="sxs-lookup"><span data-stu-id="567cf-315">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="567cf-316">This tutorial and the sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="567cf-316">This tutorial and the sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="567cf-317">Please leave feedback on what you liked or what you would like to see improved, not only about the tutorial itself but also about the products that it demonstrates.</span><span class="sxs-lookup"><span data-stu-id="567cf-317">Please leave feedback on what you liked or what you would like to see improved, not only about the tutorial itself but also about the products that it demonstrates.</span></span> <span data-ttu-id="567cf-318">Your feedback will help us prioritize improvements.</span><span class="sxs-lookup"><span data-stu-id="567cf-318">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="567cf-319">We are especially interested in finding out how much interest there is in more automation for the process of configuring and deploying the membership database.</span><span class="sxs-lookup"><span data-stu-id="567cf-319">We are especially interested in finding out how much interest there is in more automation for the process of configuring and deploying the membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="567cf-320">What's changed</span><span class="sxs-lookup"><span data-stu-id="567cf-320">What's changed</span></span>
* <span data-ttu-id="567cf-321">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="567cf-321">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles to the Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update the Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks



























