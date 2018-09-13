---
title: Create a web app in Azure that connects to MongoDB running on a virtual machine
description: A tutorial that teaches you how to use Git to deploy an ASP.NET app to Azure App Service, connected to MongoDB on an Azure Virtual Machine.
tags: azure-portal
services: app-service\web, virtual-machines
documentationcenter: .net
author: cephalin
manager: erikre
editor: ''
ms.assetid: adf7a472-ae00-45a8-aec4-06247e21318b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: cephalin
ms.openlocfilehash: d8b3b5cac27cad0cdc457e66ef669566915a1322
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556294"
---
# <a name="create-a-web-app-in-azure-that-connects-to-mongodb-running-on-a-virtual-machine"></a><span data-ttu-id="5328e-103">Create a web app in Azure that connects to MongoDB running on a virtual machine</span><span class="sxs-lookup"><span data-stu-id="5328e-103">Create a web app in Azure that connects to MongoDB running on a virtual machine</span></span>
<span data-ttu-id="5328e-104">Using Git, you can deploy an ASP.NET application to Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="5328e-104">Using Git, you can deploy an ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="5328e-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects to a MongoDB database running on a virtual machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="5328e-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects to a MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="5328e-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span><span class="sxs-lookup"><span data-stu-id="5328e-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="5328e-107">After running and testing the ASP.NET application on your development computer, you will upload the application to App Service Web Apps using Git.</span><span class="sxs-lookup"><span data-stu-id="5328e-107">After running and testing the ASP.NET application on your development computer, you will upload the application to App Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="5328e-108">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="5328e-108">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5328e-109">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="5328e-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="5328e-110">Background knowledge</span><span class="sxs-lookup"><span data-stu-id="5328e-110">Background knowledge</span></span>
<span data-ttu-id="5328e-111">Knowledge of the following is useful for this tutorial, though not required:</span><span class="sxs-lookup"><span data-stu-id="5328e-111">Knowledge of the following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="5328e-112">The C# driver for MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5328e-112">The C# driver for MongoDB.</span></span> <span data-ttu-id="5328e-113">For more information on developing C# applications against MongoDB, see the MongoDB [CSharp Language Center][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="5328e-113">For more information on developing C# applications against MongoDB, see the MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="5328e-114">The ASP .NET web application framework.</span><span class="sxs-lookup"><span data-stu-id="5328e-114">The ASP .NET web application framework.</span></span> <span data-ttu-id="5328e-115">You can learn all about it at the [ASP.net website][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="5328e-115">You can learn all about it at the [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="5328e-116">The ASP .NET MVC web application framework.</span><span class="sxs-lookup"><span data-stu-id="5328e-116">The ASP .NET MVC web application framework.</span></span> <span data-ttu-id="5328e-117">You can learn all about it at the [ASP.NET MVC website][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="5328e-117">You can learn all about it at the [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="5328e-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="5328e-118">Azure.</span></span> <span data-ttu-id="5328e-119">You can get started reading at [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="5328e-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5328e-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5328e-120">Prerequisites</span></span>
* <span data-ttu-id="5328e-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="5328e-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="5328e-122">Azure SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="5328e-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="5328e-123">An active Microsoft Azure subscription</span><span class="sxs-lookup"><span data-stu-id="5328e-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="5328e-124">Create a virtual machine and install MongoDB</span><span class="sxs-lookup"><span data-stu-id="5328e-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="5328e-125">This tutorial assumes you have created a virtual machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="5328e-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="5328e-126">After creating the virtual machine you need to install MongoDB on the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="5328e-126">After creating the virtual machine you need to install MongoDB on the virtual machine:</span></span>

* <span data-ttu-id="5328e-127">To create a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="5328e-127">To create a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="5328e-128">After you have created the virtual machine in Azure and installed MongoDB, be sure to remember the DNS name of the virtual machine ("testlinuxvm.cloudapp.net", for example) and the external port for MongoDB that you specified in the endpoint.</span><span class="sxs-lookup"><span data-stu-id="5328e-128">After you have created the virtual machine in Azure and installed MongoDB, be sure to remember the DNS name of the virtual machine ("testlinuxvm.cloudapp.net", for example) and the external port for MongoDB that you specified in the endpoint.</span></span>  <span data-ttu-id="5328e-129">You will need this information later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="5328e-129">You will need this information later in the tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-the-application"></a><span data-ttu-id="5328e-130">Create the application</span><span class="sxs-lookup"><span data-stu-id="5328e-130">Create the application</span></span>
<span data-ttu-id="5328e-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment to Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="5328e-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment to Azure App Service Web Apps.</span></span> <span data-ttu-id="5328e-132">You will run the application locally, but it will connect to your virtual machine on Azure and use the MongoDB instance that you created there.</span><span class="sxs-lookup"><span data-stu-id="5328e-132">You will run the application locally, but it will connect to your virtual machine on Azure and use the MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="5328e-133">In Visual Studio, click **New Project**.</span><span class="sxs-lookup"><span data-stu-id="5328e-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Start Page New Project][StartPageNewProject]
2. <span data-ttu-id="5328e-135">In the **New Project** window, in the left pane, select **Visual C#**, and then select **Web**.</span><span class="sxs-lookup"><span data-stu-id="5328e-135">In the **New Project** window, in the left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="5328e-136">In the middle pane, select **ASP.NET  Web Application**.</span><span class="sxs-lookup"><span data-stu-id="5328e-136">In the middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="5328e-137">At the bottom, name your project "MyTaskListApp," and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5328e-137">At the bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![New Project Dialog][NewProjectMyTaskListApp]
3. <span data-ttu-id="5328e-139">In the **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5328e-139">In the **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![Select MVC Template][VS2013SelectMVCTemplate]
4. <span data-ttu-id="5328e-141">If you aren't already signed into Microsoft Azure, you will be prompted to sign in.</span><span class="sxs-lookup"><span data-stu-id="5328e-141">If you aren't already signed into Microsoft Azure, you will be prompted to sign in.</span></span> <span data-ttu-id="5328e-142">Follow the prompts to sign into Azure.</span><span class="sxs-lookup"><span data-stu-id="5328e-142">Follow the prompts to sign into Azure.</span></span>
5. <span data-ttu-id="5328e-143">Once you are signed in, you can start configuring your App Service web app.</span><span class="sxs-lookup"><span data-stu-id="5328e-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="5328e-144">Specify the **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5328e-144">Specify the **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="5328e-145">After the project creation completes, wait for the web app to be created in Azure App Service as indicated in the **Azure App Service Activity** window.</span><span class="sxs-lookup"><span data-stu-id="5328e-145">After the project creation completes, wait for the web app to be created in Azure App Service as indicated in the **Azure App Service Activity** window.</span></span> <span data-ttu-id="5328e-146">Then, click **Publish MyTaskListApp to this Web App now**.</span><span class="sxs-lookup"><span data-stu-id="5328e-146">Then, click **Publish MyTaskListApp to this Web App now**.</span></span>
7. <span data-ttu-id="5328e-147">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="5328e-147">Click **Publish**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="5328e-148">Once your default ASP.NET application is published to Azure App Service Web Apps, it will be launched in the browser.</span><span class="sxs-lookup"><span data-stu-id="5328e-148">Once your default ASP.NET application is published to Azure App Service Web Apps, it will be launched in the browser.</span></span>

## <a name="install-the-mongodb-c-driver"></a><span data-ttu-id="5328e-149">Install the MongoDB C# driver</span><span class="sxs-lookup"><span data-stu-id="5328e-149">Install the MongoDB C# driver</span></span>
<span data-ttu-id="5328e-150">MongoDB offers client-side support for C# applications through a driver, which you need to install on your local development computer.</span><span class="sxs-lookup"><span data-stu-id="5328e-150">MongoDB offers client-side support for C# applications through a driver, which you need to install on your local development computer.</span></span> <span data-ttu-id="5328e-151">The C# driver is available through NuGet.</span><span class="sxs-lookup"><span data-stu-id="5328e-151">The C# driver is available through NuGet.</span></span>

<span data-ttu-id="5328e-152">To install the MongoDB C# driver:</span><span class="sxs-lookup"><span data-stu-id="5328e-152">To install the MongoDB C# driver:</span></span>

1. <span data-ttu-id="5328e-153">In **Solution Explorer**, right-click the **MyTaskListApp** project and select **Manage NuGetPackages**.</span><span class="sxs-lookup"><span data-stu-id="5328e-153">In **Solution Explorer**, right-click the **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![Manage NuGet Packages][VS2013ManageNuGetPackages]
2. <span data-ttu-id="5328e-155">In the **Manage NuGet Packages** window, in the left pane, click **Online**.</span><span class="sxs-lookup"><span data-stu-id="5328e-155">In the **Manage NuGet Packages** window, in the left pane, click **Online**.</span></span> <span data-ttu-id="5328e-156">In the **Search Online** box on the right, type "mongodb.driver".</span><span class="sxs-lookup"><span data-stu-id="5328e-156">In the **Search Online** box on the right, type "mongodb.driver".</span></span>  <span data-ttu-id="5328e-157">Click **Install** to install the driver.</span><span class="sxs-lookup"><span data-stu-id="5328e-157">Click **Install** to install the driver.</span></span>
   
    ![Search for MongoDB C# Driver][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="5328e-159">Click **I Accept** to accept the 10gen, Inc. license terms.</span><span class="sxs-lookup"><span data-stu-id="5328e-159">Click **I Accept** to accept the 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="5328e-160">Click **Close** after the driver has installed.</span><span class="sxs-lookup"><span data-stu-id="5328e-160">Click **Close** after the driver has installed.</span></span>
    <span data-ttu-id="5328e-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="5328e-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="5328e-162">The MongoDB C# driver is now installed.</span><span class="sxs-lookup"><span data-stu-id="5328e-162">The MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="5328e-163">References to the **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added to the project.</span><span class="sxs-lookup"><span data-stu-id="5328e-163">References to the **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added to the project.</span></span>

![MongoDB C# Driver References][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="5328e-165">Add a model</span><span class="sxs-lookup"><span data-stu-id="5328e-165">Add a model</span></span>
<span data-ttu-id="5328e-166">In **Solution Explorer**, right-click the *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span><span class="sxs-lookup"><span data-stu-id="5328e-166">In **Solution Explorer**, right-click the *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="5328e-167">In *TaskModel.cs*, replace the existing code with the following code:</span><span class="sxs-lookup"><span data-stu-id="5328e-167">In *TaskModel.cs*, replace the existing code with the following code:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MongoDB.Bson.Serialization.Attributes;
    using MongoDB.Bson.Serialization.IdGenerators;
    using MongoDB.Bson;

    namespace MyTaskListApp.Models
    {
        public class MyTask
        {
            [BsonId(IdGenerator = typeof(CombGuidGenerator))]
            public Guid Id { get; set; }

            [BsonElement("Name")]
            public string Name { get; set; }

            [BsonElement("Category")]
            public string Category { get; set; }

            [BsonElement("Date")]
            public DateTime Date { get; set; }

            [BsonElement("CreatedDate")]
            public DateTime CreatedDate { get; set; }

        }
    }

## <a name="add-the-data-access-layer"></a><span data-ttu-id="5328e-168">Add the data access layer</span><span class="sxs-lookup"><span data-stu-id="5328e-168">Add the data access layer</span></span>
<span data-ttu-id="5328e-169">In **Solution Explorer**, right-click the *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span><span class="sxs-lookup"><span data-stu-id="5328e-169">In **Solution Explorer**, right-click the *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="5328e-170">Right-click the *DAL* folder and **Add** a new **Class**.</span><span class="sxs-lookup"><span data-stu-id="5328e-170">Right-click the *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="5328e-171">Name the class file *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="5328e-171">Name the class file *Dal.cs*.</span></span>  <span data-ttu-id="5328e-172">In *Dal.cs*, replace the existing code with the following code:</span><span class="sxs-lookup"><span data-stu-id="5328e-172">In *Dal.cs*, replace the existing code with the following code:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;


    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            private MongoServer mongoServer = null;
            private bool disposed = false;

            // To do: update the connection string with the DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  The database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from the MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }

            // Creates a Task and inserts it into the collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }

            private IMongoCollection<MyTask> GetTasksCollection()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            # region IDisposable

            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        if (mongoServer != null)
                        {
                            this.mongoServer.Disconnect();
                        }
                    }
                }

                this.disposed = true;
            }

            # endregion
        }
    }

## <a name="add-a-controller"></a><span data-ttu-id="5328e-173">Add a controller</span><span class="sxs-lookup"><span data-stu-id="5328e-173">Add a controller</span></span>
<span data-ttu-id="5328e-174">Open the *Controllers\HomeController.cs* file in **Solution Explorer** and replace the existing code with the following:</span><span class="sxs-lookup"><span data-stu-id="5328e-174">Open the *Controllers\HomeController.cs* file in **Solution Explorer** and replace the existing code with the following:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.Mvc;
    using MyTaskListApp.Models;
    using System.Configuration;

    namespace MyTaskListApp.Controllers
    {
        public class HomeController : Controller, IDisposable
        {
            private Dal dal = new Dal();
            private bool disposed = false;
            //
            // GET: /MyTask/

            public ActionResult Index()
            {
                return View(dal.GetAllTasks());
            }

            //
            // GET: /MyTask/Create

            public ActionResult Create()
            {
                return View();
            }

            //
            // POST: /MyTask/Create

            [HttpPost]
            public ActionResult Create(MyTask task)
            {
                try
                {
                    dal.CreateTask(task);
                    return RedirectToAction("Index");
                }
                catch
                {
                    return View();
                }
            }

            public ActionResult About()
            {
                return View();
            }

            # region IDisposable

            new protected void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            new protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        this.dal.Dispose();
                    }
                }

                this.disposed = true;
            }

            # endregion

        }
    }

## <a name="set-up-the-styles"></a><span data-ttu-id="5328e-175">Set up the styles</span><span class="sxs-lookup"><span data-stu-id="5328e-175">Set up the styles</span></span>
<span data-ttu-id="5328e-176">To change the title at the top of the page, open the *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in the navbar header with "My Task List Application" so that it looks like this:</span><span class="sxs-lookup"><span data-stu-id="5328e-176">To change the title at the top of the page, open the *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in the navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="5328e-177">In order to set up the Task List menu, open the *\Views\Home\Index.cshtml* file and replace the existing code with the following code:</span><span class="sxs-lookup"><span data-stu-id="5328e-177">In order to set up the Task List menu, open the *\Views\Home\Index.cshtml* file and replace the existing code with the following code:</span></span>

    @model IEnumerable<MyTaskListApp.Models.MyTask>

    @{
        ViewBag.Title = "My Task List";
    }

    <h2>My Task List</h2>

    <table border="1">
        <tr>
            <th>Task</th>
            <th>Category</th>
            <th>Date</th>

        </tr>

    @foreach (var item in Model) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.Name)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Category)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Date)
            </td>

        </tr>
    }

    </table>
    <div>  @Html.Partial("Create", new MyTaskListApp.Models.MyTask())</div>


<span data-ttu-id="5328e-178">To add the ability to create a new task, right-click the *Views\Home\\* folder and **Add** a **View**.</span><span class="sxs-lookup"><span data-stu-id="5328e-178">To add the ability to create a new task, right-click the *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="5328e-179">Name the view *Create*.</span><span class="sxs-lookup"><span data-stu-id="5328e-179">Name the view *Create*.</span></span> <span data-ttu-id="5328e-180">Replace the code with the following:</span><span class="sxs-lookup"><span data-stu-id="5328e-180">Replace the code with the following:</span></span>

    @model MyTaskListApp.Models.MyTask

    <script src="@Url.Content("~/Scripts/jquery-1.10.2.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.unobtrusive.min.js")" type="text/javascript"></script>

    @using (Html.BeginForm("Create", "Home")) {
        @Html.ValidationSummary(true)
        <fieldset>
            <legend>New Task</legend>

            <div class="editor-label">
                @Html.LabelFor(model => model.Name)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Name)
                @Html.ValidationMessageFor(model => model.Name)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Category)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Category)
                @Html.ValidationMessageFor(model => model.Category)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Date)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Date)
                @Html.ValidationMessageFor(model => model.Date)
            </div>

            <p>
                <input type="submit" value="Create" />
            </p>
        </fieldset>
    }

<span data-ttu-id="5328e-181">**Solution Explorer** should look like this:</span><span class="sxs-lookup"><span data-stu-id="5328e-181">**Solution Explorer** should look like this:</span></span>

![Solution Explorer][SolutionExplorerMyTaskListApp]

## <a name="set-the-mongodb-connection-string"></a><span data-ttu-id="5328e-183">Set the MongoDB connection string</span><span class="sxs-lookup"><span data-stu-id="5328e-183">Set the MongoDB connection string</span></span>
<span data-ttu-id="5328e-184">In **Solution Explorer**, open the *DAL/Dal.cs* file.</span><span class="sxs-lookup"><span data-stu-id="5328e-184">In **Solution Explorer**, open the *DAL/Dal.cs* file.</span></span> <span data-ttu-id="5328e-185">Find the following line of code:</span><span class="sxs-lookup"><span data-stu-id="5328e-185">Find the following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="5328e-186">Replace `<vm-dns-name>` with the DNS name of the virtual machine running MongoDB you created in the [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="5328e-186">Replace `<vm-dns-name>` with the DNS name of the virtual machine running MongoDB you created in the [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="5328e-187">To find the DNS name of your virtual machine, go to the Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span><span class="sxs-lookup"><span data-stu-id="5328e-187">To find the DNS name of your virtual machine, go to the Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="5328e-188">If the DNS name of the virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on the default port 27017, the connection string line of code will look like:</span><span class="sxs-lookup"><span data-stu-id="5328e-188">If the DNS name of the virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on the default port 27017, the connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="5328e-189">If the virtual machine endpoint specifies a different external port for MongoDB, you can specifiy the port in the connection string:</span><span class="sxs-lookup"><span data-stu-id="5328e-189">If the virtual machine endpoint specifies a different external port for MongoDB, you can specifiy the port in the connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="5328e-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span><span class="sxs-lookup"><span data-stu-id="5328e-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-the-local-deployment"></a><span data-ttu-id="5328e-191">Test the local deployment</span><span class="sxs-lookup"><span data-stu-id="5328e-191">Test the local deployment</span></span>
<span data-ttu-id="5328e-192">To run your application on your development computer, select **Start Debugging** from the **Debug** menu or hit **F5**.</span><span class="sxs-lookup"><span data-stu-id="5328e-192">To run your application on your development computer, select **Start Debugging** from the **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="5328e-193">IIS Express starts and a browser opens and launches the application's home page.</span><span class="sxs-lookup"><span data-stu-id="5328e-193">IIS Express starts and a browser opens and launches the application's home page.</span></span>  <span data-ttu-id="5328e-194">You can add a new task, which will be added to the MongoDB database running on your virtual machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="5328e-194">You can add a new task, which will be added to the MongoDB database running on your virtual machine in Azure.</span></span>

![My Task List Application][TaskListAppBlank]

## <a name="publish-to-azure-app-service-web-apps"></a><span data-ttu-id="5328e-196">Publish to Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="5328e-196">Publish to Azure App Service Web Apps</span></span>
<span data-ttu-id="5328e-197">In this section you will publish your changes to Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="5328e-197">In this section you will publish your changes to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="5328e-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="5328e-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="5328e-199">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="5328e-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="5328e-200">You should now see your web app running in Azure App Service and accessing the MongoDB database in Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="5328e-200">You should now see your web app running in Azure App Service and accessing the MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="5328e-201">Summary</span><span class="sxs-lookup"><span data-stu-id="5328e-201">Summary</span></span>
<span data-ttu-id="5328e-202">You have now successfully deployed your ASP.NET application to Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="5328e-202">You have now successfully deployed your ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="5328e-203">To view the web app:</span><span class="sxs-lookup"><span data-stu-id="5328e-203">To view the web app:</span></span>

1. <span data-ttu-id="5328e-204">Log into the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5328e-204">Log into the Azure Portal.</span></span>
2. <span data-ttu-id="5328e-205">Click **Web apps**.</span><span class="sxs-lookup"><span data-stu-id="5328e-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="5328e-206">Select your web app in the **Web Apps** list.</span><span class="sxs-lookup"><span data-stu-id="5328e-206">Select your web app in the **Web Apps** list.</span></span>

<span data-ttu-id="5328e-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="5328e-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- HYPERLINKS -->

[AzurePortal]: http://manage.windowsazure.com
[WindowsAzure]: http://www.windowsazure.com
[MongoC#LangCenter]: http://docs.mongodb.org/ecosystem/drivers/csharp/
[MVCWebSite]: http://www.asp.net/mvc
[ASP.NET]: http://www.asp.net/
[MongoConnectionStrings]: http://www.mongodb.org/display/DOCS/Connections
[MongoDB]: http://www.mongodb.org
[InstallMongoOnWindowsVM]:../virtual-machines/windows/classic/install-mongodb.md
[VSEWeb]: http://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express
[VSUlt]: http://www.microsoft.com/visualstudio/eng/2013-downloads

<!-- IMAGES -->


[StartPageNewProject]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-store-data-mongodb-vm/NewProject.png
[NewProjectMyTaskListApp]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-store-data-mongodb-vm/NewProjectMyTaskListApp.png
[VS2013SelectMVCTemplate]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-store-data-mongodb-vm/VS2013SelectMVCTemplate.png
[VS2013DefaultMVCApplication]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013DefaultMVCApplication.png
[VS2013ManageNuGetPackages]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-store-data-mongodb-vm/VS2013ManageNuGetPackages.png
[SearchforMongoDBCSharpDriver]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-store-data-mongodb-vm/SearchforMongoDBCSharpDriver.png
[MongoDBCsharpDriverInstalled]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCsharpDriverInstalled.png
[MongoDBCSharpDriverReferences]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCSharpDriverReferences.png
[SolutionExplorerMyTaskListApp]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-store-data-mongodb-vm/SolutionExplorerMyTaskListApp.png
[TaskListAppBlank]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-store-data-mongodb-vm/TaskListAppBlank.png
[WAWSCreateWebSite]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSCreateWebSite.png
[WAWSDashboardMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSDashboardMyTaskListApp.png
[Image9]: ./media/web-sites-dotnet-store-data-mongodb-vm/RepoReady.png
[Image10]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitInstructions.png
[Image11]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitDeploymentComplete.png

<!-- TOC BOOKMARKS -->
[Create a virtual machine and install MongoDB]: #virtualmachine
[Create and run the My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy the ASP.NET application to the web site using Git]: #deployapp











