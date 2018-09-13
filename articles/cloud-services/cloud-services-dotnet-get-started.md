---
title: Get started with Azure Cloud Services and ASP.NET | Microsoft Docs
description: Learn how to create a multi-tier app using ASP.NET MVC and Azure. The app runs in a cloud service, with web role and worker role. It uses Entity Framework, SQL Database, and Azure Storage queues and blobs.
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: ''
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 11/16/2016
ms.author: adegeo
ms.openlocfilehash: 67b09859e79339d0773eb214432fb6d47cf74b31
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553242"
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="4f5ba-105">Get started with Azure Cloud Services and ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4f5ba-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="4f5ba-106">Overview</span><span class="sxs-lookup"><span data-stu-id="4f5ba-106">Overview</span></span>
<span data-ttu-id="4f5ba-107">This tutorial shows how to create a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it to an [Azure cloud service](cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-107">This tutorial shows how to create a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it to an [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="4f5ba-108">The application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), the [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and the [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-108">The application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), the [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and the [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="4f5ba-109">You can [download the Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from the MSDN Code Gallery.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-109">You can [download the Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from the MSDN Code Gallery.</span></span>

<span data-ttu-id="4f5ba-110">The tutorial shows you how to build and run the application locally, how to deploy it to Azure and run in the cloud, and finally how to build it from scratch.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-110">The tutorial shows you how to build and run the application locally, how to deploy it to Azure and run in the cloud, and finally how to build it from scratch.</span></span> <span data-ttu-id="4f5ba-111">You can start by building from scratch and then do the test and deploy steps afterward if you prefer.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-111">You can start by building from scratch and then do the test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="4f5ba-112">Contoso Ads application</span><span class="sxs-lookup"><span data-stu-id="4f5ba-112">Contoso Ads application</span></span>
<span data-ttu-id="4f5ba-113">The application is an advertising bulletin board.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-113">The application is an advertising bulletin board.</span></span> <span data-ttu-id="4f5ba-114">Users create an ad by entering text and uploading an image.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="4f5ba-115">They can see a list of ads with thumbnail images, and they can see the full size image when they select an ad to see the details.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-115">They can see a list of ads with thumbnail images, and they can see the full size image when they select an ad to see the details.</span></span>

![Ad list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="4f5ba-117">The application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a back-end process.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-117">The application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="4f5ba-118">Alternative architecture: Websites and WebJobs</span><span class="sxs-lookup"><span data-stu-id="4f5ba-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="4f5ba-119">This tutorial shows how to run both front-end and back-end in an Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-119">This tutorial shows how to run both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="4f5ba-120">An alternative is to run the front-end in an [Azure website](/services/web-sites/) and use the [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for the back-end.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-120">An alternative is to run the front-end in an [Azure website](/services/web-sites/) and use the [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for the back-end.</span></span> <span data-ttu-id="4f5ba-121">For a tutorial that uses WebJobs, see [Get Started with the Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-121">For a tutorial that uses WebJobs, see [Get Started with the Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="4f5ba-122">For information about how to choose the services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-122">For information about how to choose the services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="4f5ba-123">What you'll learn</span><span class="sxs-lookup"><span data-stu-id="4f5ba-123">What you'll learn</span></span>
* <span data-ttu-id="4f5ba-124">How to enable your machine for Azure development by installing the Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-124">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="4f5ba-125">How to create a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-125">How to create a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="4f5ba-126">How to test the cloud service project locally, using the Azure storage emulator.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-126">How to test the cloud service project locally, using the Azure storage emulator.</span></span>
* <span data-ttu-id="4f5ba-127">How to publish the cloud project to an Azure cloud service and test using an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-127">How to publish the cloud project to an Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="4f5ba-128">How to upload files and store them in the Azure Blob service.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-128">How to upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="4f5ba-129">How to use the Azure Queue service for communication between tiers.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-129">How to use the Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f5ba-130">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4f5ba-130">Prerequisites</span></span>
<span data-ttu-id="4f5ba-131">The tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-131">The tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="4f5ba-132">It also assumes that you know how to work with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-132">It also assumes that you know how to work with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="4f5ba-133">The sample application uses MVC, but most of the tutorial also applies to Web Forms.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-133">The sample application uses MVC, but most of the tutorial also applies to Web Forms.</span></span>

<span data-ttu-id="4f5ba-134">You can run the app locally without an Azure subscription, but you'll need one in order to deploy the application to the cloud.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-134">You can run the app locally without an Azure subscription, but you'll need one in order to deploy the application to the cloud.</span></span> <span data-ttu-id="4f5ba-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="4f5ba-136">The tutorial instructions work with either of the following products:</span><span class="sxs-lookup"><span data-stu-id="4f5ba-136">The tutorial instructions work with either of the following products:</span></span>

* <span data-ttu-id="4f5ba-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="4f5ba-137">Visual Studio 2013</span></span>
* <span data-ttu-id="4f5ba-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="4f5ba-138">Visual Studio 2015</span></span>
* <span data-ttu-id="4f5ba-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4f5ba-139">Visual Studio 2017</span></span>

<span data-ttu-id="4f5ba-140">If you don't have one of these, Visual Studio may be installed automatically when you install the Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-140">If you don't have one of these, Visual Studio may be installed automatically when you install the Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="4f5ba-141">Application architecture</span><span class="sxs-lookup"><span data-stu-id="4f5ba-141">Application architecture</span></span>
<span data-ttu-id="4f5ba-142">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-142">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="4f5ba-143">For each ad the database stores two URLs, one for the full-size image and one for the thumbnail.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-143">For each ad the database stores two URLs, one for the full-size image and one for the thumbnail.</span></span>

![Ad table](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="4f5ba-145">When a user uploads an image, the front-end running in a web role stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-145">When a user uploads an image, the front-end running in a web role stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="4f5ba-146">At the same time, it writes a message to an Azure queue.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-146">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="4f5ba-147">A back-end process running in a worker role periodically polls the queue for new messages.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-147">A back-end process running in a worker role periodically polls the queue for new messages.</span></span> <span data-ttu-id="4f5ba-148">When a new message appears, the worker role creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-148">When a new message appears, the worker role creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="4f5ba-149">The following diagram shows how the parts of the application interact.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-149">The following diagram shows how the parts of the application interact.</span></span>

![Contoso Ads architecture](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2015-2013.md)]

## <a name="download-and-run-the-completed-solution"></a><span data-ttu-id="4f5ba-151">Download and run the completed solution</span><span class="sxs-lookup"><span data-stu-id="4f5ba-151">Download and run the completed solution</span></span>
1. <span data-ttu-id="4f5ba-152">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-152">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="4f5ba-153">Start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="4f5ba-154">From the **File** menu choose **Open Project**, navigate to where you downloaded the solution, and then open the solution file.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-154">From the **File** menu choose **Open Project**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="4f5ba-155">Press CTRL+SHIFT+B to build the solution.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-155">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="4f5ba-156">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-156">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="4f5ba-157">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog box and clicking the **Restore** button at the top right.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-157">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog box and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="4f5ba-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as the startup project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as the startup project.</span></span>
6. <span data-ttu-id="4f5ba-159">If you're using Visual Studio 2015 or higher, change the SQL Server connection string in the application *Web.config* file of the ContosoAdsWeb project and in the *ServiceConfiguration.Local.cscfg* file of the ContosoAdsCloudService project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-159">If you're using Visual Studio 2015 or higher, change the SQL Server connection string in the application *Web.config* file of the ContosoAdsWeb project and in the *ServiceConfiguration.Local.cscfg* file of the ContosoAdsCloudService project.</span></span> <span data-ttu-id="4f5ba-160">In each case, change "(localdb)\v11.0" to "(localdb)\MSSQLLocalDB".</span><span class="sxs-lookup"><span data-stu-id="4f5ba-160">In each case, change "(localdb)\v11.0" to "(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="4f5ba-161">Press CTRL+F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-161">Press CTRL+F5 to run the application.</span></span>

    <span data-ttu-id="4f5ba-162">When you run a cloud service project locally, Visual Studio automatically invokes the Azure *compute emulator* and Azure *storage emulator*.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-162">When you run a cloud service project locally, Visual Studio automatically invokes the Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="4f5ba-163">The compute emulator uses your computer's resources to simulate the web role and worker role environments.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-163">The compute emulator uses your computer's resources to simulate the web role and worker role environments.</span></span> <span data-ttu-id="4f5ba-164">The storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database to simulate Azure cloud storage.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-164">The storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database to simulate Azure cloud storage.</span></span>

    <span data-ttu-id="4f5ba-165">The first time you run a cloud service project, it takes a minute or so for the emulators to start up.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-165">The first time you run a cloud service project, it takes a minute or so for the emulators to start up.</span></span> <span data-ttu-id="4f5ba-166">When emulator startup is finished, the default browser opens to the application home page.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-166">When emulator startup is finished, the default browser opens to the application home page.</span></span>

    ![Contoso Ads architecture](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="4f5ba-168">Click  **Create an Ad**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="4f5ba-169">Enter some test data and select a *.jpg* image to upload, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-169">Enter some test data and select a *.jpg* image to upload, and then click **Create**.</span></span>

    ![Create page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="4f5ba-171">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-171">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="4f5ba-172">Wait a moment and then refresh the Index page to see the thumbnail.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-172">Wait a moment and then refresh the Index page to see the thumbnail.</span></span>

     ![Index page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="4f5ba-174">Click **Details** for your ad to see the full-size image.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-174">Click **Details** for your ad to see the full-size image.</span></span>

     ![Details page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="4f5ba-176">You've been running the application entirely on your local computer, with no connection to the cloud.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-176">You've been running the application entirely on your local computer, with no connection to the cloud.</span></span> <span data-ttu-id="4f5ba-177">The storage emulator stores the queue and blob data in a SQL Server Express LocalDB database, and the application stores the ad data in another LocalDB database.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-177">The storage emulator stores the queue and blob data in a SQL Server Express LocalDB database, and the application stores the ad data in another LocalDB database.</span></span> <span data-ttu-id="4f5ba-178">Entity Framework Code First automatically created the ad database the first time the web app tried to access it.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-178">Entity Framework Code First automatically created the ad database the first time the web app tried to access it.</span></span>

<span data-ttu-id="4f5ba-179">In the following section you'll configure the solution to use Azure cloud resources for queues, blobs, and the application database when it runs in the cloud.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-179">In the following section you'll configure the solution to use Azure cloud resources for queues, blobs, and the application database when it runs in the cloud.</span></span> <span data-ttu-id="4f5ba-180">If you wanted to continue to run locally but use cloud storage and database resources, you could do that; it's just a matter of setting connection strings, which you'll see how to do.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-180">If you wanted to continue to run locally but use cloud storage and database resources, you could do that; it's just a matter of setting connection strings, which you'll see how to do.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="4f5ba-181">Deploy the application to Azure</span><span class="sxs-lookup"><span data-stu-id="4f5ba-181">Deploy the application to Azure</span></span>
<span data-ttu-id="4f5ba-182">You'll do the following steps to run the application in the cloud:</span><span class="sxs-lookup"><span data-stu-id="4f5ba-182">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="4f5ba-183">Create an Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-183">Create an Azure cloud service.</span></span>
* <span data-ttu-id="4f5ba-184">Create an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-184">Create an Azure SQL database.</span></span>
* <span data-ttu-id="4f5ba-185">Create an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-185">Create an Azure storage account.</span></span>
* <span data-ttu-id="4f5ba-186">Configure the solution to use your Azure SQL database when it runs in Azure.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-186">Configure the solution to use your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="4f5ba-187">Configure the solution to use your Azure storage account when it runs in Azure.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-187">Configure the solution to use your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="4f5ba-188">Deploy the project to your Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-188">Deploy the project to your Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="4f5ba-189">Create an Azure cloud service</span><span class="sxs-lookup"><span data-stu-id="4f5ba-189">Create an Azure cloud service</span></span>
<span data-ttu-id="4f5ba-190">An Azure cloud service is the environment the application will run in.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-190">An Azure cloud service is the environment the application will run in.</span></span>

1. <span data-ttu-id="4f5ba-191">In your browser, open the [Azure classic portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-191">In your browser, open the [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4f5ba-192">Click **New > Compute > Cloud Service > Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-192">Click **New > Compute > Cloud Service > Quick Create**.</span></span>
3. <span data-ttu-id="4f5ba-193">In the URL input box, enter a URL prefix.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-193">In the URL input box, enter a URL prefix.</span></span>

    <span data-ttu-id="4f5ba-194">This URL has to be unique.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-194">This URL has to be unique.</span></span>  <span data-ttu-id="4f5ba-195">You'll get an error message if the prefix you choose is already in use by someone else.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-195">You'll get an error message if the prefix you choose is already in use by someone else.</span></span>
4. <span data-ttu-id="4f5ba-196">Choose the region where you want to deploy the application.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-196">Choose the region where you want to deploy the application.</span></span>

    <span data-ttu-id="4f5ba-197">This field specifies which datacenter your cloud service will be hosted in.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-197">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="4f5ba-198">For a production application, you'd choose the region closest to your customers.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-198">For a production application, you'd choose the region closest to your customers.</span></span> <span data-ttu-id="4f5ba-199">For this tutorial, choose the region closest to you.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-199">For this tutorial, choose the region closest to you.</span></span>
5. <span data-ttu-id="4f5ba-200">Click **Create Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-200">Click **Create Cloud Service**.</span></span>

    <span data-ttu-id="4f5ba-201">In the following image, a cloud service is created with the URL contosoads.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-201">In the following image, a cloud service is created with the URL contosoads.cloudapp.net.</span></span>

    ![New Cloud Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="4f5ba-203">Create an Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="4f5ba-203">Create an Azure SQL database</span></span>
<span data-ttu-id="4f5ba-204">When the app runs in the cloud, it will use a cloud-based database.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-204">When the app runs in the cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="4f5ba-205">In the [Azure classic portal](http://manage.windowsazure.com), click **New > Data Services > SQL Database > Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-205">In the [Azure classic portal](http://manage.windowsazure.com), click **New > Data Services > SQL Database > Quick Create**.</span></span>
2. <span data-ttu-id="4f5ba-206">In the **Database Name** box, enter *contosoads*.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-206">In the **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="4f5ba-207">From the **Server** drop-down list, choose **New SQL Database server**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-207">From the **Server** drop-down list, choose **New SQL Database server**.</span></span>

    <span data-ttu-id="4f5ba-208">Alternatively, if your subscription already has a server, you can select that server from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-208">Alternatively, if your subscription already has a server, you can select that server from the drop-down list.</span></span>
4. <span data-ttu-id="4f5ba-209">Choose the same **Region** that you chose for the cloud service.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-209">Choose the same **Region** that you chose for the cloud service.</span></span>

    <span data-ttu-id="4f5ba-210">When the cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-210">When the cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span></span> <span data-ttu-id="4f5ba-211">Bandwidth within a data center is free.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-211">Bandwidth within a data center is free.</span></span>
5. <span data-ttu-id="4f5ba-212">Enter an administrator **Login Name** and **Password**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-212">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="4f5ba-213">If you selected **New SQL Database server** you aren't entering an existing name and password here, you're entering a new name and password that you're defining now to use later when you access the database.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-213">If you selected **New SQL Database server** you aren't entering an existing name and password here, you're entering a new name and password that you're defining now to use later when you access the database.</span></span> <span data-ttu-id="4f5ba-214">If you selected a server that you created previously, you'll be prompted for the password to the administrative user account you already created.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-214">If you selected a server that you created previously, you'll be prompted for the password to the administrative user account you already created.</span></span>
6. <span data-ttu-id="4f5ba-215">Click **Create SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-215">Click **Create SQL Database**.</span></span>

    ![New SQL Database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/newdb.png)
7. <span data-ttu-id="4f5ba-217">After Azure finishes creating the database, click the **SQL Databases** tab in the left pane of the portal, and then click the name of the new database.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-217">After Azure finishes creating the database, click the **SQL Databases** tab in the left pane of the portal, and then click the name of the new database.</span></span>
8. <span data-ttu-id="4f5ba-218">Click the **Dashboard** tab.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-218">Click the **Dashboard** tab.</span></span>
9. <span data-ttu-id="4f5ba-219">Click **Manage allowed IP addresses**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-219">Click **Manage allowed IP addresses**.</span></span>
10. <span data-ttu-id="4f5ba-220">Under **Allowed Services**, change **Azure Services** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-220">Under **Allowed Services**, change **Azure Services** to **Yes**.</span></span>
11. <span data-ttu-id="4f5ba-221">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-221">Click **Save**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="4f5ba-222">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="4f5ba-222">Create an Azure storage account</span></span>
<span data-ttu-id="4f5ba-223">An Azure storage account provides resources for storing queue and blob data in the cloud.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-223">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span>

<span data-ttu-id="4f5ba-224">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-224">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="4f5ba-225">For this tutorial you'll use just one account.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-225">For this tutorial you'll use just one account.</span></span>

1. <span data-ttu-id="4f5ba-226">In the [Azure classic portal](http://manage.windowsazure.com), click **New > Data Services > Storage > Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-226">In the [Azure classic portal](http://manage.windowsazure.com), click **New > Data Services > Storage > Quick Create**.</span></span>
2. <span data-ttu-id="4f5ba-227">In the **URL** box, enter a URL prefix.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-227">In the **URL** box, enter a URL prefix.</span></span>

    <span data-ttu-id="4f5ba-228">This prefix plus the text you see under the box will be the unique URL to your storage account.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-228">This prefix plus the text you see under the box will be the unique URL to your storage account.</span></span> <span data-ttu-id="4f5ba-229">If the prefix you enter has already been used by someone else, you'll have to choose a different prefix.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-229">If the prefix you enter has already been used by someone else, you'll have to choose a different prefix.</span></span>
3. <span data-ttu-id="4f5ba-230">Set the **Region** drop-down list to the same region you chose for the cloud service.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-230">Set the **Region** drop-down list to the same region you chose for the cloud service.</span></span>

    <span data-ttu-id="4f5ba-231">When the cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-231">When the cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span></span> <span data-ttu-id="4f5ba-232">Bandwidth within a data center is free.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-232">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="4f5ba-233">Azure affinity groups provide a mechanism to minimize the distance between resources in a data center, which can reduce latency.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-233">Azure affinity groups provide a mechanism to minimize the distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="4f5ba-234">This tutorial does not use affinity groups.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-234">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="4f5ba-235">For more information, see [How to Create an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-235">For more information, see [How to Create an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
4. <span data-ttu-id="4f5ba-236">Set the **Replication** drop-down list to **Locally redundant**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-236">Set the **Replication** drop-down list to **Locally redundant**.</span></span>

    <span data-ttu-id="4f5ba-237">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-237">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span></span> <span data-ttu-id="4f5ba-238">Geo-replication can incur additional costs.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-238">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="4f5ba-239">For test and development accounts, you generally don't want to pay for geo-replication.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-239">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="4f5ba-240">For more information, see [Create, manage, or delete a storage account](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-240">For more information, see [Create, manage, or delete a storage account](../storage/storage-create-storage-account.md).</span></span>
5. <span data-ttu-id="4f5ba-241">Click **Create Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-241">Click **Create Storage Account**.</span></span>

    ![New storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="4f5ba-243">In the image, a storage account is created with the URL `contosoads.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-243">In the image, a storage account is created with the URL `contosoads.core.windows.net`.</span></span>

### <a name="configure-the-solution-to-use-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="4f5ba-244">Configure the solution to use your Azure SQL database when it runs in Azure</span><span class="sxs-lookup"><span data-stu-id="4f5ba-244">Configure the solution to use your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="4f5ba-245">The web project and the worker role project each has its own database connection string, and each needs to point to the Azure SQL database when the app runs in Azure.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-245">The web project and the worker role project each has its own database connection string, and each needs to point to the Azure SQL database when the app runs in Azure.</span></span>

<span data-ttu-id="4f5ba-246">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for the web role and a cloud service environment setting for the worker role.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-246">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for the web role and a cloud service environment setting for the worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="4f5ba-247">In this section and the next section you store credentials in project files.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-247">In this section and the next section you store credentials in project files.</span></span> <span data-ttu-id="4f5ba-248">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-248">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="4f5ba-249">In the ContosoAdsWeb project, open the *Web.Release.config* transform file for the application *Web.config* file, delete the comment block that contains a `<connectionStrings>` element, and paste the following code in its place.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-249">In the ContosoAdsWeb project, open the *Web.Release.config* transform file for the application *Web.config* file, delete the comment block that contains a `<connectionStrings>` element, and paste the following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="4f5ba-250">Leave the file open for editing.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-250">Leave the file open for editing.</span></span>
2. <span data-ttu-id="4f5ba-251">In the [Azure classic portal](http://manage.windowsazure.com), click **SQL Databases** in the left pane, click the database you created for this tutorial, click the **Dashboard** tab, and then click **Show connection strings**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-251">In the [Azure classic portal](http://manage.windowsazure.com), click **SQL Databases** in the left pane, click the database you created for this tutorial, click the **Dashboard** tab, and then click **Show connection strings**.</span></span>

    ![Show connection strings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="4f5ba-253">The portal displays connection strings, with a placeholder for the password.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-253">The portal displays connection strings, with a placeholder for the password.</span></span>

    ![Connection strings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="4f5ba-255">In the *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place the ADO.NET connection string from the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-255">In the *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place the ADO.NET connection string from the Azure classic portal.</span></span>
4. <span data-ttu-id="4f5ba-256">In the connection string that you pasted into the *Web.Release.config* transform file, replace `{your_password_here}` with the password you created for the new SQL database.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-256">In the connection string that you pasted into the *Web.Release.config* transform file, replace `{your_password_here}` with the password you created for the new SQL database.</span></span>
5. <span data-ttu-id="4f5ba-257">Save the file.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-257">Save the file.</span></span>  
6. <span data-ttu-id="4f5ba-258">Select and copy the connection string (without the surrounding quotation marks) for use in the following steps for configuring the worker role project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-258">Select and copy the connection string (without the surrounding quotation marks) for use in the following steps for configuring the worker role project.</span></span>
7. <span data-ttu-id="4f5ba-259">In **Solution Explorer**, under **Roles** in the cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-259">In **Solution Explorer**, under **Roles** in the cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Role properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="4f5ba-261">Click the **Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-261">Click the **Settings** tab.</span></span>
9. <span data-ttu-id="4f5ba-262">Change **Service Configuration** to **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-262">Change **Service Configuration** to **Cloud**.</span></span>
10. <span data-ttu-id="4f5ba-263">Select the **Value** field for the `ContosoAdsDbConnectionString` setting, and then paste the connection string that you copied from the previous section of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-263">Select the **Value** field for the `ContosoAdsDbConnectionString` setting, and then paste the connection string that you copied from the previous section of the tutorial.</span></span>

     ![Database connection string for worker role](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="4f5ba-265">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-265">Save your changes.</span></span>  

### <a name="configure-the-solution-to-use-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="4f5ba-266">Configure the solution to use your Azure storage account when it runs in Azure</span><span class="sxs-lookup"><span data-stu-id="4f5ba-266">Configure the solution to use your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="4f5ba-267">Azure storage account connection strings for both the web role project and the worker role project are stored in environment settings in the cloud service project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-267">Azure storage account connection strings for both the web role project and the worker role project are stored in environment settings in the cloud service project.</span></span> <span data-ttu-id="4f5ba-268">For each project there is a separate set of settings to be used when the application runs locally and when it runs in the cloud.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-268">For each project there is a separate set of settings to be used when the application runs locally and when it runs in the cloud.</span></span> <span data-ttu-id="4f5ba-269">You'll update the cloud environment settings for both web and worker role projects.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-269">You'll update the cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="4f5ba-270">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in the **ContosoAdsCloudService** project, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-270">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in the **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Role properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="4f5ba-272">Click the **Settings** tab. In the **Service Configuration** drop-down box, choose **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-272">Click the **Settings** tab. In the **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Cloud configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="4f5ba-274">Select the **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at the right end of the line.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-274">Select the **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at the right end of the line.</span></span> <span data-ttu-id="4f5ba-275">Click the ellipsis button to open the **Create Storage Account Connection String** dialog box.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-275">Click the ellipsis button to open the **Create Storage Account Connection String** dialog box.</span></span>

    ![Open Connection String Create box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="4f5ba-277">In the **Create Storage Connection String** dialog box, click **Your subscription**, choose the storage account that you created earlier, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-277">In the **Create Storage Connection String** dialog box, click **Your subscription**, choose the storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="4f5ba-278">If you're not already logged in, you'll be prompted for your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-278">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Create Storage Connection String](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="4f5ba-280">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-280">Save your changes.</span></span>
6. <span data-ttu-id="4f5ba-281">Follow the same procedure that you used for the `StorageConnectionString` connection string to set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-281">Follow the same procedure that you used for the `StorageConnectionString` connection string to set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="4f5ba-282">This connection string is used for logging.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-282">This connection string is used for logging.</span></span>
7. <span data-ttu-id="4f5ba-283">Follow the same procedure that you used for the **ContosoAdsWeb** role to set both connection strings for the **ContosoAdsWorker** role.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-283">Follow the same procedure that you used for the **ContosoAdsWeb** role to set both connection strings for the **ContosoAdsWorker** role.</span></span> <span data-ttu-id="4f5ba-284">Don't forget to set **Service Configuration** to **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-284">Don't forget to set **Service Configuration** to **Cloud**.</span></span>

<span data-ttu-id="4f5ba-285">The role environment settings that you have configured using the Visual Studio UI are stored in the following files in the ContosoAdsCloudService project:</span><span class="sxs-lookup"><span data-stu-id="4f5ba-285">The role environment settings that you have configured using the Visual Studio UI are stored in the following files in the ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="4f5ba-286">*ServiceDefinition.csdef* - Defines the setting names.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-286">*ServiceDefinition.csdef* - Defines the setting names.</span></span>
* <span data-ttu-id="4f5ba-287">*ServiceConfiguration.Cloud.cscfg* - Provides values for when the app runs in the cloud.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-287">*ServiceConfiguration.Cloud.cscfg* - Provides values for when the app runs in the cloud.</span></span>
* <span data-ttu-id="4f5ba-288">*ServiceConfiguration.Local.cscfg* - Provides values for when the app runs locally.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-288">*ServiceConfiguration.Local.cscfg* - Provides values for when the app runs locally.</span></span>

<span data-ttu-id="4f5ba-289">For example, the ServiceDefinition.csdef includes the following definitions.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-289">For example, the ServiceDefinition.csdef includes the following definitions.</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="4f5ba-290">And the *ServiceConfiguration.Cloud.cscfg* file includes the values you entered for those settings in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-290">And the *ServiceConfiguration.Cloud.cscfg* file includes the values you entered for those settings in Visual Studio.</span></span>

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

<span data-ttu-id="4f5ba-291">The `<Instances>` setting specifies the number of virtual machines that Azure will run the worker role code on.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-291">The `<Instances>` setting specifies the number of virtual machines that Azure will run the worker role code on.</span></span> <span data-ttu-id="4f5ba-292">The [Next steps](#next-steps) section includes links to more information about scaling out a cloud service,</span><span class="sxs-lookup"><span data-stu-id="4f5ba-292">The [Next steps](#next-steps) section includes links to more information about scaling out a cloud service,</span></span>

### <a name="deploy-the-project-to-azure"></a><span data-ttu-id="4f5ba-293">Deploy the project to Azure</span><span class="sxs-lookup"><span data-stu-id="4f5ba-293">Deploy the project to Azure</span></span>
1. <span data-ttu-id="4f5ba-294">In **Solution Explorer**, right-click the **ContosoAdsCloudService** cloud project and then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-294">In **Solution Explorer**, right-click the **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Publish menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="4f5ba-296">In the **Sign in** step of the **Publish Azure Application** wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-296">In the **Sign in** step of the **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Sign in step](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="4f5ba-298">In the **Settings** step of the wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-298">In the **Settings** step of the wizard, click **Next**.</span></span>

    ![Settings step](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="4f5ba-300">The default settings in the **Advanced** tab are fine for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-300">The default settings in the **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="4f5ba-301">For information about the advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-301">For information about the advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="4f5ba-302">In the **Summary** step, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-302">In the **Summary** step, click **Publish**.</span></span>

    ![Summary step](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="4f5ba-304">The **Azure Activity Log** window opens in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-304">The **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="4f5ba-305">Click the right arrow icon to expand the deployment details.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-305">Click the right arrow icon to expand the deployment details.</span></span>

    <span data-ttu-id="4f5ba-306">The deployment can take up to 5 minutes or more to complete.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-306">The deployment can take up to 5 minutes or more to complete.</span></span>

    ![Azure Activity Log window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="4f5ba-308">When the deployment status is complete, click the **Web app URL** to start the application.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-308">When the deployment status is complete, click the **Web app URL** to start the application.</span></span>
7. <span data-ttu-id="4f5ba-309">You can now test the app by creating, viewing, and editing some ads, as you did when you ran the application locally.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-309">You can now test the app by creating, viewing, and editing some ads, as you did when you ran the application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="4f5ba-310">When you're finished testing, delete or stop the cloud service.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-310">When you're finished testing, delete or stop the cloud service.</span></span> <span data-ttu-id="4f5ba-311">Even if you're not using the cloud service, it's accruing charges because virtual machine resources are reserved for it.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-311">Even if you're not using the cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="4f5ba-312">And if you leave it running, anyone who finds your URL can create and view ads.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-312">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="4f5ba-313">In the [Azure classic portal](http://manage.windowsazure.com), go to the **Dashboard** tab for your cloud service, and then click the **Delete** button at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-313">In the [Azure classic portal](http://manage.windowsazure.com), go to the **Dashboard** tab for your cloud service, and then click the **Delete** button at the bottom of the page.</span></span> <span data-ttu-id="4f5ba-314">If you just want to temporarily prevent others from accessing the site, click **Stop** instead.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-314">If you just want to temporarily prevent others from accessing the site, click **Stop** instead.</span></span> <span data-ttu-id="4f5ba-315">In that case, charges will continue to accrue.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-315">In that case, charges will continue to accrue.</span></span> <span data-ttu-id="4f5ba-316">You can follow a similar procedure to delete the SQL database and storage account when you no longer need them.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-316">You can follow a similar procedure to delete the SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-the-application-from-scratch"></a><span data-ttu-id="4f5ba-317">Create the application from scratch</span><span class="sxs-lookup"><span data-stu-id="4f5ba-317">Create the application from scratch</span></span>
<span data-ttu-id="4f5ba-318">If you haven't already downloaded [the completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-318">If you haven't already downloaded [the completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="4f5ba-319">You'll copy files from the downloaded project into the new project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-319">You'll copy files from the downloaded project into the new project.</span></span>

<span data-ttu-id="4f5ba-320">Creating the Contoso Ads application involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="4f5ba-320">Creating the Contoso Ads application involves the following steps:</span></span>

* <span data-ttu-id="4f5ba-321">Create a cloud service Visual Studio solution.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-321">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="4f5ba-322">Update and add NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-322">Update and add NuGet packages.</span></span>
* <span data-ttu-id="4f5ba-323">Set project references.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-323">Set project references.</span></span>
* <span data-ttu-id="4f5ba-324">Configure connection strings.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-324">Configure connection strings.</span></span>
* <span data-ttu-id="4f5ba-325">Add code files.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-325">Add code files.</span></span>

<span data-ttu-id="4f5ba-326">After the solution is created, you'll review the code that is unique to cloud service projects and Azure blobs and queues.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-326">After the solution is created, you'll review the code that is unique to cloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="4f5ba-327">Create a cloud service Visual Studio solution</span><span class="sxs-lookup"><span data-stu-id="4f5ba-327">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="4f5ba-328">In Visual Studio, choose **New Project** from the **File** menu.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-328">In Visual Studio, choose **New Project** from the **File** menu.</span></span>
2. <span data-ttu-id="4f5ba-329">In the left pane of the **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose the **Azure Cloud Service** template.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-329">In the left pane of the **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose the **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="4f5ba-330">Name the project and solution ContosoAdsCloudService, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-330">Name the project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![New Project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="4f5ba-332">In the **New Azure Cloud Service** dialog box, add a web role and a worker role.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-332">In the **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="4f5ba-333">Name the web role ContosoAdsWeb, and name the worker role ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-333">Name the web role ContosoAdsWeb, and name the worker role ContosoAdsWorker.</span></span> <span data-ttu-id="4f5ba-334">(Use the pencil icon in the right-hand pane to change the default names of the roles.)</span><span class="sxs-lookup"><span data-stu-id="4f5ba-334">(Use the pencil icon in the right-hand pane to change the default names of the roles.)</span></span>

    ![New Cloud Service Project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="4f5ba-336">When you see the **New ASP.NET Project** dialog box for the web role, choose the MVC template, and then click **Change Authentication**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-336">When you see the **New ASP.NET Project** dialog box for the web role, choose the MVC template, and then click **Change Authentication**.</span></span>

    ![Change Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="4f5ba-338">In the **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-338">In the **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![No Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="4f5ba-340">In the **New ASP.NET Project** dialog, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-340">In the **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="4f5ba-341">In **Solution Explorer**, right-click the solution (not one of the projects), and choose **Add - New Project**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-341">In **Solution Explorer**, right-click the solution (not one of the projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="4f5ba-342">In the **Add New Project** dialog box, choose **Windows** under **Visual C#** in the left pane, and then click the **Class Library** template.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-342">In the **Add New Project** dialog box, choose **Windows** under **Visual C#** in the left pane, and then click the **Class Library** template.</span></span>  
10. <span data-ttu-id="4f5ba-343">Name the project *ContosoAdsCommon*, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-343">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="4f5ba-344">You need to reference the Entity Framework context and the data model from both web and worker role projects.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-344">You need to reference the Entity Framework context and the data model from both web and worker role projects.</span></span> <span data-ttu-id="4f5ba-345">As an alternative you could define the EF-related classes in the web role project and reference that project from the worker role project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-345">As an alternative you could define the EF-related classes in the web role project and reference that project from the worker role project.</span></span> <span data-ttu-id="4f5ba-346">But in the alternative approach, your worker role project would have a reference to web assemblies which it doesn't need.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-346">But in the alternative approach, your worker role project would have a reference to web assemblies which it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="4f5ba-347">Update and add NuGet packages</span><span class="sxs-lookup"><span data-stu-id="4f5ba-347">Update and add NuGet packages</span></span>
1. <span data-ttu-id="4f5ba-348">Open the **Manage NuGet Packages** dialog box for the solution.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-348">Open the **Manage NuGet Packages** dialog box for the solution.</span></span>
2. <span data-ttu-id="4f5ba-349">At the top of the window, select **Updates**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-349">At the top of the window, select **Updates**.</span></span>
3. <span data-ttu-id="4f5ba-350">Look for the *WindowsAzure.Storage* package, and if it's in the list, select it and select the web and worker projects to update it in, and then click **Update**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-350">Look for the *WindowsAzure.Storage* package, and if it's in the list, select it and select the web and worker projects to update it in, and then click **Update**.</span></span>

    <span data-ttu-id="4f5ba-351">The storage client library is updated more frequently than Visual Studio project templates, so you'll often find that the version in a newly created projected needs to be updated.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-351">The storage client library is updated more frequently than Visual Studio project templates, so you'll often find that the version in a newly created projected needs to be updated.</span></span>
4. <span data-ttu-id="4f5ba-352">At the top of the window, select **Browse**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-352">At the top of the window, select **Browse**.</span></span>
5. <span data-ttu-id="4f5ba-353">Find the *EntityFramework* NuGet package, and install it in all three projects.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-353">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="4f5ba-354">Find the *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in the worker role project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-354">Find the *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in the worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="4f5ba-355">Set project references</span><span class="sxs-lookup"><span data-stu-id="4f5ba-355">Set project references</span></span>
1. <span data-ttu-id="4f5ba-356">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-356">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="4f5ba-357">Right-click the ContosoAdsWeb project, and then click **References** - **Add References**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-357">Right-click the ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="4f5ba-358">In the **Reference Manager** dialog box, select **Solution – Projects** in the left pane, select **ContosoAdsCommon**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-358">In the **Reference Manager** dialog box, select **Solution – Projects** in the left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="4f5ba-359">In the ContosoAdsWorker project, set a reference to the ContosAdsCommon project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-359">In the ContosoAdsWorker project, set a reference to the ContosAdsCommon project.</span></span>

    <span data-ttu-id="4f5ba-360">ContosoAdsCommon will contain the Entity Framework data model and context class, which will be used by both the front-end and back-end.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-360">ContosoAdsCommon will contain the Entity Framework data model and context class, which will be used by both the front-end and back-end.</span></span>
3. <span data-ttu-id="4f5ba-361">In the ContosoAdsWorker project, set a reference to `System.Drawing`.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-361">In the ContosoAdsWorker project, set a reference to `System.Drawing`.</span></span>

    <span data-ttu-id="4f5ba-362">This assembly is used by the back-end to convert images to thumbnails.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-362">This assembly is used by the back-end to convert images to thumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="4f5ba-363">Configure connection strings</span><span class="sxs-lookup"><span data-stu-id="4f5ba-363">Configure connection strings</span></span>
<span data-ttu-id="4f5ba-364">In this section you configure Azure Storage and SQL connection strings for testing locally.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-364">In this section you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="4f5ba-365">The deployment instructions earlier in the tutorial explain how to set up the connection strings for when the app runs in the cloud.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-365">The deployment instructions earlier in the tutorial explain how to set up the connection strings for when the app runs in the cloud.</span></span>

1. <span data-ttu-id="4f5ba-366">In the ContosoAdsWeb project, open the application Web.config file, and insert the following `connectionStrings` element after the `configSections` element.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-366">In the ContosoAdsWeb project, open the application Web.config file, and insert the following `connectionStrings` element after the `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="4f5ba-367">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span><span class="sxs-lookup"><span data-stu-id="4f5ba-367">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="4f5ba-368">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-368">Save your changes.</span></span>
3. <span data-ttu-id="4f5ba-369">In the ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-369">In the ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Role properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="4f5ba-371">In the **ContosAdsWeb [Role]** properties window, click the **Settings** tab, and then click **Add Setting**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-371">In the **ContosAdsWeb [Role]** properties window, click the **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="4f5ba-372">Leave **Service Configuration** set to **All Configurations**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-372">Leave **Service Configuration** set to **All Configurations**.</span></span>
5. <span data-ttu-id="4f5ba-373">Add a new setting named *StorageConnectionString*.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-373">Add a new setting named *StorageConnectionString*.</span></span> <span data-ttu-id="4f5ba-374">Set **Type** to *ConnectionString*, and set **Value** to *UseDevelopmentStorage=true*.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-374">Set **Type** to *ConnectionString*, and set **Value** to *UseDevelopmentStorage=true*.</span></span>

    ![New connection string](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="4f5ba-376">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-376">Save your changes.</span></span>
7. <span data-ttu-id="4f5ba-377">Follow the same procedure to add a storage connection string in the ContosoAdsWorker role properties.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-377">Follow the same procedure to add a storage connection string in the ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="4f5ba-378">Still in the **ContosoAdsWorker [Role]** properties window, add another connection string:</span><span class="sxs-lookup"><span data-stu-id="4f5ba-378">Still in the **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="4f5ba-379">Name: ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="4f5ba-379">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="4f5ba-380">Type: String</span><span class="sxs-lookup"><span data-stu-id="4f5ba-380">Type: String</span></span>
   * <span data-ttu-id="4f5ba-381">Value: Paste the same connection string you used for the web role project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-381">Value: Paste the same connection string you used for the web role project.</span></span> <span data-ttu-id="4f5ba-382">(The following example is for Visual Studio 2013; don't forget to change the Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span><span class="sxs-lookup"><span data-stu-id="4f5ba-382">(The following example is for Visual Studio 2013; don't forget to change the Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="4f5ba-383">Add code files</span><span class="sxs-lookup"><span data-stu-id="4f5ba-383">Add code files</span></span>
<span data-ttu-id="4f5ba-384">In this section you copy code files from the downloaded solution into the new solution.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-384">In this section you copy code files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="4f5ba-385">The following sections will show and explain key parts of this code.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-385">The following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="4f5ba-386">To add files to a project or a folder, right-click the project or folder and click **Add** - **Existing Item**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-386">To add files to a project or a folder, right-click the project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="4f5ba-387">Select the files you want and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-387">Select the files you want and then click **Add**.</span></span> <span data-ttu-id="4f5ba-388">If asked whether you want to replace existing files, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-388">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="4f5ba-389">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the *Ad.cs* and *ContosoAdscontext.cs* files from the downloaded project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-389">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the *Ad.cs* and *ContosoAdscontext.cs* files from the downloaded project.</span></span>
2. <span data-ttu-id="4f5ba-390">In the ContosoAdsWeb project, add the following files from the downloaded project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-390">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="4f5ba-391">*Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-391">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="4f5ba-392">In the *Views\Shared* folder: *\_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-392">In the *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="4f5ba-393">In the *Views\Home* folder: *Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-393">In the *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="4f5ba-394">In the *Controllers* folder: *AdController.cs*.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-394">In the *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="4f5ba-395">In the *Views\Ad* folder (create the folder first): five *.cshtml* files.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-395">In the *Views\Ad* folder (create the folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="4f5ba-396">In the ContosoAdsWorker project, add *WorkerRole.cs* from the downloaded project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-396">In the ContosoAdsWorker project, add *WorkerRole.cs* from the downloaded project.</span></span>

<span data-ttu-id="4f5ba-397">You can now build and run the application as instructed earlier in the tutorial, and the app will use local database and storage emulator resources.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-397">You can now build and run the application as instructed earlier in the tutorial, and the app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="4f5ba-398">The following sections explain the code related to working with the Azure environment, blobs, and queues.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-398">The following sections explain the code related to working with the Azure environment, blobs, and queues.</span></span> <span data-ttu-id="4f5ba-399">This tutorial does not explain how to create MVC controllers and views using scaffolding, how to write Entity Framework code that works with SQL Server databases, or the basics of asynchronous programming in ASP.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-399">This tutorial does not explain how to create MVC controllers and views using scaffolding, how to write Entity Framework code that works with SQL Server databases, or the basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="4f5ba-400">For information about these topics, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="4f5ba-400">For information about these topics, see the following resources:</span></span>

* [<span data-ttu-id="4f5ba-401">Get started with MVC 5</span><span class="sxs-lookup"><span data-stu-id="4f5ba-401">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="4f5ba-402">Get started with EF 6 and MVC 5</span><span class="sxs-lookup"><span data-stu-id="4f5ba-402">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="4f5ba-403">[Introduction to asynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-403">[Introduction to asynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="4f5ba-404">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="4f5ba-404">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="4f5ba-405">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-405">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

```csharp
public enum Category
{
    Cars,
    [Display(Name="Real Estate")]
    RealEstate,
    [Display(Name = "Free Stuff")]
    FreeStuff
}

public class Ad
{
    public int AdId { get; set; }

    [StringLength(100)]
    public string Title { get; set; }

    public int Price { get; set; }

    [StringLength(1000)]
    [DataType(DataType.MultilineText)]
    public string Description { get; set; }

    [StringLength(1000)]
    [DisplayName("Full-size Image")]
    public string ImageURL { get; set; }

    [StringLength(1000)]
    [DisplayName("Thumbnail")]
    public string ThumbnailURL { get; set; }

    [DataType(DataType.Date)]
    [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
    public DateTime PostedDate { get; set; }

    public Category? Category { get; set; }
    [StringLength(12)]
    public string Phone { get; set; }
}
```

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="4f5ba-406">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="4f5ba-406">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="4f5ba-407">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-407">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

```csharp
public class ContosoAdsContext : DbContext
{
    public ContosoAdsContext() : base("name=ContosoAdsContext")
    {
    }
    public ContosoAdsContext(string connString)
        : base(connString)
    {
    }
    public System.Data.Entity.DbSet<Ad> Ads { get; set; }
}
```

<span data-ttu-id="4f5ba-408">The class has two constructors.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-408">The class has two constructors.</span></span> <span data-ttu-id="4f5ba-409">The first of them is used by the web project, and specifies the name of a connection string that is stored in the Web.config file.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-409">The first of them is used by the web project, and specifies the name of a connection string that is stored in the Web.config file.</span></span> <span data-ttu-id="4f5ba-410">The second constructor enables you to pass in the actual connection string.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-410">The second constructor enables you to pass in the actual connection string.</span></span> <span data-ttu-id="4f5ba-411">That is needed by the worker role project, since it doesn't have a Web.config file.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-411">That is needed by the worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="4f5ba-412">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-412">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="4f5ba-413">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="4f5ba-413">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="4f5ba-414">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-414">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="4f5ba-415">This ensures that whenever you start using a new storage account, or start using the storage emulator on a new computer, the required blob container and queue will be created automatically.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-415">This ensures that whenever you start using a new storage account, or start using the storage emulator on a new computer, the required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="4f5ba-416">The code gets access to the storage account by using the storage connection string from the *.cscfg* file.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-416">The code gets access to the storage account by using the storage connection string from the *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="4f5ba-417">Then it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-417">Then it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="4f5ba-418">By default, new containers only allow clients with storage account credentials to access blobs.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-418">By default, new containers only allow clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="4f5ba-419">The website needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-419">The website needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

<span data-ttu-id="4f5ba-420">Similar code gets a reference to the *images* queue and creates a new queue.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-420">Similar code gets a reference to the *images* queue and creates a new queue.</span></span> <span data-ttu-id="4f5ba-421">In this case no permissions change is needed.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-421">In this case no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="4f5ba-422">ContosoAdsWeb - \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="4f5ba-422">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="4f5ba-423">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-423">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="4f5ba-424">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="4f5ba-424">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="4f5ba-425">The *Views\Home\Index.cshtml* file displays category links on the home page.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-425">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="4f5ba-426">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-426">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="4f5ba-427">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="4f5ba-427">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="4f5ba-428">In the *AdController.cs* file the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-428">In the *AdController.cs* file the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="4f5ba-429">Then the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-429">Then the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="4f5ba-430">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-430">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="4f5ba-431">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-431">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="4f5ba-432">The retry policy specified here waits 3 seconds after each try for up to 3 tries.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-432">The retry policy specified here waits 3 seconds after each try for up to 3 tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="4f5ba-433">Similar code gets a reference to the *images* queue.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-433">Similar code gets a reference to the *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="4f5ba-434">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-434">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="4f5ba-435">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-435">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="4f5ba-436">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-436">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="4f5ba-437">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-437">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="4f5ba-438">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-438">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="4f5ba-439">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-439">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

```csharp
private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
{
    string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
    CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
    using (var fileStream = imageFile.InputStream)
    {
        await imageBlob.UploadFromStreamAsync(fileStream);
    }
    return imageBlob;
}
```

<span data-ttu-id="4f5ba-440">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform that back-end process that an image is ready for conversion to a thumbnail.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-440">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform that back-end process that an image is ready for conversion to a thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="4f5ba-441">The code for the HttpPost `Edit` method is similar except that if the user selects a new image file any blobs that already exist must be deleted.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-441">The code for the HttpPost `Edit` method is similar except that if the user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="4f5ba-442">The next example shows the code that deletes blobs when you delete an ad.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-442">The next example shows the code that deletes blobs when you delete an ad.</span></span>

```csharp
private async Task DeleteAdBlobsAsync(Ad ad)
{
    if (!string.IsNullOrWhiteSpace(ad.ImageURL))
    {
        Uri blobUri = new Uri(ad.ImageURL);
        await DeleteAdBlobAsync(blobUri);
    }
    if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
    {
        Uri blobUri = new Uri(ad.ThumbnailURL);
        await DeleteAdBlobAsync(blobUri);
    }
}
private static async Task DeleteAdBlobAsync(Uri blobUri)
{
    string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
    CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
    await blobToDelete.DeleteAsync();
}
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="4f5ba-443">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="4f5ba-443">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="4f5ba-444">The *Index.cshtml* file displays thumbnails with the other ad data.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-444">The *Index.cshtml* file displays thumbnails with the other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="4f5ba-445">The *Details.cshtml* file displays the full-size image.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-445">The *Details.cshtml* file displays the full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="4f5ba-446">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="4f5ba-446">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="4f5ba-447">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-447">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="4f5ba-448">An `<input>` element tells the browser to provide a file selection dialog.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-448">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="4f5ba-449">ContosoAdsWorker - WorkerRole.cs - OnStart method</span><span class="sxs-lookup"><span data-stu-id="4f5ba-449">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="4f5ba-450">The Azure worker role environment calls the `OnStart` method in the `WorkerRole` class when the worker role is getting started, and it calls the `Run` method when the `OnStart` method finishes.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-450">The Azure worker role environment calls the `OnStart` method in the `WorkerRole` class when the worker role is getting started, and it calls the `Run` method when the `OnStart` method finishes.</span></span>

<span data-ttu-id="4f5ba-451">The `OnStart` method gets the database connection string from the *.cscfg* file and passes it to the Entity Framework DbContext class.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-451">The `OnStart` method gets the database connection string from the *.cscfg* file and passes it to the Entity Framework DbContext class.</span></span> <span data-ttu-id="4f5ba-452">The SQLClient provider is used by default, so the provider does not have to be specified.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-452">The SQLClient provider is used by default, so the provider does not have to be specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="4f5ba-453">After that the method gets a reference to the storage account and creates the blob container and queue if they don't exist.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-453">After that the method gets a reference to the storage account and creates the blob container and queue if they don't exist.</span></span> <span data-ttu-id="4f5ba-454">The code for that is similar to what you already saw in the web role `Application_Start` method.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-454">The code for that is similar to what you already saw in the web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="4f5ba-455">ContosoAdsWorker - WorkerRole.cs - Run method</span><span class="sxs-lookup"><span data-stu-id="4f5ba-455">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="4f5ba-456">The `Run` method is called when the `OnStart` method finishes its initialization work.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-456">The `Run` method is called when the `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="4f5ba-457">The method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-457">The method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

<span data-ttu-id="4f5ba-458">After each iteration of the loop, if no queue message was found, the program sleeps for a second.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-458">After each iteration of the loop, if no queue message was found, the program sleeps for a second.</span></span> <span data-ttu-id="4f5ba-459">This prevents the worker role from incurring excessive CPU time and storage transaction costs.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-459">This prevents the worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="4f5ba-460">The Microsoft Customer Advisory Team tells a story about a  developer who forgot to include this, deployed to production, and left for vacation.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-460">The Microsoft Customer Advisory Team tells a story about a  developer who forgot to include this, deployed to production, and left for vacation.</span></span> <span data-ttu-id="4f5ba-461">When he got back, his oversight cost more than the vacation.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-461">When he got back, his oversight cost more than the vacation.</span></span>

<span data-ttu-id="4f5ba-462">Sometimes the content of a queue message causes an error in processing.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-462">Sometimes the content of a queue message causes an error in processing.</span></span> <span data-ttu-id="4f5ba-463">This is called a *poison message*, and if you just logged an error and restarted the loop, you could endlessly try to process that message.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-463">This is called a *poison message*, and if you just logged an error and restarted the loop, you could endlessly try to process that message.</span></span>  <span data-ttu-id="4f5ba-464">Therefore the catch block includes an if statement that checks to see how many times the app has tried to process the current message, and if it has been more than 5 times, the message is deleted from the queue.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-464">Therefore the catch block includes an if statement that checks to see how many times the app has tried to process the current message, and if it has been more than 5 times, the message is deleted from the queue.</span></span>

<span data-ttu-id="4f5ba-465">`ProcessQueueMessage` is called when a queue message is found.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-465">`ProcessQueueMessage` is called when a queue message is found.</span></span>

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

<span data-ttu-id="4f5ba-466">This code reads the database to get the image URL, converts the image to a thumbnail, saves the thumbnail in a blob, updates the database with the thumbnail blob URL, and deletes the queue message.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-466">This code reads the database to get the image URL, converts the image to a thumbnail, saves the thumbnail in a blob, updates the database with the thumbnail blob URL, and deletes the queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="4f5ba-467">The code in the `ConvertImageToThumbnailJPG` method uses classes in the System.Drawing namespace for simplicity.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-467">The code in the `ConvertImageToThumbnailJPG` method uses classes in the System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="4f5ba-468">However, the classes in this namespace were designed for use with Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-468">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="4f5ba-469">They are not supported for use in a Windows or ASP.NET service.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-469">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="4f5ba-470">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-470">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="4f5ba-471">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="4f5ba-471">Troubleshooting</span></span>
<span data-ttu-id="4f5ba-472">In case something doesn't work while you're following the instructions in this tutorial, here are some common errors and how to resolve them.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-472">In case something doesn't work while you're following the instructions in this tutorial, here are some common errors and how to resolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="4f5ba-473">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="4f5ba-473">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="4f5ba-474">The `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using the Azure compute emulator.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-474">The `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using the Azure compute emulator.</span></span>  <span data-ttu-id="4f5ba-475">If you get this error when you're running locally, make sure that you have set the ContosoAdsCloudService project as the startup project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-475">If you get this error when you're running locally, make sure that you have set the ContosoAdsCloudService project as the startup project.</span></span> <span data-ttu-id="4f5ba-476">This sets up the project to run using the Azure compute emulator.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-476">This sets up the project to run using the Azure compute emulator.</span></span>

<span data-ttu-id="4f5ba-477">One of the things the application uses the Azure RoleEnvironment for is to get the connection string values that are stored in the *.cscfg* files, so another cause of this exception is a missing connection string.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-477">One of the things the application uses the Azure RoleEnvironment for is to get the connection string values that are stored in the *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="4f5ba-478">Make sure that you created the StorageConnectionString setting for both Cloud and Local configurations in the ContosoAdsWeb project, and that you created both connection strings for both configurations in the ContosoAdsWorker project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-478">Make sure that you created the StorageConnectionString setting for both Cloud and Local configurations in the ContosoAdsWeb project, and that you created both connection strings for both configurations in the ContosoAdsWorker project.</span></span> <span data-ttu-id="4f5ba-479">If you do a **Find All** search for StorageConnectionString in the entire solution, you should see it 9 times in 6 files.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-479">If you do a **Find All** search for StorageConnectionString in the entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-to-port-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="4f5ba-480">Cannot override to port xxx.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-480">Cannot override to port xxx.</span></span> <span data-ttu-id="4f5ba-481">New port below minimum allowed value 8080 for protocol http</span><span class="sxs-lookup"><span data-stu-id="4f5ba-481">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="4f5ba-482">Try changing the port number used by the web project.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-482">Try changing the port number used by the web project.</span></span> <span data-ttu-id="4f5ba-483">Right-click the ContosoAdsWeb project, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-483">Right-click the ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="4f5ba-484">Click the **Web** tab, and then change the port number in the **Project Url** setting.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-484">Click the **Web** tab, and then change the port number in the **Project Url** setting.</span></span>

<span data-ttu-id="4f5ba-485">For another alternative that might resolve the problem, see the following  section.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-485">For another alternative that might resolve the problem, see the following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="4f5ba-486">Other errors when running locally</span><span class="sxs-lookup"><span data-stu-id="4f5ba-486">Other errors when running locally</span></span>
<span data-ttu-id="4f5ba-487">By default new cloud service projects use the Azure compute emulator express to simulate the Azure environment.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-487">By default new cloud service projects use the Azure compute emulator express to simulate the Azure environment.</span></span> <span data-ttu-id="4f5ba-488">This is a lightweight version of the full compute emulator, and under some conditions the full emulator will work when the express version does not.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-488">This is a lightweight version of the full compute emulator, and under some conditions the full emulator will work when the express version does not.</span></span>  

<span data-ttu-id="4f5ba-489">To change the project to use the full emulator, right-click the ContosoAdsCloudService project, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-489">To change the project to use the full emulator, right-click the ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="4f5ba-490">In the **Properties** window click the **Web** tab, and then click the **Use Full Emulator** radio button.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-490">In the **Properties** window click the **Web** tab, and then click the **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="4f5ba-491">In order to run the application with the full emulator, you have to open Visual Studio with administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-491">In order to run the application with the full emulator, you have to open Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f5ba-492">Next steps</span><span class="sxs-lookup"><span data-stu-id="4f5ba-492">Next steps</span></span>
<span data-ttu-id="4f5ba-493">The Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-493">The Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="4f5ba-494">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors, and so forth.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-494">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors, and so forth.</span></span>

<span data-ttu-id="4f5ba-495">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex to more complex:</span><span class="sxs-lookup"><span data-stu-id="4f5ba-495">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex to more complex:</span></span>

* <span data-ttu-id="4f5ba-496">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-496">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="4f5ba-497">Similar in concept to Contoso Ads but implements more features and more real-world coding practices.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-497">Similar in concept to Contoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="4f5ba-498">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-498">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="4f5ba-499">Introduces Azure Storage tables as well as blobs and queues.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-499">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="4f5ba-500">Based on an older version of the Azure SDK for .NET, will require some modifications to work with the current version.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-500">Based on an older version of the Azure SDK for .NET, will require some modifications to work with the current version.</span></span>
* <span data-ttu-id="4f5ba-501">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-501">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="4f5ba-502">A comprehensive sample demonstrating a wide range of best practices, produced by the Microsoft Patterns and Practices group.</span><span class="sxs-lookup"><span data-stu-id="4f5ba-502">A comprehensive sample demonstrating a wide range of best practices, produced by the Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="4f5ba-503">For general information about developing for the cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-503">For general information about developing for the cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="4f5ba-504">For a video introduction to Azure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span><span class="sxs-lookup"><span data-stu-id="4f5ba-504">For a video introduction to Azure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="4f5ba-505">For more information, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="4f5ba-505">For more information, see the following resources:</span></span>

* [<span data-ttu-id="4f5ba-506">Azure Cloud Services Part 1: Introduction</span><span class="sxs-lookup"><span data-stu-id="4f5ba-506">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="4f5ba-507">How to manage Cloud Services</span><span class="sxs-lookup"><span data-stu-id="4f5ba-507">How to manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="4f5ba-508">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4f5ba-508">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="4f5ba-509">How to choose a cloud service provider</span><span class="sxs-lookup"><span data-stu-id="4f5ba-509">How to choose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)





























