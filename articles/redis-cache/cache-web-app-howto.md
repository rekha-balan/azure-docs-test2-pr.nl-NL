---
title: How to create a Web App with Redis Cache | Microsoft Docs
description: Learn how to create a Web App with Redis Cache
services: redis-cache
documentationcenter: ''
author: steved0x
manager: douge
editor: ''
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: sdanie
ms.openlocfilehash: 5803fb50f664c79de9d9f92869771fc6b10c349d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669986"
---
# <a name="how-to-create-a-web-app-with-redis-cache"></a><span data-ttu-id="2ed82-103">How to create a Web App with Redis Cache</span><span class="sxs-lookup"><span data-stu-id="2ed82-103">How to create a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

<span data-ttu-id="2ed82-109">This tutorial shows how to create and deploy an ASP.NET web application to a web app in Azure App Service using Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2ed82-109">This tutorial shows how to create and deploy an ASP.NET web application to a web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="2ed82-110">The sample application displays a list of team statistics from a database and shows different ways to use Azure Redis Cache to store and retrieve data from the cache.</span><span class="sxs-lookup"><span data-stu-id="2ed82-110">The sample application displays a list of team statistics from a database and shows different ways to use Azure Redis Cache to store and retrieve data from the cache.</span></span> <span data-ttu-id="2ed82-111">When you complete the tutorial you'll have a running web app that reads and writes to a database, optimized with Azure Redis Cache, and hosted in Azure.</span><span class="sxs-lookup"><span data-stu-id="2ed82-111">When you complete the tutorial you'll have a running web app that reads and writes to a database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="2ed82-112">You'll learn:</span><span class="sxs-lookup"><span data-stu-id="2ed82-112">You'll learn:</span></span>

* <span data-ttu-id="2ed82-113">How to create an ASP.NET MVC 5 web application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ed82-113">How to create an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="2ed82-114">How to access data from a database using Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="2ed82-114">How to access data from a database using Entity Framework.</span></span>
* <span data-ttu-id="2ed82-115">How to improve data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="2ed82-115">How to improve data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="2ed82-116">How to use a Redis sorted set to retrieve the top 5 teams.</span><span class="sxs-lookup"><span data-stu-id="2ed82-116">How to use a Redis sorted set to retrieve the top 5 teams.</span></span>
* <span data-ttu-id="2ed82-117">How to provision the Azure resources for the application using a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="2ed82-117">How to provision the Azure resources for the application using a Resource Manager template.</span></span>
* <span data-ttu-id="2ed82-118">How to publish the application to Azure using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ed82-118">How to publish the application to Azure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ed82-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2ed82-119">Prerequisites</span></span>
<span data-ttu-id="2ed82-120">To complete the tutorial, you must have the following prerequisites.</span><span class="sxs-lookup"><span data-stu-id="2ed82-120">To complete the tutorial, you must have the following prerequisites.</span></span>

* [<span data-ttu-id="2ed82-121">Azure account</span><span class="sxs-lookup"><span data-stu-id="2ed82-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="2ed82-122">Visual Studio 2017 with the Azure SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="2ed82-122">Visual Studio 2017 with the Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="2ed82-123">Azure account</span><span class="sxs-lookup"><span data-stu-id="2ed82-123">Azure account</span></span>
<span data-ttu-id="2ed82-124">You need an Azure account to complete the tutorial.</span><span class="sxs-lookup"><span data-stu-id="2ed82-124">You need an Azure account to complete the tutorial.</span></span> <span data-ttu-id="2ed82-125">You can:</span><span class="sxs-lookup"><span data-stu-id="2ed82-125">You can:</span></span>

* <span data-ttu-id="2ed82-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="2ed82-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="2ed82-127">You get credits that can be used to try out paid Azure services.</span><span class="sxs-lookup"><span data-stu-id="2ed82-127">You get credits that can be used to try out paid Azure services.</span></span> <span data-ttu-id="2ed82-128">Even after the credits are used up, you can keep the account and use free Azure services and features.</span><span class="sxs-lookup"><span data-stu-id="2ed82-128">Even after the credits are used up, you can keep the account and use free Azure services and features.</span></span>
* <span data-ttu-id="2ed82-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="2ed82-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="2ed82-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span><span class="sxs-lookup"><span data-stu-id="2ed82-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-the-azure-sdk-for-net"></a><span data-ttu-id="2ed82-131">Visual Studio 2017 with the Azure SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="2ed82-131">Visual Studio 2017 with the Azure SDK for .NET</span></span>
<span data-ttu-id="2ed82-132">The tutorial is written for Visual Studio 2017 with the [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span><span class="sxs-lookup"><span data-stu-id="2ed82-132">The tutorial is written for Visual Studio 2017 with the [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="2ed82-133">The Azure SDK 2.9.5 is included with the Visual Studio installer.</span><span class="sxs-lookup"><span data-stu-id="2ed82-133">The Azure SDK 2.9.5 is included with the Visual Studio installer.</span></span>

<span data-ttu-id="2ed82-134">If you have Visual Studio 2015, you can follow the tutorial with the [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span><span class="sxs-lookup"><span data-stu-id="2ed82-134">If you have Visual Studio 2015, you can follow the tutorial with the [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="2ed82-135">[Download the latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="2ed82-135">[Download the latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="2ed82-136">Visual Studio is automatically installed with the SDK if you don't already have it.</span><span class="sxs-lookup"><span data-stu-id="2ed82-136">Visual Studio is automatically installed with the SDK if you don't already have it.</span></span> <span data-ttu-id="2ed82-137">Some screens may look different from the illustrations shown in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="2ed82-137">Some screens may look different from the illustrations shown in this tutorial.</span></span>

<span data-ttu-id="2ed82-138">If you have Visual Studio 2013, you can [download the latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="2ed82-138">If you have Visual Studio 2013, you can [download the latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="2ed82-139">Some screens may look different from the illustrations shown in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="2ed82-139">Some screens may look different from the illustrations shown in this tutorial.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="2ed82-140">Create the Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="2ed82-140">Create the Visual Studio project</span></span>
1. <span data-ttu-id="2ed82-141">Open Visual Studio and click **File**, **New**, **Project**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="2ed82-142">Expand the **Visual C#** node in the **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-142">Expand the **Visual C#** node in the **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="2ed82-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span><span class="sxs-lookup"><span data-stu-id="2ed82-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="2ed82-144">Type **ContosoTeamStats** into the **Name** textbox and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-144">Type **ContosoTeamStats** into the **Name** textbox and click **OK**.</span></span>
   
    ![Create project][cache-create-project]
3. <span data-ttu-id="2ed82-146">Select **MVC** as the project type.</span><span class="sxs-lookup"><span data-stu-id="2ed82-146">Select **MVC** as the project type.</span></span> 

    <span data-ttu-id="2ed82-147">Ensure that **No Authentication** is specified for the **Authentication** settings.</span><span class="sxs-lookup"><span data-stu-id="2ed82-147">Ensure that **No Authentication** is specified for the **Authentication** settings.</span></span> <span data-ttu-id="2ed82-148">Depending on your version of Visual Studio, the default may be set to something else.</span><span class="sxs-lookup"><span data-stu-id="2ed82-148">Depending on your version of Visual Studio, the default may be set to something else.</span></span> <span data-ttu-id="2ed82-149">To change it, click **Change Authentication** and select **No Authentication**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-149">To change it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="2ed82-150">If you are following along with Visual Studio 2015, clear the **Host in the cloud** checkbox.</span><span class="sxs-lookup"><span data-stu-id="2ed82-150">If you are following along with Visual Studio 2015, clear the **Host in the cloud** checkbox.</span></span> <span data-ttu-id="2ed82-151">You'll [provision the Azure resources](#provision-the-azure-resources) and [publish the application to Azure](#publish-the-application-to-azure) in subsequent steps in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="2ed82-151">You'll [provision the Azure resources](#provision-the-azure-resources) and [publish the application to Azure](#publish-the-application-to-azure) in subsequent steps in the tutorial.</span></span> <span data-ttu-id="2ed82-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in the cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2ed82-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in the cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![Select project template][cache-select-template]
4. <span data-ttu-id="2ed82-154">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="2ed82-154">Click **OK** to create the project.</span></span>

## <a name="create-the-aspnet-mvc-application"></a><span data-ttu-id="2ed82-155">Create the ASP.NET MVC application</span><span class="sxs-lookup"><span data-stu-id="2ed82-155">Create the ASP.NET MVC application</span></span>
<span data-ttu-id="2ed82-156">In this section of the tutorial, you'll create the basic application that reads and displays team statistics from a database.</span><span class="sxs-lookup"><span data-stu-id="2ed82-156">In this section of the tutorial, you'll create the basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="2ed82-157">Add the Entity Framework NuGet package</span><span class="sxs-lookup"><span data-stu-id="2ed82-157">Add the Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="2ed82-158">Add the model</span><span class="sxs-lookup"><span data-stu-id="2ed82-158">Add the model</span></span>](#add-the-model)
* [<span data-ttu-id="2ed82-159">Add the controller</span><span class="sxs-lookup"><span data-stu-id="2ed82-159">Add the controller</span></span>](#add-the-controller)
* [<span data-ttu-id="2ed82-160">Configure the views</span><span class="sxs-lookup"><span data-stu-id="2ed82-160">Configure the views</span></span>](#configure-the-views)

### <a name="add-the-entity-framework-nuget-package"></a><span data-ttu-id="2ed82-161">Add the Entity Framework NuGet package</span><span class="sxs-lookup"><span data-stu-id="2ed82-161">Add the Entity Framework NuGet package</span></span>

1. <span data-ttu-id="2ed82-162">Click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span><span class="sxs-lookup"><span data-stu-id="2ed82-162">Click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="2ed82-163">Run the following command from the **Package Manager Console** window.</span><span class="sxs-lookup"><span data-stu-id="2ed82-163">Run the following command from the **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="2ed82-164">For more information about this package, see the [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span><span class="sxs-lookup"><span data-stu-id="2ed82-164">For more information about this package, see the [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-the-model"></a><span data-ttu-id="2ed82-165">Add the model</span><span class="sxs-lookup"><span data-stu-id="2ed82-165">Add the model</span></span>
1. <span data-ttu-id="2ed82-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Add model][cache-model-add-class]
2. <span data-ttu-id="2ed82-168">Enter `Team` for the class name and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-168">Enter `Team` for the class name and click **Add**.</span></span>
   
    ![Add model class][cache-model-add-class-dialog]
3. <span data-ttu-id="2ed82-170">Replace the `using` statements at the top of the `Team.cs` file with the following `using` statements.</span><span class="sxs-lookup"><span data-stu-id="2ed82-170">Replace the `using` statements at the top of the `Team.cs` file with the following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="2ed82-171">Replace the definition of the `Team` class with the following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span><span class="sxs-lookup"><span data-stu-id="2ed82-171">Replace the definition of the `Team` class with the following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="2ed82-172">For more information on the code first approach to Entity Framework that's used in this tutorial, see [Code first to a new database](https://msdn.microsoft.com/data/jj193542).</span><span class="sxs-lookup"><span data-stu-id="2ed82-172">For more information on the code first approach to Entity Framework that's used in this tutorial, see [Code first to a new database](https://msdn.microsoft.com/data/jj193542).</span></span>

    ```c#
    public class Team
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public int Wins { get; set; }
        public int Losses { get; set; }
        public int Ties { get; set; }
    
        static public void PlayGames(IEnumerable<Team> teams)
        {
            // Simple random generation of statistics.
            Random r = new Random();
    
            foreach (var t in teams)
            {
                t.Wins = r.Next(33);
                t.Losses = r.Next(33);
                t.Ties = r.Next(0, 5);
            }
        }
    }
    
    public class TeamContext : DbContext
    {
        public TeamContext()
            : base("TeamContext")
        {
        }
    
        public DbSet<Team> Teams { get; set; }
    }
    
    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
    {
        protected override void Seed(TeamContext context)
        {
            var teams = new List<Team>
            {
                new Team{Name="Adventure Works Cycles"},
                new Team{Name="Alpine Ski House"},
                new Team{Name="Blue Yonder Airlines"},
                new Team{Name="Coho Vineyard"},
                new Team{Name="Contoso, Ltd."},
                new Team{Name="Fabrikam, Inc."},
                new Team{Name="Lucerne Publishing"},
                new Team{Name="Northwind Traders"},
                new Team{Name="Consolidated Messenger"},
                new Team{Name="Fourth Coffee"},
                new Team{Name="Graphic Design Institute"},
                new Team{Name="Nod Publishers"}
            };
    
            Team.PlayGames(teams);
    
            teams.ForEach(t => context.Teams.Add(t));
            context.SaveChanges();
        }
    }
    
    public class TeamConfiguration : DbConfiguration
    {
        public TeamConfiguration()
        {
            SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
        }
    }
    ```


1. <span data-ttu-id="2ed82-173">In **Solution Explorer**, double-click **web.config** to open it.</span><span class="sxs-lookup"><span data-stu-id="2ed82-173">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="2ed82-175">Add the following `connectionStrings` section.</span><span class="sxs-lookup"><span data-stu-id="2ed82-175">Add the following `connectionStrings` section.</span></span> <span data-ttu-id="2ed82-176">The name of the connection string must match the name of the Entity Framework database context class which is `TeamContext`.</span><span class="sxs-lookup"><span data-stu-id="2ed82-176">The name of the connection string must match the name of the Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\v11.0;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="2ed82-177">You can add the new `connectionStrings` section so that it follows `configSections`, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="2ed82-177">You can add the new `connectionStrings` section so that it follows `configSections`, as shown in the following example.</span></span>

    ```xml
    <configuration>
      <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
      </configSections>
      <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\v11.0;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
      </connectionStrings>
      ...
      ```

### <a name="add-the-controller"></a><span data-ttu-id="2ed82-178">Add the controller</span><span class="sxs-lookup"><span data-stu-id="2ed82-178">Add the controller</span></span>
1. <span data-ttu-id="2ed82-179">Press **F6** to build the project.</span><span class="sxs-lookup"><span data-stu-id="2ed82-179">Press **F6** to build the project.</span></span> 
2. <span data-ttu-id="2ed82-180">In **Solution Explorer**, right-click the **Controllers** folder and choose **Add**, **Controller**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-180">In **Solution Explorer**, right-click the **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Add controller][cache-add-controller]
3. <span data-ttu-id="2ed82-182">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-182">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="2ed82-183">If you get an error after clicking **Add**, ensure that you have built the project first.</span><span class="sxs-lookup"><span data-stu-id="2ed82-183">If you get an error after clicking **Add**, ensure that you have built the project first.</span></span>
   
    ![Add controller class][cache-add-controller-class]
4. <span data-ttu-id="2ed82-185">Select **Team (ContosoTeamStats.Models)** from the **Model class** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="2ed82-185">Select **Team (ContosoTeamStats.Models)** from the **Model class** drop-down list.</span></span> <span data-ttu-id="2ed82-186">Select **TeamContext (ContosoTeamStats.Models)** from the **Data context class** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="2ed82-186">Select **TeamContext (ContosoTeamStats.Models)** from the **Data context class** drop-down list.</span></span> <span data-ttu-id="2ed82-187">Type `TeamsController` in the **Controller** name textbox (if it is not automatically populated).</span><span class="sxs-lookup"><span data-stu-id="2ed82-187">Type `TeamsController` in the **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="2ed82-188">Click **Add** to create the controller class and add the default views.</span><span class="sxs-lookup"><span data-stu-id="2ed82-188">Click **Add** to create the controller class and add the default views.</span></span>
   
    ![Configure controller][cache-configure-controller]
5. <span data-ttu-id="2ed82-190">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** to open it.</span><span class="sxs-lookup"><span data-stu-id="2ed82-190">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** to open it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="2ed82-192">Add the following two `using` statements at the top of the file under the other `using` statements.</span><span class="sxs-lookup"><span data-stu-id="2ed82-192">Add the following two `using` statements at the top of the file under the other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="2ed82-193">Add the following line of code at the end of the `Application_Start` method.</span><span class="sxs-lookup"><span data-stu-id="2ed82-193">Add the following line of code at the end of the `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="2ed82-194">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span><span class="sxs-lookup"><span data-stu-id="2ed82-194">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="2ed82-196">Replace `controller = "Home"` in the following code in the `RegisterRoutes` method with `controller = "Teams"` as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="2ed82-196">Replace `controller = "Home"` in the following code in the `RegisterRoutes` method with `controller = "Teams"` as shown in the following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-the-views"></a><span data-ttu-id="2ed82-197">Configure the views</span><span class="sxs-lookup"><span data-stu-id="2ed82-197">Configure the views</span></span>
1. <span data-ttu-id="2ed82-198">In **Solution Explorer**, expand the **Views** folder and then the **Shared** folder, and double-click **_Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-198">In **Solution Explorer**, expand the **Views** folder and then the **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="2ed82-200">Change the contents of the `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="2ed82-200">Change the contents of the `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in the following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="2ed82-201">In the `body` section, update the first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span><span class="sxs-lookup"><span data-stu-id="2ed82-201">In the `body` section, update the first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="2ed82-202">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="2ed82-202">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="2ed82-203">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="2ed82-203">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Code changes][cache-layout-cshtml-code]
2. <span data-ttu-id="2ed82-205">Press **Ctrl+F5** to build and run the application.</span><span class="sxs-lookup"><span data-stu-id="2ed82-205">Press **Ctrl+F5** to build and run the application.</span></span> <span data-ttu-id="2ed82-206">This version of the application reads the results directly from the database.</span><span class="sxs-lookup"><span data-stu-id="2ed82-206">This version of the application reads the results directly from the database.</span></span> <span data-ttu-id="2ed82-207">Note the **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added to the application by the **MVC 5 Controller with views, using Entity Framework** scaffold.</span><span class="sxs-lookup"><span data-stu-id="2ed82-207">Note the **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added to the application by the **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="2ed82-208">In the next section of the tutorial you'll add Redis Cache to optimize the data access and provide additional features to the application.</span><span class="sxs-lookup"><span data-stu-id="2ed82-208">In the next section of the tutorial you'll add Redis Cache to optimize the data access and provide additional features to the application.</span></span>

![Starter application][cache-starter-application]

## <a name="configure-the-application-to-use-redis-cache"></a><span data-ttu-id="2ed82-210">Configure the application to use Redis Cache</span><span class="sxs-lookup"><span data-stu-id="2ed82-210">Configure the application to use Redis Cache</span></span>
<span data-ttu-id="2ed82-211">In this section of the tutorial, you'll configure the sample application to store and retrieve Contoso team statistics from an Azure Redis Cache instance by using the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span><span class="sxs-lookup"><span data-stu-id="2ed82-211">In this section of the tutorial, you'll configure the sample application to store and retrieve Contoso team statistics from an Azure Redis Cache instance by using the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="2ed82-212">Configure the application to use StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="2ed82-212">Configure the application to use StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="2ed82-213">Update the TeamsController class to return results from the cache or the database</span><span class="sxs-lookup"><span data-stu-id="2ed82-213">Update the TeamsController class to return results from the cache or the database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="2ed82-214">Update the Create, Edit, and Delete methods to work with the cache</span><span class="sxs-lookup"><span data-stu-id="2ed82-214">Update the Create, Edit, and Delete methods to work with the cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="2ed82-215">Update the Teams Index view to work with the cache</span><span class="sxs-lookup"><span data-stu-id="2ed82-215">Update the Teams Index view to work with the cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-the-application-to-use-stackexchangeredis"></a><span data-ttu-id="2ed82-216">Configure the application to use StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="2ed82-216">Configure the application to use StackExchange.Redis</span></span>
1. <span data-ttu-id="2ed82-217">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span><span class="sxs-lookup"><span data-stu-id="2ed82-217">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="2ed82-218">Run the following command from the `Package Manager Console` window.</span><span class="sxs-lookup"><span data-stu-id="2ed82-218">Run the following command from the `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="2ed82-219">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span><span class="sxs-lookup"><span data-stu-id="2ed82-219">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span></span> <span data-ttu-id="2ed82-220">If you prefer to use a strong-named version of the `StackExchange.Redis` client library, install the `StackExchange.Redis.StrongName` package.</span><span class="sxs-lookup"><span data-stu-id="2ed82-220">If you prefer to use a strong-named version of the `StackExchange.Redis` client library, install the `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="2ed82-221">In **Solution Explorer**, expand the **Controllers** folder and double-click **TeamsController.cs** to open it.</span><span class="sxs-lookup"><span data-stu-id="2ed82-221">In **Solution Explorer**, expand the **Controllers** folder and double-click **TeamsController.cs** to open it.</span></span>
   
    ![Teams controller][cache-teamscontroller]
4. <span data-ttu-id="2ed82-223">Add the following two `using` statements to **TeamsController.cs**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-223">Add the following two `using` statements to **TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="2ed82-224">Add the following two properties to the `TeamsController` class.</span><span class="sxs-lookup"><span data-stu-id="2ed82-224">Add the following two properties to the `TeamsController` class.</span></span>

    ```c#   
    // Redis Connection string info
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

6. <span data-ttu-id="2ed82-225">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with the source code of your sample application, should you decide to check it in somewhere.</span><span class="sxs-lookup"><span data-stu-id="2ed82-225">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with the source code of your sample application, should you decide to check it in somewhere.</span></span> <span data-ttu-id="2ed82-226">In this example the `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="2ed82-226">In this example the `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="2ed82-227">Edit the `WebAppPlusCacheAppSecrets.config` file and add the following contents.</span><span class="sxs-lookup"><span data-stu-id="2ed82-227">Edit the `WebAppPlusCacheAppSecrets.config` file and add the following contents.</span></span> <span data-ttu-id="2ed82-228">If you run the application locally this information is used to connect to your Azure Redis Cache instance.</span><span class="sxs-lookup"><span data-stu-id="2ed82-228">If you run the application locally this information is used to connect to your Azure Redis Cache instance.</span></span> <span data-ttu-id="2ed82-229">Later in the tutorial you'll provision an Azure Redis Cache instance and update the cache name and password.</span><span class="sxs-lookup"><span data-stu-id="2ed82-229">Later in the tutorial you'll provision an Azure Redis Cache instance and update the cache name and password.</span></span> <span data-ttu-id="2ed82-230">If you don't plan to run the sample application locally you can skip the creation of this file and the subsequent steps that reference the file, because when you deploy to Azure the application retrieves the cache connection information from the app setting for the Web App and not from this file.</span><span class="sxs-lookup"><span data-stu-id="2ed82-230">If you don't plan to run the sample application locally you can skip the creation of this file and the subsequent steps that reference the file, because when you deploy to Azure the application retrieves the cache connection information from the app setting for the Web App and not from this file.</span></span> <span data-ttu-id="2ed82-231">Since the `WebAppPlusCacheAppSecrets.config` is not deployed to Azure with your application, you don't need it unless you are going to run the application locally.</span><span class="sxs-lookup"><span data-stu-id="2ed82-231">Since the `WebAppPlusCacheAppSecrets.config` is not deployed to Azure with your application, you don't need it unless you are going to run the application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="2ed82-232">In **Solution Explorer**, double-click **web.config** to open it.</span><span class="sxs-lookup"><span data-stu-id="2ed82-232">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="2ed82-234">Add the following `file` attribute to the `appSettings` element.</span><span class="sxs-lookup"><span data-stu-id="2ed82-234">Add the following `file` attribute to the `appSettings` element.</span></span> <span data-ttu-id="2ed82-235">If you used a different file name or location, substitute those values for the ones shown in the example.</span><span class="sxs-lookup"><span data-stu-id="2ed82-235">If you used a different file name or location, substitute those values for the ones shown in the example.</span></span>
   
   * <span data-ttu-id="2ed82-236">Before: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="2ed82-236">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="2ed82-237">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="2ed82-237">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="2ed82-238">The ASP.NET runtime merges the contents of the external file with the markup in the `<appSettings>` element.</span><span class="sxs-lookup"><span data-stu-id="2ed82-238">The ASP.NET runtime merges the contents of the external file with the markup in the `<appSettings>` element.</span></span> <span data-ttu-id="2ed82-239">The runtime ignores the file attribute if the specified file cannot be found.</span><span class="sxs-lookup"><span data-stu-id="2ed82-239">The runtime ignores the file attribute if the specified file cannot be found.</span></span> <span data-ttu-id="2ed82-240">Your secrets (the connection string to your cache) are not included as part of the source code for the application.</span><span class="sxs-lookup"><span data-stu-id="2ed82-240">Your secrets (the connection string to your cache) are not included as part of the source code for the application.</span></span> <span data-ttu-id="2ed82-241">When you deploy your web app to Azure, the `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span><span class="sxs-lookup"><span data-stu-id="2ed82-241">When you deploy your web app to Azure, the `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="2ed82-242">There are several ways to specify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision the Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span><span class="sxs-lookup"><span data-stu-id="2ed82-242">There are several ways to specify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision the Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="2ed82-243">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span><span class="sxs-lookup"><span data-stu-id="2ed82-243">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database"></a><span data-ttu-id="2ed82-244">Update the TeamsController class to return results from the cache or the database</span><span class="sxs-lookup"><span data-stu-id="2ed82-244">Update the TeamsController class to return results from the cache or the database</span></span>
<span data-ttu-id="2ed82-245">In this sample, team statistics can be retrieved from the database or from the cache.</span><span class="sxs-lookup"><span data-stu-id="2ed82-245">In this sample, team statistics can be retrieved from the database or from the cache.</span></span> <span data-ttu-id="2ed82-246">Team statistics are stored in the cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span><span class="sxs-lookup"><span data-stu-id="2ed82-246">Team statistics are stored in the cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="2ed82-247">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span><span class="sxs-lookup"><span data-stu-id="2ed82-247">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="2ed82-248">In this sample you'll query the sorted set for the top 5 teams ranked by number of wins.</span><span class="sxs-lookup"><span data-stu-id="2ed82-248">In this sample you'll query the sorted set for the top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> It is not required to store the team statistics in multiple formats in the cache in order to use Azure Redis Cache. This tutorial uses multiple formats to demonstrate some of the different ways and different data types you can use to cache data.
> 
> 

1. <span data-ttu-id="2ed82-251">Add the following `using` statements to the `TeamsController.cs` file at the top with the other `using` statements.</span><span class="sxs-lookup"><span data-stu-id="2ed82-251">Add the following `using` statements to the `TeamsController.cs` file at the top with the other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="2ed82-252">Replace the current `public ActionResult Index()` method implementation with the following implementation.</span><span class="sxs-lookup"><span data-stu-id="2ed82-252">Replace the current `public ActionResult Index()` method implementation with the following implementation.</span></span>

    ```c#
    // GET: Teams
    public ActionResult Index(string actionType, string resultType)
    {
        List<Team> teams = null;

        switch(actionType)
        {
            case "playGames": // Play a new season of games.
                PlayGames();
                break;

            case "clearCache": // Clear the results from the cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild the database with sample data.
                RebuildDB();
                break;
        }

        // Measure the time it takes to retrieve the results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve the top 5 teams from the sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from the cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from the database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add the elapsed time of the operation to the ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="2ed82-253">Add the following three methods to the `TeamsController` class to implement the `playGames`, `clearCache`, and `rebuildDB` action types from the switch statement added in the previous code snippet.</span><span class="sxs-lookup"><span data-stu-id="2ed82-253">Add the following three methods to the `TeamsController` class to implement the `playGames`, `clearCache`, and `rebuildDB` action types from the switch statement added in the previous code snippet.</span></span>
   
    <span data-ttu-id="2ed82-254">The `PlayGames` method updates the team statistics by simulating a season of games, saves the results to the database, and clears the now outdated data from the cache.</span><span class="sxs-lookup"><span data-stu-id="2ed82-254">The `PlayGames` method updates the team statistics by simulating a season of games, saves the results to the database, and clears the now outdated data from the cache.</span></span>

    ```c#
    void PlayGames()
    {
        ViewBag.msg += "Updating team statistics. ";
        // Play a "season" of games.
        var teams = from t in db.Teams
                    select t;

        Team.PlayGames(teams);

        db.SaveChanges();

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="2ed82-255">The `RebuildDB` method reinitializes the database with the default set of teams, generates statistics for them, and clears the now outdated data from the cache.</span><span class="sxs-lookup"><span data-stu-id="2ed82-255">The `RebuildDB` method reinitializes the database with the default set of teams, generates statistics for them, and clears the now outdated data from the cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize the database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="2ed82-256">The `ClearCachedTeams` method removes any cached team statistics from the cache.</span><span class="sxs-lookup"><span data-stu-id="2ed82-256">The `ClearCachedTeams` method removes any cached team statistics from the cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="2ed82-257">Add the following four methods to the `TeamsController` class to implement the various ways of retrieving the team statistics from the cache and the database.</span><span class="sxs-lookup"><span data-stu-id="2ed82-257">Add the following four methods to the `TeamsController` class to implement the various ways of retrieving the team statistics from the cache and the database.</span></span> <span data-ttu-id="2ed82-258">Each of these methods returns a `List<Team>` which is then displayed by the view.</span><span class="sxs-lookup"><span data-stu-id="2ed82-258">Each of these methods returns a `List<Team>` which is then displayed by the view.</span></span>
   
    <span data-ttu-id="2ed82-259">The `GetFromDB` method reads the team statistics from the database.</span><span class="sxs-lookup"><span data-stu-id="2ed82-259">The `GetFromDB` method reads the team statistics from the database.</span></span>
   
    ```c#
    List<Team> GetFromDB()
    {
        ViewBag.msg += "Results read from DB. ";
        var results = from t in db.Teams
            orderby t.Wins descending
            select t; 

        return results.ToList<Team>();
    }
    ```

    <span data-ttu-id="2ed82-260">The `GetFromList` method reads the team statistics from cache as a serialized `List<Team>`.</span><span class="sxs-lookup"><span data-stu-id="2ed82-260">The `GetFromList` method reads the team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="2ed82-261">If there is a cache miss, the team statistics are read from the database and then stored in the cache for next time.</span><span class="sxs-lookup"><span data-stu-id="2ed82-261">If there is a cache miss, the team statistics are read from the database and then stored in the cache for next time.</span></span> <span data-ttu-id="2ed82-262">In this sample we're using JSON.NET serialization to serialize the .NET objects to and from the cache.</span><span class="sxs-lookup"><span data-stu-id="2ed82-262">In this sample we're using JSON.NET serialization to serialize the .NET objects to and from the cache.</span></span> <span data-ttu-id="2ed82-263">For more information, see [How to work with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span><span class="sxs-lookup"><span data-stu-id="2ed82-263">For more information, see [How to work with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

    ```c#
    List<Team> GetFromList()
    {
        List<Team> teams = null;

        IDatabase cache = Connection.GetDatabase();
        string serializedTeams = cache.StringGet("teamsList");
        if (!String.IsNullOrEmpty(serializedTeams))
        {
            teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

            ViewBag.msg += "List read from cache. ";
        }
        else
        {
            ViewBag.msg += "Teams list cache miss. ";
            // Get from database and store in cache
            teams = GetFromDB();

            ViewBag.msg += "Storing results to cache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="2ed82-264">The `GetFromSortedSet` method reads the team statistics from a cached sorted set.</span><span class="sxs-lookup"><span data-stu-id="2ed82-264">The `GetFromSortedSet` method reads the team statistics from a cached sorted set.</span></span> <span data-ttu-id="2ed82-265">If there is a cache miss, the team statistics are read from the database and stored in the cache as a sorted set.</span><span class="sxs-lookup"><span data-stu-id="2ed82-265">If there is a cache miss, the team statistics are read from the database and stored in the cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
        if (teamsSortedSet.Count() > 0)
        {
            ViewBag.msg += "Reading sorted set from cache. ";
            teams = new List<Team>();
            foreach (var t in teamsSortedSet)
            {
                Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                teams.Add(tt);
            }
        }
        else
        {
            ViewBag.msg += "Teams sorted set cache miss. ";

            // Read from DB
            teams = GetFromDB();

            ViewBag.msg += "Storing results to cache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding to sorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="2ed82-266">The `GetFromSortedSetTop5` method reads the top 5 teams from the cached sorted set.</span><span class="sxs-lookup"><span data-stu-id="2ed82-266">The `GetFromSortedSetTop5` method reads the top 5 teams from the cached sorted set.</span></span> <span data-ttu-id="2ed82-267">It starts by checking the cache for the existence of the `teamsSortedSet` key.</span><span class="sxs-lookup"><span data-stu-id="2ed82-267">It starts by checking the cache for the existence of the `teamsSortedSet` key.</span></span> <span data-ttu-id="2ed82-268">If this key is not present, the `GetFromSortedSet` method is called to read the team statistics and store them in the cache.</span><span class="sxs-lookup"><span data-stu-id="2ed82-268">If this key is not present, the `GetFromSortedSet` method is called to read the team statistics and store them in the cache.</span></span> <span data-ttu-id="2ed82-269">Next, the cached sorted set is queried for the top 5 teams which are returned.</span><span class="sxs-lookup"><span data-stu-id="2ed82-269">Next, the cached sorted set is queried for the top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load the entire sorted set into the cache.
            GetFromSortedSet();

            // Retrieve the top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get the top 5 teams from the sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-the-create-edit-and-delete-methods-to-work-with-the-cache"></a><span data-ttu-id="2ed82-270">Update the Create, Edit, and Delete methods to work with the cache</span><span class="sxs-lookup"><span data-stu-id="2ed82-270">Update the Create, Edit, and Delete methods to work with the cache</span></span>
<span data-ttu-id="2ed82-271">The scaffolding code that was generated as part of this sample includes methods to add, edit, and delete teams.</span><span class="sxs-lookup"><span data-stu-id="2ed82-271">The scaffolding code that was generated as part of this sample includes methods to add, edit, and delete teams.</span></span> <span data-ttu-id="2ed82-272">Anytime a team is added, edited, or removed, the data in the cache becomes outdated.</span><span class="sxs-lookup"><span data-stu-id="2ed82-272">Anytime a team is added, edited, or removed, the data in the cache becomes outdated.</span></span> <span data-ttu-id="2ed82-273">In this section you'll modify these three methods to clear the cached teams so that the cache won't be out of sync with the database.</span><span class="sxs-lookup"><span data-stu-id="2ed82-273">In this section you'll modify these three methods to clear the cached teams so that the cache won't be out of sync with the database.</span></span>

1. <span data-ttu-id="2ed82-274">Browse to the `Create(Team team)` method in the `TeamsController` class.</span><span class="sxs-lookup"><span data-stu-id="2ed82-274">Browse to the `Create(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="2ed82-275">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="2ed82-275">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Create
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="2ed82-276">Browse to the `Edit(Team team)` method in the `TeamsController` class.</span><span class="sxs-lookup"><span data-stu-id="2ed82-276">Browse to the `Edit(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="2ed82-277">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="2ed82-277">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="2ed82-278">Browse to the `DeleteConfirmed(int id)` method in the `TeamsController` class.</span><span class="sxs-lookup"><span data-stu-id="2ed82-278">Browse to the `DeleteConfirmed(int id)` method in the `TeamsController` class.</span></span> <span data-ttu-id="2ed82-279">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="2ed82-279">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, the cache is out of date.
        // Clear the cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-the-teams-index-view-to-work-with-the-cache"></a><span data-ttu-id="2ed82-280">Update the Teams Index view to work with the cache</span><span class="sxs-lookup"><span data-stu-id="2ed82-280">Update the Teams Index view to work with the cache</span></span>
1. <span data-ttu-id="2ed82-281">In **Solution Explorer**, expand the **Views** folder, then the **Teams** folder, and double-click **Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-281">In **Solution Explorer**, expand the **Views** folder, then the **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="2ed82-283">Near the top of the file, look for the following paragraph element.</span><span class="sxs-lookup"><span data-stu-id="2ed82-283">Near the top of the file, look for the following paragraph element.</span></span>
   
    ![Action table][cache-teams-index-table]
   
    <span data-ttu-id="2ed82-285">This is the link to create a new team.</span><span class="sxs-lookup"><span data-stu-id="2ed82-285">This is the link to create a new team.</span></span> <span data-ttu-id="2ed82-286">Replace the paragraph element with the following table.</span><span class="sxs-lookup"><span data-stu-id="2ed82-286">Replace the paragraph element with the following table.</span></span> <span data-ttu-id="2ed82-287">This table has action links for creating a new team, playing a new season of games, clearing the cache, retrieving the teams from the cache in several formats, retrieving the teams from the database, and rebuilding the database with fresh sample data.</span><span class="sxs-lookup"><span data-stu-id="2ed82-287">This table has action links for creating a new team, playing a new season of games, clearing the cache, retrieving the teams from the cache in several formats, retrieving the teams from the database, and rebuilding the database with fresh sample data.</span></span>

    ```html
    <table class="table">
        <tr>
            <td>
                @Html.ActionLink("Create New", "Create")
            </td>
            <td>
                @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
            </td>
            <td>
                @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
            </td>
            <td>
                @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
            </td>
            <td>
                @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
            </td>
            <td>
                @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
            </td>
            <td>
                @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
            </td>
            <td>
                @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
            </td>
        </tr>    
    </table>
    ```


1. <span data-ttu-id="2ed82-288">Scroll to the bottom of the **Index.cshtml** file and add the following `tr` element so that it is the last row in the last table in the file.</span><span class="sxs-lookup"><span data-stu-id="2ed82-288">Scroll to the bottom of the **Index.cshtml** file and add the following `tr` element so that it is the last row in the last table in the file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="2ed82-289">This row displays the value of `ViewBag.Msg` which contains a status report about the current operation.</span><span class="sxs-lookup"><span data-stu-id="2ed82-289">This row displays the value of `ViewBag.Msg` which contains a status report about the current operation.</span></span> <span data-ttu-id="2ed82-290">The `ViewBag.Msg` is set when you click any of the action links from the previous step.</span><span class="sxs-lookup"><span data-stu-id="2ed82-290">The `ViewBag.Msg` is set when you click any of the action links from the previous step.</span></span>   
   
    ![Status message][cache-status-message]
2. <span data-ttu-id="2ed82-292">Press **F6** to build the project.</span><span class="sxs-lookup"><span data-stu-id="2ed82-292">Press **F6** to build the project.</span></span>

## <a name="provision-the-azure-resources"></a><span data-ttu-id="2ed82-293">Provision the Azure resources</span><span class="sxs-lookup"><span data-stu-id="2ed82-293">Provision the Azure resources</span></span>
<span data-ttu-id="2ed82-294">To host your application in Azure, you must first provision the Azure services that your application requires.</span><span class="sxs-lookup"><span data-stu-id="2ed82-294">To host your application in Azure, you must first provision the Azure services that your application requires.</span></span> <span data-ttu-id="2ed82-295">The sample application in this tutorial uses the following Azure services.</span><span class="sxs-lookup"><span data-stu-id="2ed82-295">The sample application in this tutorial uses the following Azure services.</span></span>

* <span data-ttu-id="2ed82-296">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="2ed82-296">Azure Redis Cache</span></span>
* <span data-ttu-id="2ed82-297">App Service Web App</span><span class="sxs-lookup"><span data-stu-id="2ed82-297">App Service Web App</span></span>
* <span data-ttu-id="2ed82-298">SQL Database</span><span class="sxs-lookup"><span data-stu-id="2ed82-298">SQL Database</span></span>

<span data-ttu-id="2ed82-299">To deploy these services to a new or existing resource group of your choice, click the following **Deploy to Azure** button.</span><span class="sxs-lookup"><span data-stu-id="2ed82-299">To deploy these services to a new or existing resource group of your choice, click the following **Deploy to Azure** button.</span></span>

<span data-ttu-id="2ed82-300">[![Deploy to Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="2ed82-300">[![Deploy to Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="2ed82-301">This **Deploy to Azure** button uses the [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template to provision these services and set the connection string for the SQL Database and the application setting for the Azure Redis Cache connection string.</span><span class="sxs-lookup"><span data-stu-id="2ed82-301">This **Deploy to Azure** button uses the [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template to provision these services and set the connection string for the SQL Database and the application setting for the Azure Redis Cache connection string.</span></span>

> [!NOTE]
> If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.
> 
> 

<span data-ttu-id="2ed82-303">Clicking the **Deploy to Azure** button takes you to the Azure portal and initiates the process of creating the resources described by the template.</span><span class="sxs-lookup"><span data-stu-id="2ed82-303">Clicking the **Deploy to Azure** button takes you to the Azure portal and initiates the process of creating the resources described by the template.</span></span>

![Deploy to Azure][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="2ed82-305">In the **Basics** section, select the Azure subscription to use, and select an existing resource group or create a new one, and specify the resource group location.</span><span class="sxs-lookup"><span data-stu-id="2ed82-305">In the **Basics** section, select the Azure subscription to use, and select an existing resource group or create a new one, and specify the resource group location.</span></span>
2. <span data-ttu-id="2ed82-306">In the **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-306">In the **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="2ed82-307">The other parameters are configured for a free App Service hosting plan, and lower-cost options for the SQL Database and Azure Redis Cache, which don't come with a free tier.</span><span class="sxs-lookup"><span data-stu-id="2ed82-307">The other parameters are configured for a free App Service hosting plan, and lower-cost options for the SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![Deploy to Azure][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="2ed82-309">After configuring the desired settings, scroll to the end of the page, read the terms and conditions, and check the **I agree to the terms and conditions stated above** checkbox.</span><span class="sxs-lookup"><span data-stu-id="2ed82-309">After configuring the desired settings, scroll to the end of the page, read the terms and conditions, and check the **I agree to the terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="2ed82-310">To begin provisioning the resources, click **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-310">To begin provisioning the resources, click **Purchase**.</span></span>

<span data-ttu-id="2ed82-311">To view the progress of your deployment, click the notification icon and click **Deployment started**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-311">To view the progress of your deployment, click the notification icon and click **Deployment started**.</span></span>

![Deployment started][cache-deployment-started]

<span data-ttu-id="2ed82-313">You can view the status of your deployment on the **Microsoft.Template** blade.</span><span class="sxs-lookup"><span data-stu-id="2ed82-313">You can view the status of your deployment on the **Microsoft.Template** blade.</span></span>

![Deploy to Azure][cache-deploy-to-azure-step-3]

<span data-ttu-id="2ed82-315">When provisioning is complete, you can publish your application to Azure from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ed82-315">When provisioning is complete, you can publish your application to Azure from Visual Studio.</span></span>

> [!NOTE]
> Any errors that may occur during the provisioning process are displayed on the **Microsoft.Template** blade. Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription. Resolve any errors and restart the process by clicking **Redeploy** on the **Microsoft.Template** blade or the **Deploy to Azure** button in this tutorial.
> 
> 

## <a name="publish-the-application-to-azure"></a><span data-ttu-id="2ed82-319">Publish the application to Azure</span><span class="sxs-lookup"><span data-stu-id="2ed82-319">Publish the application to Azure</span></span>
<span data-ttu-id="2ed82-320">In this step of the tutorial, you'll publish the application to Azure and run it in the cloud.</span><span class="sxs-lookup"><span data-stu-id="2ed82-320">In this step of the tutorial, you'll publish the application to Azure and run it in the cloud.</span></span>

1. <span data-ttu-id="2ed82-321">Right-click the **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-321">Right-click the **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Publish][cache-publish-app]
2. <span data-ttu-id="2ed82-323">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-323">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Publish][cache-publish-to-app-service]
3. <span data-ttu-id="2ed82-325">Select the subscription used when creating the Azure resources, expand the resource group containing the resources, and select the desired Web App.</span><span class="sxs-lookup"><span data-stu-id="2ed82-325">Select the subscription used when creating the Azure resources, expand the resource group containing the resources, and select the desired Web App.</span></span> <span data-ttu-id="2ed82-326">If you used the **Deploy to Azure** button your Web App name starts with **webSite** followed by some additional characters.</span><span class="sxs-lookup"><span data-stu-id="2ed82-326">If you used the **Deploy to Azure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Select Web App][cache-select-web-app]
4. <span data-ttu-id="2ed82-328">Click **OK** to begin the publishing process.</span><span class="sxs-lookup"><span data-stu-id="2ed82-328">Click **OK** to begin the publishing process.</span></span> <span data-ttu-id="2ed82-329">After a few moments the publishing process completes and a browser is launched with the running sample application.</span><span class="sxs-lookup"><span data-stu-id="2ed82-329">After a few moments the publishing process completes and a browser is launched with the running sample application.</span></span> <span data-ttu-id="2ed82-330">If you get a DNS error when validating or publishing, and the provisioning process for the Azure resources for the application has just recently completed, wait a moment and try again.</span><span class="sxs-lookup"><span data-stu-id="2ed82-330">If you get a DNS error when validating or publishing, and the provisioning process for the Azure resources for the application has just recently completed, wait a moment and try again.</span></span>
   
    ![Cache added][cache-added-to-application]

<span data-ttu-id="2ed82-332">The following table describes each action link from the sample application.</span><span class="sxs-lookup"><span data-stu-id="2ed82-332">The following table describes each action link from the sample application.</span></span>

| <span data-ttu-id="2ed82-333">Action</span><span class="sxs-lookup"><span data-stu-id="2ed82-333">Action</span></span> | <span data-ttu-id="2ed82-334">Description</span><span class="sxs-lookup"><span data-stu-id="2ed82-334">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2ed82-335">Create New</span><span class="sxs-lookup"><span data-stu-id="2ed82-335">Create New</span></span> |<span data-ttu-id="2ed82-336">Create a new Team.</span><span class="sxs-lookup"><span data-stu-id="2ed82-336">Create a new Team.</span></span> |
| <span data-ttu-id="2ed82-337">Play Season</span><span class="sxs-lookup"><span data-stu-id="2ed82-337">Play Season</span></span> |<span data-ttu-id="2ed82-338">Play a season of games, update the team stats, and clear any outdated team data from the cache.</span><span class="sxs-lookup"><span data-stu-id="2ed82-338">Play a season of games, update the team stats, and clear any outdated team data from the cache.</span></span> |
| <span data-ttu-id="2ed82-339">Clear Cache</span><span class="sxs-lookup"><span data-stu-id="2ed82-339">Clear Cache</span></span> |<span data-ttu-id="2ed82-340">Clear the team stats from the cache.</span><span class="sxs-lookup"><span data-stu-id="2ed82-340">Clear the team stats from the cache.</span></span> |
| <span data-ttu-id="2ed82-341">List from Cache</span><span class="sxs-lookup"><span data-stu-id="2ed82-341">List from Cache</span></span> |<span data-ttu-id="2ed82-342">Retrieve the team stats from the cache.</span><span class="sxs-lookup"><span data-stu-id="2ed82-342">Retrieve the team stats from the cache.</span></span> <span data-ttu-id="2ed82-343">If there is a cache miss, load the stats from the database and save to the cache for next time.</span><span class="sxs-lookup"><span data-stu-id="2ed82-343">If there is a cache miss, load the stats from the database and save to the cache for next time.</span></span> |
| <span data-ttu-id="2ed82-344">Sorted Set from Cache</span><span class="sxs-lookup"><span data-stu-id="2ed82-344">Sorted Set from Cache</span></span> |<span data-ttu-id="2ed82-345">Retrieve the team stats from the cache using a sorted set.</span><span class="sxs-lookup"><span data-stu-id="2ed82-345">Retrieve the team stats from the cache using a sorted set.</span></span> <span data-ttu-id="2ed82-346">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span><span class="sxs-lookup"><span data-stu-id="2ed82-346">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="2ed82-347">Top 5 Teams from Cache</span><span class="sxs-lookup"><span data-stu-id="2ed82-347">Top 5 Teams from Cache</span></span> |<span data-ttu-id="2ed82-348">Retrieve the top 5 teams from the cache using a sorted set.</span><span class="sxs-lookup"><span data-stu-id="2ed82-348">Retrieve the top 5 teams from the cache using a sorted set.</span></span> <span data-ttu-id="2ed82-349">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span><span class="sxs-lookup"><span data-stu-id="2ed82-349">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="2ed82-350">Load from DB</span><span class="sxs-lookup"><span data-stu-id="2ed82-350">Load from DB</span></span> |<span data-ttu-id="2ed82-351">Retrieve the team stats from the database.</span><span class="sxs-lookup"><span data-stu-id="2ed82-351">Retrieve the team stats from the database.</span></span> |
| <span data-ttu-id="2ed82-352">Rebuild DB</span><span class="sxs-lookup"><span data-stu-id="2ed82-352">Rebuild DB</span></span> |<span data-ttu-id="2ed82-353">Rebuild the database and reload it with sample team data.</span><span class="sxs-lookup"><span data-stu-id="2ed82-353">Rebuild the database and reload it with sample team data.</span></span> |
| <span data-ttu-id="2ed82-354">Edit / Details / Delete</span><span class="sxs-lookup"><span data-stu-id="2ed82-354">Edit / Details / Delete</span></span> |<span data-ttu-id="2ed82-355">Edit a team, view details for a team, delete a team.</span><span class="sxs-lookup"><span data-stu-id="2ed82-355">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="2ed82-356">Click some of the actions and experiment with retrieving the data from the different sources.</span><span class="sxs-lookup"><span data-stu-id="2ed82-356">Click some of the actions and experiment with retrieving the data from the different sources.</span></span> <span data-ttu-id="2ed82-357">Not the differences in the time it takes to complete the various ways of retrieving the data from the database and the cache.</span><span class="sxs-lookup"><span data-stu-id="2ed82-357">Not the differences in the time it takes to complete the various ways of retrieving the data from the database and the cache.</span></span>

## <a name="delete-the-resources-when-you-are-finished-with-the-application"></a><span data-ttu-id="2ed82-358">Delete the resources when you are finished with the application</span><span class="sxs-lookup"><span data-stu-id="2ed82-358">Delete the resources when you are finished with the application</span></span>
<span data-ttu-id="2ed82-359">When you are finished with the sample tutorial application, you can delete the Azure resources used in order to conserve cost and resources.</span><span class="sxs-lookup"><span data-stu-id="2ed82-359">When you are finished with the sample tutorial application, you can delete the Azure resources used in order to conserve cost and resources.</span></span> <span data-ttu-id="2ed82-360">If you use the **Deploy to Azure** button in the [Provision the Azure resources](#provision-the-azure-resources) section and all of your resources are contained in the same resource group, you can delete them together in one operation by deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="2ed82-360">If you use the **Deploy to Azure** button in the [Provision the Azure resources](#provision-the-azure-resources) section and all of your resources are contained in the same resource group, you can delete them together in one operation by deleting the resource group.</span></span>

1. <span data-ttu-id="2ed82-361">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-361">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="2ed82-362">Type the name of your resource group into the **Filter items...** textbox.</span><span class="sxs-lookup"><span data-stu-id="2ed82-362">Type the name of your resource group into the **Filter items...** textbox.</span></span>
3. <span data-ttu-id="2ed82-363">Click **...** to the right of your resource group.</span><span class="sxs-lookup"><span data-stu-id="2ed82-363">Click **...** to the right of your resource group.</span></span>
4. <span data-ttu-id="2ed82-364">Click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-364">Click **Delete**.</span></span>
   
    ![Delete][cache-delete-resource-group]
5. <span data-ttu-id="2ed82-366">Type the name of your resource group and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="2ed82-366">Type the name of your resource group and click **Delete**.</span></span>
   
    ![Confirm delete][cache-delete-confirm]

<span data-ttu-id="2ed82-368">After a few moments the resource group and all of its contained resources are deleted.</span><span class="sxs-lookup"><span data-stu-id="2ed82-368">After a few moments the resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> Note that deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted. Make sure that you do not accidentally delete the wrong resource group or resources. If you created the resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.
> 
> 

## <a name="run-the-sample-application-on-your-local-machine"></a><span data-ttu-id="2ed82-372">Run the sample application on your local machine</span><span class="sxs-lookup"><span data-stu-id="2ed82-372">Run the sample application on your local machine</span></span>
<span data-ttu-id="2ed82-373">To run the application locally on your machine, you need an Azure Redis Cache instance in which to cache your data.</span><span class="sxs-lookup"><span data-stu-id="2ed82-373">To run the application locally on your machine, you need an Azure Redis Cache instance in which to cache your data.</span></span> 

* <span data-ttu-id="2ed82-374">If you have published your application to Azure as described in the previous section, you can use the Azure Redis Cache instance that was provisioned during that step.</span><span class="sxs-lookup"><span data-stu-id="2ed82-374">If you have published your application to Azure as described in the previous section, you can use the Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="2ed82-375">If you have another existing Azure Redis Cache instance, you can use that to run this sample locally.</span><span class="sxs-lookup"><span data-stu-id="2ed82-375">If you have another existing Azure Redis Cache instance, you can use that to run this sample locally.</span></span>
* <span data-ttu-id="2ed82-376">If you need to create an Azure Redis Cache instance, you can follow the steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="2ed82-376">If you need to create an Azure Redis Cache instance, you can follow the steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="2ed82-377">Once you have selected or created the cache to use, browse to the cache in the Azure portal and retrieve the [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span><span class="sxs-lookup"><span data-stu-id="2ed82-377">Once you have selected or created the cache to use, browse to the cache in the Azure portal and retrieve the [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="2ed82-378">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="2ed82-378">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="2ed82-379">Open the `WebAppPlusCacheAppSecrets.config` file that you created during the [Configure the application to use Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using the editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="2ed82-379">Open the `WebAppPlusCacheAppSecrets.config` file that you created during the [Configure the application to use Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using the editor of your choice.</span></span>
2. <span data-ttu-id="2ed82-380">Edit the `value` attribute and replace `MyCache.redis.cache.windows.net` with the [host name](cache-configure.md#properties) of your cache, and specify either the [primary or secondary key](cache-configure.md#access-keys) of your cache as the password.</span><span class="sxs-lookup"><span data-stu-id="2ed82-380">Edit the `value` attribute and replace `MyCache.redis.cache.windows.net` with the [host name](cache-configure.md#properties) of your cache, and specify either the [primary or secondary key](cache-configure.md#access-keys) of your cache as the password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="2ed82-381">Press **Ctrl+F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="2ed82-381">Press **Ctrl+F5** to run the application.</span></span>

> [!NOTE]
> Note that because the application, including the database, is running locally and the Redis Cache is hosted in Azure, the cache may appear to under-perform the database. For best performance, the client application and Azure Redis Cache instance should be in the same location. 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2ed82-384">Next steps</span><span class="sxs-lookup"><span data-stu-id="2ed82-384">Next steps</span></span>
* <span data-ttu-id="2ed82-385">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on the [ASP.NET](http://asp.net/) site.</span><span class="sxs-lookup"><span data-stu-id="2ed82-385">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on the [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="2ed82-386">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="2ed82-386">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="2ed82-387">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="2ed82-387">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="2ed82-388">Learn more about the [Code first to a new database](https://msdn.microsoft.com/data/jj193542) approach to Entity Framework that's used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="2ed82-388">Learn more about the [Code first to a new database](https://msdn.microsoft.com/data/jj193542) approach to Entity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="2ed82-389">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ed82-389">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="2ed82-390">Learn how to [monitor](cache-how-to-monitor.md) your cache in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2ed82-390">Learn how to [monitor](cache-how-to-monitor.md) your cache in the Azure portal.</span></span>
* <span data-ttu-id="2ed82-391">Explore Azure Redis Cache premium features</span><span class="sxs-lookup"><span data-stu-id="2ed82-391">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="2ed82-392">How to configure persistence for a Premium Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="2ed82-392">How to configure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="2ed82-393">How to configure clustering for a Premium Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="2ed82-393">How to configure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="2ed82-394">How to configure Virtual Network support for a Premium Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="2ed82-394">How to configure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="2ed82-395">See the [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span><span class="sxs-lookup"><span data-stu-id="2ed82-395">See the [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

<!-- IMAGES -->
[cache-starter-application]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-status-message.png
[deploybutton]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-web-app-howto/cache-delete-confirm.png





























