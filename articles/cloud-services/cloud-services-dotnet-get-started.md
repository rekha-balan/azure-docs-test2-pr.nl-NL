---
title: Get started with Azure Cloud Services and ASP.NET | Microsoft Docs
description: Learn how to create a multi-tier app using ASP.NET MVC and Azure. The app runs in a cloud service, with web role and worker role. It uses Entity Framework, SQL Database, and Azure Storage queues and blobs.
services: cloud-services, storage
documentationcenter: .net
author: jpconnock
manager: timlt
editor: ''
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: jeconnoc
ms.openlocfilehash: 819a2f81ca5403a3656bf713cf0ee3ae58050a4b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775248"
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="0307e-105">Get started with Azure Cloud Services and ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0307e-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="0307e-106">Overview</span><span class="sxs-lookup"><span data-stu-id="0307e-106">Overview</span></span>
<span data-ttu-id="0307e-107">This tutorial shows how to create a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it to an [Azure cloud service](cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="0307e-107">This tutorial shows how to create a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it to an [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="0307e-108">The application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), the [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and the [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span><span class="sxs-lookup"><span data-stu-id="0307e-108">The application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), the [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and the [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="0307e-109">You can [download the Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from the MSDN Code Gallery.</span><span class="sxs-lookup"><span data-stu-id="0307e-109">You can [download the Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from the MSDN Code Gallery.</span></span>

<span data-ttu-id="0307e-110">The tutorial shows you how to build and run the application locally, how to deploy it to Azure and run in the cloud, and how to build it from scratch.</span><span class="sxs-lookup"><span data-stu-id="0307e-110">The tutorial shows you how to build and run the application locally, how to deploy it to Azure and run in the cloud, and how to build it from scratch.</span></span> <span data-ttu-id="0307e-111">You can start by building from scratch and then do the test and deploy steps afterward if you prefer.</span><span class="sxs-lookup"><span data-stu-id="0307e-111">You can start by building from scratch and then do the test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="0307e-112">Contoso Ads application</span><span class="sxs-lookup"><span data-stu-id="0307e-112">Contoso Ads application</span></span>
<span data-ttu-id="0307e-113">The application is an advertising bulletin board.</span><span class="sxs-lookup"><span data-stu-id="0307e-113">The application is an advertising bulletin board.</span></span> <span data-ttu-id="0307e-114">Users create an ad by entering text and uploading an image.</span><span class="sxs-lookup"><span data-stu-id="0307e-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="0307e-115">They can see a list of ads with thumbnail images, and they can see the full-size image when they select an ad to see the details.</span><span class="sxs-lookup"><span data-stu-id="0307e-115">They can see a list of ads with thumbnail images, and they can see the full-size image when they select an ad to see the details.</span></span>

![Ad list](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="0307e-117">The application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a back-end process.</span><span class="sxs-lookup"><span data-stu-id="0307e-117">The application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a back-end process.</span></span>

## <a name="alternative-architecture-web-apps-and-webjobs"></a><span data-ttu-id="0307e-118">Alternative architecture: Web Apps and WebJobs</span><span class="sxs-lookup"><span data-stu-id="0307e-118">Alternative architecture: Web Apps and WebJobs</span></span>
<span data-ttu-id="0307e-119">This tutorial shows how to run both front-end and back-end in an Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="0307e-119">This tutorial shows how to run both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="0307e-120">An alternative is to run the front-end in an [Azure Web Apps](/azure/app-service/) and use the [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature for the back-end.</span><span class="sxs-lookup"><span data-stu-id="0307e-120">An alternative is to run the front-end in an [Azure Web Apps](/azure/app-service/) and use the [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature for the back-end.</span></span> <span data-ttu-id="0307e-121">For a tutorial that uses WebJobs, see [Get Started with the Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki).</span><span class="sxs-lookup"><span data-stu-id="0307e-121">For a tutorial that uses WebJobs, see [Get Started with the Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki).</span></span> <span data-ttu-id="0307e-122">For information about how to choose the services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service/choose-web-site-cloud-service-vm.md).</span><span class="sxs-lookup"><span data-stu-id="0307e-122">For information about how to choose the services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="0307e-123">What you'll learn</span><span class="sxs-lookup"><span data-stu-id="0307e-123">What you'll learn</span></span>
* <span data-ttu-id="0307e-124">How to enable your machine for Azure development by installing the Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="0307e-124">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="0307e-125">How to create a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span><span class="sxs-lookup"><span data-stu-id="0307e-125">How to create a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="0307e-126">How to test the cloud service project locally, using the Azure storage emulator.</span><span class="sxs-lookup"><span data-stu-id="0307e-126">How to test the cloud service project locally, using the Azure storage emulator.</span></span>
* <span data-ttu-id="0307e-127">How to publish the cloud project to an Azure cloud service and test using an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="0307e-127">How to publish the cloud project to an Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="0307e-128">How to upload files and store them in the Azure Blob service.</span><span class="sxs-lookup"><span data-stu-id="0307e-128">How to upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="0307e-129">How to use the Azure Queue service for communication between tiers.</span><span class="sxs-lookup"><span data-stu-id="0307e-129">How to use the Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0307e-130">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0307e-130">Prerequisites</span></span>
<span data-ttu-id="0307e-131">The tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span><span class="sxs-lookup"><span data-stu-id="0307e-131">The tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="0307e-132">It also assumes that you know how to work with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0307e-132">It also assumes that you know how to work with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="0307e-133">The sample application uses MVC, but most of the tutorial also applies to Web Forms.</span><span class="sxs-lookup"><span data-stu-id="0307e-133">The sample application uses MVC, but most of the tutorial also applies to Web Forms.</span></span>

<span data-ttu-id="0307e-134">You can run the app locally without an Azure subscription, but you'll need one to deploy the application to the cloud.</span><span class="sxs-lookup"><span data-stu-id="0307e-134">You can run the app locally without an Azure subscription, but you'll need one to deploy the application to the cloud.</span></span> <span data-ttu-id="0307e-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span><span class="sxs-lookup"><span data-stu-id="0307e-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="0307e-136">The tutorial instructions work with either of the following products:</span><span class="sxs-lookup"><span data-stu-id="0307e-136">The tutorial instructions work with either of the following products:</span></span>

* <span data-ttu-id="0307e-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="0307e-137">Visual Studio 2013</span></span>
* <span data-ttu-id="0307e-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="0307e-138">Visual Studio 2015</span></span>
* <span data-ttu-id="0307e-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="0307e-139">Visual Studio 2017</span></span>

<span data-ttu-id="0307e-140">If you don't have one of these, Visual Studio may be installed automatically when you install the Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="0307e-140">If you don't have one of these, Visual Studio may be installed automatically when you install the Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="0307e-141">Application architecture</span><span class="sxs-lookup"><span data-stu-id="0307e-141">Application architecture</span></span>
<span data-ttu-id="0307e-142">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span><span class="sxs-lookup"><span data-stu-id="0307e-142">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="0307e-143">For each ad, the database stores two URLs, one for the full-size image and one for the thumbnail.</span><span class="sxs-lookup"><span data-stu-id="0307e-143">For each ad, the database stores two URLs, one for the full-size image and one for the thumbnail.</span></span>

![Ad table](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="0307e-145">When a user uploads an image, the front-end running in a web role stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span><span class="sxs-lookup"><span data-stu-id="0307e-145">When a user uploads an image, the front-end running in a web role stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="0307e-146">At the same time, it writes a message to an Azure queue.</span><span class="sxs-lookup"><span data-stu-id="0307e-146">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="0307e-147">A back-end process running in a worker role periodically polls the queue for new messages.</span><span class="sxs-lookup"><span data-stu-id="0307e-147">A back-end process running in a worker role periodically polls the queue for new messages.</span></span> <span data-ttu-id="0307e-148">When a new message appears, the worker role creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span><span class="sxs-lookup"><span data-stu-id="0307e-148">When a new message appears, the worker role creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="0307e-149">The following diagram shows how the parts of the application interact.</span><span class="sxs-lookup"><span data-stu-id="0307e-149">The following diagram shows how the parts of the application interact.</span></span>

![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-the-completed-solution"></a><span data-ttu-id="0307e-151">Download and run the completed solution</span><span class="sxs-lookup"><span data-stu-id="0307e-151">Download and run the completed solution</span></span>
1. <span data-ttu-id="0307e-152">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span><span class="sxs-lookup"><span data-stu-id="0307e-152">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="0307e-153">Start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0307e-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="0307e-154">From the **File** menu choose **Open Project**, navigate to where you downloaded the solution, and then open the solution file.</span><span class="sxs-lookup"><span data-stu-id="0307e-154">From the **File** menu choose **Open Project**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="0307e-155">Press CTRL+SHIFT+B to build the solution.</span><span class="sxs-lookup"><span data-stu-id="0307e-155">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="0307e-156">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span><span class="sxs-lookup"><span data-stu-id="0307e-156">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="0307e-157">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog box and clicking the **Restore** button at the top right.</span><span class="sxs-lookup"><span data-stu-id="0307e-157">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog box and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="0307e-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as the startup project.</span><span class="sxs-lookup"><span data-stu-id="0307e-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as the startup project.</span></span>
6. <span data-ttu-id="0307e-159">If you're using Visual Studio 2015 or higher, change the SQL Server connection string in the application *Web.config* file of the ContosoAdsWeb project and in the *ServiceConfiguration.Local.cscfg* file of the ContosoAdsCloudService project.</span><span class="sxs-lookup"><span data-stu-id="0307e-159">If you're using Visual Studio 2015 or higher, change the SQL Server connection string in the application *Web.config* file of the ContosoAdsWeb project and in the *ServiceConfiguration.Local.cscfg* file of the ContosoAdsCloudService project.</span></span> <span data-ttu-id="0307e-160">In each case, change "(localdb)\v11.0" to "(localdb)\MSSQLLocalDB".</span><span class="sxs-lookup"><span data-stu-id="0307e-160">In each case, change "(localdb)\v11.0" to "(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="0307e-161">Press CTRL+F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="0307e-161">Press CTRL+F5 to run the application.</span></span>

    <span data-ttu-id="0307e-162">When you run a cloud service project locally, Visual Studio automatically invokes the Azure *compute emulator* and Azure *storage emulator*.</span><span class="sxs-lookup"><span data-stu-id="0307e-162">When you run a cloud service project locally, Visual Studio automatically invokes the Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="0307e-163">The compute emulator uses your computer's resources to simulate the web role and worker role environments.</span><span class="sxs-lookup"><span data-stu-id="0307e-163">The compute emulator uses your computer's resources to simulate the web role and worker role environments.</span></span> <span data-ttu-id="0307e-164">The storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database to simulate Azure cloud storage.</span><span class="sxs-lookup"><span data-stu-id="0307e-164">The storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database to simulate Azure cloud storage.</span></span>

    <span data-ttu-id="0307e-165">The first time you run a cloud service project, it takes a minute or so for the emulators to start up.</span><span class="sxs-lookup"><span data-stu-id="0307e-165">The first time you run a cloud service project, it takes a minute or so for the emulators to start up.</span></span> <span data-ttu-id="0307e-166">When emulator startup is finished, the default browser opens to the application home page.</span><span class="sxs-lookup"><span data-stu-id="0307e-166">When emulator startup is finished, the default browser opens to the application home page.</span></span>

    ![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="0307e-168">Click  **Create an Ad**.</span><span class="sxs-lookup"><span data-stu-id="0307e-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="0307e-169">Enter some test data and select a *.jpg* image to upload, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0307e-169">Enter some test data and select a *.jpg* image to upload, and then click **Create**.</span></span>

    ![Create page](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="0307e-171">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span><span class="sxs-lookup"><span data-stu-id="0307e-171">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="0307e-172">Wait a moment and then refresh the Index page to see the thumbnail.</span><span class="sxs-lookup"><span data-stu-id="0307e-172">Wait a moment and then refresh the Index page to see the thumbnail.</span></span>

     ![Index page](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="0307e-174">Click **Details** for your ad to see the full-size image.</span><span class="sxs-lookup"><span data-stu-id="0307e-174">Click **Details** for your ad to see the full-size image.</span></span>

     ![Details page](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="0307e-176">You've been running the application entirely on your local computer, with no connection to the cloud.</span><span class="sxs-lookup"><span data-stu-id="0307e-176">You've been running the application entirely on your local computer, with no connection to the cloud.</span></span> <span data-ttu-id="0307e-177">The storage emulator stores the queue and blob data in a SQL Server Express LocalDB database, and the application stores the ad data in another LocalDB database.</span><span class="sxs-lookup"><span data-stu-id="0307e-177">The storage emulator stores the queue and blob data in a SQL Server Express LocalDB database, and the application stores the ad data in another LocalDB database.</span></span> <span data-ttu-id="0307e-178">Entity Framework Code First automatically created the ad database the first time the web app tried to access it.</span><span class="sxs-lookup"><span data-stu-id="0307e-178">Entity Framework Code First automatically created the ad database the first time the web app tried to access it.</span></span>

<span data-ttu-id="0307e-179">In the following section you'll configure the solution to use Azure cloud resources for queues, blobs, and the application database when it runs in the cloud.</span><span class="sxs-lookup"><span data-stu-id="0307e-179">In the following section you'll configure the solution to use Azure cloud resources for queues, blobs, and the application database when it runs in the cloud.</span></span> <span data-ttu-id="0307e-180">If you wanted to continue to run locally but use cloud storage and database resources, you could do that.</span><span class="sxs-lookup"><span data-stu-id="0307e-180">If you wanted to continue to run locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="0307e-181">It's just a matter of setting connection strings, which you'll see how to do.</span><span class="sxs-lookup"><span data-stu-id="0307e-181">It's just a matter of setting connection strings, which you'll see how to do.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="0307e-182">Deploy the application to Azure</span><span class="sxs-lookup"><span data-stu-id="0307e-182">Deploy the application to Azure</span></span>
<span data-ttu-id="0307e-183">You'll do the following steps to run the application in the cloud:</span><span class="sxs-lookup"><span data-stu-id="0307e-183">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="0307e-184">Create an Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="0307e-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="0307e-185">Create an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0307e-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="0307e-186">Create an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="0307e-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="0307e-187">Configure the solution to use your Azure SQL database when it runs in Azure.</span><span class="sxs-lookup"><span data-stu-id="0307e-187">Configure the solution to use your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="0307e-188">Configure the solution to use your Azure storage account when it runs in Azure.</span><span class="sxs-lookup"><span data-stu-id="0307e-188">Configure the solution to use your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="0307e-189">Deploy the project to your Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="0307e-189">Deploy the project to your Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="0307e-190">Create an Azure cloud service</span><span class="sxs-lookup"><span data-stu-id="0307e-190">Create an Azure cloud service</span></span>
<span data-ttu-id="0307e-191">An Azure cloud service is the environment the application will run in.</span><span class="sxs-lookup"><span data-stu-id="0307e-191">An Azure cloud service is the environment the application will run in.</span></span>

1. <span data-ttu-id="0307e-192">In your browser, open the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0307e-192">In your browser, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0307e-193">Click **Create a resource > Compute > Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="0307e-193">Click **Create a resource > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="0307e-194">In the DNS name input box, enter a URL prefix for the cloud service.</span><span class="sxs-lookup"><span data-stu-id="0307e-194">In the DNS name input box, enter a URL prefix for the cloud service.</span></span>

    <span data-ttu-id="0307e-195">This URL has to be unique.</span><span class="sxs-lookup"><span data-stu-id="0307e-195">This URL has to be unique.</span></span>  <span data-ttu-id="0307e-196">You'll get an error message if the prefix you choose is already in use.</span><span class="sxs-lookup"><span data-stu-id="0307e-196">You'll get an error message if the prefix you choose is already in use.</span></span>
4. <span data-ttu-id="0307e-197">Specify a new Resource group for the  service.</span><span class="sxs-lookup"><span data-stu-id="0307e-197">Specify a new Resource group for the  service.</span></span> <span data-ttu-id="0307e-198">Click **Create new** and then type a name in the Resource group input box, such as CS_contososadsRG.</span><span class="sxs-lookup"><span data-stu-id="0307e-198">Click **Create new** and then type a name in the Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="0307e-199">Choose the region where you want to deploy the application.</span><span class="sxs-lookup"><span data-stu-id="0307e-199">Choose the region where you want to deploy the application.</span></span>

    <span data-ttu-id="0307e-200">This field specifies which datacenter your cloud service will be hosted in.</span><span class="sxs-lookup"><span data-stu-id="0307e-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="0307e-201">For a production application, you'd choose the region closest to your customers.</span><span class="sxs-lookup"><span data-stu-id="0307e-201">For a production application, you'd choose the region closest to your customers.</span></span> <span data-ttu-id="0307e-202">For this tutorial, choose the region closest to you.</span><span class="sxs-lookup"><span data-stu-id="0307e-202">For this tutorial, choose the region closest to you.</span></span>
5. <span data-ttu-id="0307e-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0307e-203">Click **Create**.</span></span>

    <span data-ttu-id="0307e-204">In the following image, a cloud service is created with the URL CSvccontosoads.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="0307e-204">In the following image, a cloud service is created with the URL CSvccontosoads.cloudapp.net.</span></span>

    ![New Cloud Service](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="0307e-206">Create an Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="0307e-206">Create an Azure SQL database</span></span>
<span data-ttu-id="0307e-207">When the app runs in the cloud, it will use a cloud-based database.</span><span class="sxs-lookup"><span data-stu-id="0307e-207">When the app runs in the cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="0307e-208">In the [Azure portal](https://portal.azure.com), click **Create a resource > Databases > SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="0307e-208">In the [Azure portal](https://portal.azure.com), click **Create a resource > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="0307e-209">In the **Database Name** box, enter *contosoads*.</span><span class="sxs-lookup"><span data-stu-id="0307e-209">In the **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="0307e-210">In the **Resource group**, click **Use existing** and select the resource group used for the cloud service.</span><span class="sxs-lookup"><span data-stu-id="0307e-210">In the **Resource group**, click **Use existing** and select the resource group used for the cloud service.</span></span>
4. <span data-ttu-id="0307e-211">In the following image, click **Server - Configure required settings** and **Create a new server**.</span><span class="sxs-lookup"><span data-stu-id="0307e-211">In the following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![Tunnel to database server](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="0307e-213">Alternatively, if your subscription already has a server, you can select that server from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="0307e-213">Alternatively, if your subscription already has a server, you can select that server from the drop-down list.</span></span>
5. <span data-ttu-id="0307e-214">In the **Server name** box, enter *csvccontosodbserver*.</span><span class="sxs-lookup"><span data-stu-id="0307e-214">In the **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="0307e-215">Enter an administrator **Login Name** and **Password**.</span><span class="sxs-lookup"><span data-stu-id="0307e-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="0307e-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span><span class="sxs-lookup"><span data-stu-id="0307e-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="0307e-217">You're entering a new name and password that you're defining now to use later when you access the database.</span><span class="sxs-lookup"><span data-stu-id="0307e-217">You're entering a new name and password that you're defining now to use later when you access the database.</span></span> <span data-ttu-id="0307e-218">If you selected a server that you created previously, you'll be prompted for the password to the administrative user account you already created.</span><span class="sxs-lookup"><span data-stu-id="0307e-218">If you selected a server that you created previously, you'll be prompted for the password to the administrative user account you already created.</span></span>
7. <span data-ttu-id="0307e-219">Choose the same **Location** that you chose for the cloud service.</span><span class="sxs-lookup"><span data-stu-id="0307e-219">Choose the same **Location** that you chose for the cloud service.</span></span>

    <span data-ttu-id="0307e-220">When the cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span><span class="sxs-lookup"><span data-stu-id="0307e-220">When the cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span></span> <span data-ttu-id="0307e-221">Bandwidth within a data center is free.</span><span class="sxs-lookup"><span data-stu-id="0307e-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="0307e-222">Check **Allow azure services to access server**.</span><span class="sxs-lookup"><span data-stu-id="0307e-222">Check **Allow azure services to access server**.</span></span>
9. <span data-ttu-id="0307e-223">Click **Select** for the new server.</span><span class="sxs-lookup"><span data-stu-id="0307e-223">Click **Select** for the new server.</span></span>

    ![New SQL Database server](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="0307e-225">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0307e-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="0307e-226">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="0307e-226">Create an Azure storage account</span></span>
<span data-ttu-id="0307e-227">An Azure storage account provides resources for storing queue and blob data in the cloud.</span><span class="sxs-lookup"><span data-stu-id="0307e-227">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span>

<span data-ttu-id="0307e-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span><span class="sxs-lookup"><span data-stu-id="0307e-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="0307e-229">For this tutorial, you'll use just one account.</span><span class="sxs-lookup"><span data-stu-id="0307e-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="0307e-230">In the [Azure portal](https://portal.azure.com), click **Create a resource > Storage > Storage account - blob, file, table, queue**.</span><span class="sxs-lookup"><span data-stu-id="0307e-230">In the [Azure portal](https://portal.azure.com), click **Create a resource > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="0307e-231">In the **Name** box, enter a URL prefix.</span><span class="sxs-lookup"><span data-stu-id="0307e-231">In the **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="0307e-232">This prefix plus the text you see under the box will be the unique URL to your storage account.</span><span class="sxs-lookup"><span data-stu-id="0307e-232">This prefix plus the text you see under the box will be the unique URL to your storage account.</span></span> <span data-ttu-id="0307e-233">If the prefix you enter has already been used by someone else, you'll have to choose a different prefix.</span><span class="sxs-lookup"><span data-stu-id="0307e-233">If the prefix you enter has already been used by someone else, you'll have to choose a different prefix.</span></span>
3. <span data-ttu-id="0307e-234">Set the **Deployment model** to *Classic*.</span><span class="sxs-lookup"><span data-stu-id="0307e-234">Set the **Deployment model** to *Classic*.</span></span>

4. <span data-ttu-id="0307e-235">Set the **Replication** drop-down list to **Locally redundant storage**.</span><span class="sxs-lookup"><span data-stu-id="0307e-235">Set the **Replication** drop-down list to **Locally redundant storage**.</span></span>

    <span data-ttu-id="0307e-236">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover if a major disaster occurs in the primary location.</span><span class="sxs-lookup"><span data-stu-id="0307e-236">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover if a major disaster occurs in the primary location.</span></span> <span data-ttu-id="0307e-237">Geo-replication can incur additional costs.</span><span class="sxs-lookup"><span data-stu-id="0307e-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="0307e-238">For test and development accounts, you generally don't want to pay for geo-replication.</span><span class="sxs-lookup"><span data-stu-id="0307e-238">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="0307e-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="0307e-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="0307e-240">In the **Resource group**, click **Use existing** and select the resource group used for the cloud service.</span><span class="sxs-lookup"><span data-stu-id="0307e-240">In the **Resource group**, click **Use existing** and select the resource group used for the cloud service.</span></span>
6. <span data-ttu-id="0307e-241">Set the **Location** drop-down list to the same region you chose for the cloud service.</span><span class="sxs-lookup"><span data-stu-id="0307e-241">Set the **Location** drop-down list to the same region you chose for the cloud service.</span></span>

    <span data-ttu-id="0307e-242">When the cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span><span class="sxs-lookup"><span data-stu-id="0307e-242">When the cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span></span> <span data-ttu-id="0307e-243">Bandwidth within a data center is free.</span><span class="sxs-lookup"><span data-stu-id="0307e-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="0307e-244">Azure affinity groups provide a mechanism to minimize the distance between resources in a data center, which can reduce latency.</span><span class="sxs-lookup"><span data-stu-id="0307e-244">Azure affinity groups provide a mechanism to minimize the distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="0307e-245">This tutorial does not use affinity groups.</span><span class="sxs-lookup"><span data-stu-id="0307e-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="0307e-246">For more information, see [How to Create an Affinity Group in Azure](https://msdn.microsoft.com/library/azure/gg715317.aspx).</span><span class="sxs-lookup"><span data-stu-id="0307e-246">For more information, see [How to Create an Affinity Group in Azure](https://msdn.microsoft.com/library/azure/gg715317.aspx).</span></span>
7. <span data-ttu-id="0307e-247">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0307e-247">Click **Create**.</span></span>

    ![New storage account](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="0307e-249">In the image, a storage account is created with the URL `csvccontosoads.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="0307e-249">In the image, a storage account is created with the URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-the-solution-to-use-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="0307e-250">Configure the solution to use your Azure SQL database when it runs in Azure</span><span class="sxs-lookup"><span data-stu-id="0307e-250">Configure the solution to use your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="0307e-251">The web project and the worker role project each has its own database connection string, and each needs to point to the Azure SQL database when the app runs in Azure.</span><span class="sxs-lookup"><span data-stu-id="0307e-251">The web project and the worker role project each has its own database connection string, and each needs to point to the Azure SQL database when the app runs in Azure.</span></span>

<span data-ttu-id="0307e-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for the web role and a cloud service environment setting for the worker role.</span><span class="sxs-lookup"><span data-stu-id="0307e-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for the web role and a cloud service environment setting for the worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="0307e-253">In this section and the next section, you store credentials in project files.</span><span class="sxs-lookup"><span data-stu-id="0307e-253">In this section and the next section, you store credentials in project files.</span></span> <span data-ttu-id="0307e-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="0307e-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="0307e-255">In the ContosoAdsWeb project, open the *Web.Release.config* transform file for the application *Web.config* file, delete the comment block that contains a `<connectionStrings>` element, and paste the following code in its place.</span><span class="sxs-lookup"><span data-stu-id="0307e-255">In the ContosoAdsWeb project, open the *Web.Release.config* transform file for the application *Web.config* file, delete the comment block that contains a `<connectionStrings>` element, and paste the following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="0307e-256">Leave the file open for editing.</span><span class="sxs-lookup"><span data-stu-id="0307e-256">Leave the file open for editing.</span></span>
2. <span data-ttu-id="0307e-257">In the [Azure portal](https://portal.azure.com), click **SQL Databases** in the left pane, click the database you created for this tutorial, and then click **Show connection strings**.</span><span class="sxs-lookup"><span data-stu-id="0307e-257">In the [Azure portal](https://portal.azure.com), click **SQL Databases** in the left pane, click the database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![Show connection strings](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="0307e-259">The portal displays connection strings, with a placeholder for the password.</span><span class="sxs-lookup"><span data-stu-id="0307e-259">The portal displays connection strings, with a placeholder for the password.</span></span>

    ![Connection strings](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="0307e-261">In the *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place the ADO.NET connection string from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0307e-261">In the *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place the ADO.NET connection string from the Azure portal.</span></span>
4. <span data-ttu-id="0307e-262">In the connection string that you pasted into the *Web.Release.config* transform file, replace `{your_password_here}` with the password you created for the new SQL database.</span><span class="sxs-lookup"><span data-stu-id="0307e-262">In the connection string that you pasted into the *Web.Release.config* transform file, replace `{your_password_here}` with the password you created for the new SQL database.</span></span>
5. <span data-ttu-id="0307e-263">Save the file.</span><span class="sxs-lookup"><span data-stu-id="0307e-263">Save the file.</span></span>  
6. <span data-ttu-id="0307e-264">Select and copy the connection string (without the surrounding quotation marks) for use in the following steps for configuring the worker role project.</span><span class="sxs-lookup"><span data-stu-id="0307e-264">Select and copy the connection string (without the surrounding quotation marks) for use in the following steps for configuring the worker role project.</span></span>
7. <span data-ttu-id="0307e-265">In **Solution Explorer**, under **Roles** in the cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="0307e-265">In **Solution Explorer**, under **Roles** in the cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="0307e-267">Click the **Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="0307e-267">Click the **Settings** tab.</span></span>
9. <span data-ttu-id="0307e-268">Change **Service Configuration** to **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="0307e-268">Change **Service Configuration** to **Cloud**.</span></span>
10. <span data-ttu-id="0307e-269">Select the **Value** field for the `ContosoAdsDbConnectionString` setting, and then paste the connection string that you copied from the previous section of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="0307e-269">Select the **Value** field for the `ContosoAdsDbConnectionString` setting, and then paste the connection string that you copied from the previous section of the tutorial.</span></span>

     ![Database connection string for worker role](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="0307e-271">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="0307e-271">Save your changes.</span></span>  

### <a name="configure-the-solution-to-use-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="0307e-272">Configure the solution to use your Azure storage account when it runs in Azure</span><span class="sxs-lookup"><span data-stu-id="0307e-272">Configure the solution to use your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="0307e-273">Azure storage account connection strings for both the web role project and the worker role project are stored in environment settings in the cloud service project.</span><span class="sxs-lookup"><span data-stu-id="0307e-273">Azure storage account connection strings for both the web role project and the worker role project are stored in environment settings in the cloud service project.</span></span> <span data-ttu-id="0307e-274">For each project, there is a separate set of settings to be used when the application runs locally and when it runs in the cloud.</span><span class="sxs-lookup"><span data-stu-id="0307e-274">For each project, there is a separate set of settings to be used when the application runs locally and when it runs in the cloud.</span></span> <span data-ttu-id="0307e-275">You'll update the cloud environment settings for both web and worker role projects.</span><span class="sxs-lookup"><span data-stu-id="0307e-275">You'll update the cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="0307e-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in the **ContosoAdsCloudService** project, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="0307e-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in the **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="0307e-278">Click the **Settings** tab. In the **Service Configuration** drop-down box, choose **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="0307e-278">Click the **Settings** tab. In the **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Cloud configuration](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="0307e-280">Select the **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at the right end of the line.</span><span class="sxs-lookup"><span data-stu-id="0307e-280">Select the **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at the right end of the line.</span></span> <span data-ttu-id="0307e-281">Click the ellipsis button to open the **Create Storage Account Connection String** dialog box.</span><span class="sxs-lookup"><span data-stu-id="0307e-281">Click the ellipsis button to open the **Create Storage Account Connection String** dialog box.</span></span>

    ![Open Connection String Create box](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="0307e-283">In the **Create Storage Connection String** dialog box, click **Your subscription**, choose the storage account that you created earlier, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0307e-283">In the **Create Storage Connection String** dialog box, click **Your subscription**, choose the storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="0307e-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="0307e-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Create Storage Connection String](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="0307e-286">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="0307e-286">Save your changes.</span></span>
6. <span data-ttu-id="0307e-287">Follow the same procedure that you used for the `StorageConnectionString` connection string to set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span><span class="sxs-lookup"><span data-stu-id="0307e-287">Follow the same procedure that you used for the `StorageConnectionString` connection string to set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="0307e-288">This connection string is used for logging.</span><span class="sxs-lookup"><span data-stu-id="0307e-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="0307e-289">Follow the same procedure that you used for the **ContosoAdsWeb** role to set both connection strings for the **ContosoAdsWorker** role.</span><span class="sxs-lookup"><span data-stu-id="0307e-289">Follow the same procedure that you used for the **ContosoAdsWeb** role to set both connection strings for the **ContosoAdsWorker** role.</span></span> <span data-ttu-id="0307e-290">Don't forget to set **Service Configuration** to **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="0307e-290">Don't forget to set **Service Configuration** to **Cloud**.</span></span>

<span data-ttu-id="0307e-291">The role environment settings that you have configured using the Visual Studio UI are stored in the following files in the ContosoAdsCloudService project:</span><span class="sxs-lookup"><span data-stu-id="0307e-291">The role environment settings that you have configured using the Visual Studio UI are stored in the following files in the ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="0307e-292">*ServiceDefinition.csdef* - Defines the setting names.</span><span class="sxs-lookup"><span data-stu-id="0307e-292">*ServiceDefinition.csdef* - Defines the setting names.</span></span>
* <span data-ttu-id="0307e-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when the app runs in the cloud.</span><span class="sxs-lookup"><span data-stu-id="0307e-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when the app runs in the cloud.</span></span>
* <span data-ttu-id="0307e-294">*ServiceConfiguration.Local.cscfg* - Provides values for when the app runs locally.</span><span class="sxs-lookup"><span data-stu-id="0307e-294">*ServiceConfiguration.Local.cscfg* - Provides values for when the app runs locally.</span></span>

<span data-ttu-id="0307e-295">For example, the ServiceDefinition.csdef includes the following definitions:</span><span class="sxs-lookup"><span data-stu-id="0307e-295">For example, the ServiceDefinition.csdef includes the following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="0307e-296">And the *ServiceConfiguration.Cloud.cscfg* file includes the values you entered for those settings in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0307e-296">And the *ServiceConfiguration.Cloud.cscfg* file includes the values you entered for those settings in Visual Studio.</span></span>

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

<span data-ttu-id="0307e-297">The `<Instances>` setting specifies the number of virtual machines that Azure will run the worker role code on.</span><span class="sxs-lookup"><span data-stu-id="0307e-297">The `<Instances>` setting specifies the number of virtual machines that Azure will run the worker role code on.</span></span> <span data-ttu-id="0307e-298">The [Next steps](#next-steps) section includes links to more information about scaling out a cloud service,</span><span class="sxs-lookup"><span data-stu-id="0307e-298">The [Next steps](#next-steps) section includes links to more information about scaling out a cloud service,</span></span>

### <a name="deploy-the-project-to-azure"></a><span data-ttu-id="0307e-299">Deploy the project to Azure</span><span class="sxs-lookup"><span data-stu-id="0307e-299">Deploy the project to Azure</span></span>
1. <span data-ttu-id="0307e-300">In **Solution Explorer**, right-click the **ContosoAdsCloudService** cloud project and then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="0307e-300">In **Solution Explorer**, right-click the **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Publish menu](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="0307e-302">In the **Sign in** step of the **Publish Azure Application** wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0307e-302">In the **Sign in** step of the **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Sign in step](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="0307e-304">In the **Settings** step of the wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0307e-304">In the **Settings** step of the wizard, click **Next**.</span></span>

    ![Settings step](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="0307e-306">The default settings in the **Advanced** tab are fine for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="0307e-306">The default settings in the **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="0307e-307">For information about the advanced tab, see [Publish Azure Application Wizard](https://docs.microsoft.com/azure/vs-azure-tools-publish-azure-application-wizard).</span><span class="sxs-lookup"><span data-stu-id="0307e-307">For information about the advanced tab, see [Publish Azure Application Wizard](https://docs.microsoft.com/azure/vs-azure-tools-publish-azure-application-wizard).</span></span>
4. <span data-ttu-id="0307e-308">In the **Summary** step, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="0307e-308">In the **Summary** step, click **Publish**.</span></span>

    ![Summary step](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="0307e-310">The **Azure Activity Log** window opens in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0307e-310">The **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="0307e-311">Click the right arrow icon to expand the deployment details.</span><span class="sxs-lookup"><span data-stu-id="0307e-311">Click the right arrow icon to expand the deployment details.</span></span>

    <span data-ttu-id="0307e-312">The deployment can take up to 5 minutes or more to complete.</span><span class="sxs-lookup"><span data-stu-id="0307e-312">The deployment can take up to 5 minutes or more to complete.</span></span>

    ![Azure Activity Log window](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="0307e-314">When the deployment status is complete, click the **Web app URL** to start the application.</span><span class="sxs-lookup"><span data-stu-id="0307e-314">When the deployment status is complete, click the **Web app URL** to start the application.</span></span>
7. <span data-ttu-id="0307e-315">You can now test the app by creating, viewing, and editing some ads, as you did when you ran the application locally.</span><span class="sxs-lookup"><span data-stu-id="0307e-315">You can now test the app by creating, viewing, and editing some ads, as you did when you ran the application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="0307e-316">When you're finished testing, delete or stop the cloud service.</span><span class="sxs-lookup"><span data-stu-id="0307e-316">When you're finished testing, delete or stop the cloud service.</span></span> <span data-ttu-id="0307e-317">Even if you're not using the cloud service, it's accruing charges because virtual machine resources are reserved for it.</span><span class="sxs-lookup"><span data-stu-id="0307e-317">Even if you're not using the cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="0307e-318">And if you leave it running, anyone who finds your URL can create and view ads.</span><span class="sxs-lookup"><span data-stu-id="0307e-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="0307e-319">In the [Azure portal](https://portal.azure.com), go to the **Overview** tab for your cloud service, and then click the **Delete** button at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="0307e-319">In the [Azure portal](https://portal.azure.com), go to the **Overview** tab for your cloud service, and then click the **Delete** button at the top of the page.</span></span> <span data-ttu-id="0307e-320">If you just want to temporarily prevent others from accessing the site, click **Stop** instead.</span><span class="sxs-lookup"><span data-stu-id="0307e-320">If you just want to temporarily prevent others from accessing the site, click **Stop** instead.</span></span> <span data-ttu-id="0307e-321">In that case, charges will continue to accrue.</span><span class="sxs-lookup"><span data-stu-id="0307e-321">In that case, charges will continue to accrue.</span></span> <span data-ttu-id="0307e-322">You can follow a similar procedure to delete the SQL database and storage account when you no longer need them.</span><span class="sxs-lookup"><span data-stu-id="0307e-322">You can follow a similar procedure to delete the SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-the-application-from-scratch"></a><span data-ttu-id="0307e-323">Create the application from scratch</span><span class="sxs-lookup"><span data-stu-id="0307e-323">Create the application from scratch</span></span>
<span data-ttu-id="0307e-324">If you haven't already downloaded [the completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span><span class="sxs-lookup"><span data-stu-id="0307e-324">If you haven't already downloaded [the completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="0307e-325">You'll copy files from the downloaded project into the new project.</span><span class="sxs-lookup"><span data-stu-id="0307e-325">You'll copy files from the downloaded project into the new project.</span></span>

<span data-ttu-id="0307e-326">Creating the Contoso Ads application involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="0307e-326">Creating the Contoso Ads application involves the following steps:</span></span>

* <span data-ttu-id="0307e-327">Create a cloud service Visual Studio solution.</span><span class="sxs-lookup"><span data-stu-id="0307e-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="0307e-328">Update and add NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="0307e-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="0307e-329">Set project references.</span><span class="sxs-lookup"><span data-stu-id="0307e-329">Set project references.</span></span>
* <span data-ttu-id="0307e-330">Configure connection strings.</span><span class="sxs-lookup"><span data-stu-id="0307e-330">Configure connection strings.</span></span>
* <span data-ttu-id="0307e-331">Add code files.</span><span class="sxs-lookup"><span data-stu-id="0307e-331">Add code files.</span></span>

<span data-ttu-id="0307e-332">After the solution is created, you'll review the code that is unique to cloud service projects and Azure blobs and queues.</span><span class="sxs-lookup"><span data-stu-id="0307e-332">After the solution is created, you'll review the code that is unique to cloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="0307e-333">Create a cloud service Visual Studio solution</span><span class="sxs-lookup"><span data-stu-id="0307e-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="0307e-334">In Visual Studio, choose **New Project** from the **File** menu.</span><span class="sxs-lookup"><span data-stu-id="0307e-334">In Visual Studio, choose **New Project** from the **File** menu.</span></span>
2. <span data-ttu-id="0307e-335">In the left pane of the **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose the **Azure Cloud Service** template.</span><span class="sxs-lookup"><span data-stu-id="0307e-335">In the left pane of the **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose the **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="0307e-336">Name the project and solution ContosoAdsCloudService, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0307e-336">Name the project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![New Project](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="0307e-338">In the **New Azure Cloud Service** dialog box, add a web role and a worker role.</span><span class="sxs-lookup"><span data-stu-id="0307e-338">In the **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="0307e-339">Name the web role ContosoAdsWeb, and name the worker role ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="0307e-339">Name the web role ContosoAdsWeb, and name the worker role ContosoAdsWorker.</span></span> <span data-ttu-id="0307e-340">(Use the pencil icon in the right-hand pane to change the default names of the roles.)</span><span class="sxs-lookup"><span data-stu-id="0307e-340">(Use the pencil icon in the right-hand pane to change the default names of the roles.)</span></span>

    ![New Cloud Service Project](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="0307e-342">When you see the **New ASP.NET Project** dialog box for the web role, choose the MVC template, and then click **Change Authentication**.</span><span class="sxs-lookup"><span data-stu-id="0307e-342">When you see the **New ASP.NET Project** dialog box for the web role, choose the MVC template, and then click **Change Authentication**.</span></span>

    ![Change Authentication](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="0307e-344">In the **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0307e-344">In the **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![No Authentication](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="0307e-346">In the **New ASP.NET Project** dialog, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0307e-346">In the **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="0307e-347">In **Solution Explorer**, right-click the solution (not one of the projects), and choose **Add - New Project**.</span><span class="sxs-lookup"><span data-stu-id="0307e-347">In **Solution Explorer**, right-click the solution (not one of the projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="0307e-348">In the **Add New Project** dialog box, choose **Windows** under **Visual C#** in the left pane, and then click the **Class Library** template.</span><span class="sxs-lookup"><span data-stu-id="0307e-348">In the **Add New Project** dialog box, choose **Windows** under **Visual C#** in the left pane, and then click the **Class Library** template.</span></span>  
10. <span data-ttu-id="0307e-349">Name the project *ContosoAdsCommon*, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0307e-349">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="0307e-350">You need to reference the Entity Framework context and the data model from both web and worker role projects.</span><span class="sxs-lookup"><span data-stu-id="0307e-350">You need to reference the Entity Framework context and the data model from both web and worker role projects.</span></span> <span data-ttu-id="0307e-351">As an alternative, you could define the EF-related classes in the web role project and reference that project from the worker role project.</span><span class="sxs-lookup"><span data-stu-id="0307e-351">As an alternative, you could define the EF-related classes in the web role project and reference that project from the worker role project.</span></span> <span data-ttu-id="0307e-352">But in the alternative approach, your worker role project would have a reference to web assemblies that it doesn't need.</span><span class="sxs-lookup"><span data-stu-id="0307e-352">But in the alternative approach, your worker role project would have a reference to web assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="0307e-353">Update and add NuGet packages</span><span class="sxs-lookup"><span data-stu-id="0307e-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="0307e-354">Open the **Manage NuGet Packages** dialog box for the solution.</span><span class="sxs-lookup"><span data-stu-id="0307e-354">Open the **Manage NuGet Packages** dialog box for the solution.</span></span>
2. <span data-ttu-id="0307e-355">At the top of the window, select **Updates**.</span><span class="sxs-lookup"><span data-stu-id="0307e-355">At the top of the window, select **Updates**.</span></span>
3. <span data-ttu-id="0307e-356">Look for the *WindowsAzure.Storage* package, and if it's in the list, select it and select the web and worker projects to update it in, and then click **Update**.</span><span class="sxs-lookup"><span data-stu-id="0307e-356">Look for the *WindowsAzure.Storage* package, and if it's in the list, select it and select the web and worker projects to update it in, and then click **Update**.</span></span>

    <span data-ttu-id="0307e-357">The storage client library is updated more frequently than Visual Studio project templates, so you'll often find that the version in a newly-created project needs to be updated.</span><span class="sxs-lookup"><span data-stu-id="0307e-357">The storage client library is updated more frequently than Visual Studio project templates, so you'll often find that the version in a newly-created project needs to be updated.</span></span>
4. <span data-ttu-id="0307e-358">At the top of the window, select **Browse**.</span><span class="sxs-lookup"><span data-stu-id="0307e-358">At the top of the window, select **Browse**.</span></span>
5. <span data-ttu-id="0307e-359">Find the *EntityFramework* NuGet package, and install it in all three projects.</span><span class="sxs-lookup"><span data-stu-id="0307e-359">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="0307e-360">Find the *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in the worker role project.</span><span class="sxs-lookup"><span data-stu-id="0307e-360">Find the *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in the worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="0307e-361">Set project references</span><span class="sxs-lookup"><span data-stu-id="0307e-361">Set project references</span></span>
1. <span data-ttu-id="0307e-362">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span><span class="sxs-lookup"><span data-stu-id="0307e-362">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="0307e-363">Right-click the ContosoAdsWeb project, and then click **References** - **Add References**.</span><span class="sxs-lookup"><span data-stu-id="0307e-363">Right-click the ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="0307e-364">In the **Reference Manager** dialog box, select **Solution – Projects** in the left pane, select **ContosoAdsCommon**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0307e-364">In the **Reference Manager** dialog box, select **Solution – Projects** in the left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="0307e-365">In the ContosoAdsWorker project, set a reference to the ContosAdsCommon project.</span><span class="sxs-lookup"><span data-stu-id="0307e-365">In the ContosoAdsWorker project, set a reference to the ContosAdsCommon project.</span></span>

    <span data-ttu-id="0307e-366">ContosoAdsCommon will contain the Entity Framework data model and context class, which will be used by both the front-end and back-end.</span><span class="sxs-lookup"><span data-stu-id="0307e-366">ContosoAdsCommon will contain the Entity Framework data model and context class, which will be used by both the front-end and back-end.</span></span>
3. <span data-ttu-id="0307e-367">In the ContosoAdsWorker project, set a reference to `System.Drawing`.</span><span class="sxs-lookup"><span data-stu-id="0307e-367">In the ContosoAdsWorker project, set a reference to `System.Drawing`.</span></span>

    <span data-ttu-id="0307e-368">This assembly is used by the back-end to convert images to thumbnails.</span><span class="sxs-lookup"><span data-stu-id="0307e-368">This assembly is used by the back-end to convert images to thumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="0307e-369">Configure connection strings</span><span class="sxs-lookup"><span data-stu-id="0307e-369">Configure connection strings</span></span>
<span data-ttu-id="0307e-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span><span class="sxs-lookup"><span data-stu-id="0307e-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="0307e-371">The deployment instructions earlier in the tutorial explain how to set up the connection strings for when the app runs in the cloud.</span><span class="sxs-lookup"><span data-stu-id="0307e-371">The deployment instructions earlier in the tutorial explain how to set up the connection strings for when the app runs in the cloud.</span></span>

1. <span data-ttu-id="0307e-372">In the ContosoAdsWeb project, open the application Web.config file, and insert the following `connectionStrings` element after the `configSections` element.</span><span class="sxs-lookup"><span data-stu-id="0307e-372">In the ContosoAdsWeb project, open the application Web.config file, and insert the following `connectionStrings` element after the `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="0307e-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span><span class="sxs-lookup"><span data-stu-id="0307e-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="0307e-374">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="0307e-374">Save your changes.</span></span>
3. <span data-ttu-id="0307e-375">In the ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="0307e-375">In the ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="0307e-377">In the **ContosAdsWeb [Role]** properties window, click the **Settings** tab, and then click **Add Setting**.</span><span class="sxs-lookup"><span data-stu-id="0307e-377">In the **ContosAdsWeb [Role]** properties window, click the **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="0307e-378">Leave **Service Configuration** set to **All Configurations**.</span><span class="sxs-lookup"><span data-stu-id="0307e-378">Leave **Service Configuration** set to **All Configurations**.</span></span>
5. <span data-ttu-id="0307e-379">Add a setting named *StorageConnectionString*.</span><span class="sxs-lookup"><span data-stu-id="0307e-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="0307e-380">Set **Type** to *ConnectionString*, and set **Value** to *UseDevelopmentStorage=true*.</span><span class="sxs-lookup"><span data-stu-id="0307e-380">Set **Type** to *ConnectionString*, and set **Value** to *UseDevelopmentStorage=true*.</span></span>

    ![New connection string](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="0307e-382">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="0307e-382">Save your changes.</span></span>
7. <span data-ttu-id="0307e-383">Follow the same procedure to add a storage connection string in the ContosoAdsWorker role properties.</span><span class="sxs-lookup"><span data-stu-id="0307e-383">Follow the same procedure to add a storage connection string in the ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="0307e-384">Still in the **ContosoAdsWorker [Role]** properties window, add another connection string:</span><span class="sxs-lookup"><span data-stu-id="0307e-384">Still in the **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="0307e-385">Name: ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="0307e-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="0307e-386">Type: String</span><span class="sxs-lookup"><span data-stu-id="0307e-386">Type: String</span></span>
   * <span data-ttu-id="0307e-387">Value: Paste the same connection string you used for the web role project.</span><span class="sxs-lookup"><span data-stu-id="0307e-387">Value: Paste the same connection string you used for the web role project.</span></span> <span data-ttu-id="0307e-388">(The following example is for Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="0307e-388">(The following example is for Visual Studio 2013.</span></span> <span data-ttu-id="0307e-389">Don't forget to change the Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span><span class="sxs-lookup"><span data-stu-id="0307e-389">Don't forget to change the Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="0307e-390">Add code files</span><span class="sxs-lookup"><span data-stu-id="0307e-390">Add code files</span></span>
<span data-ttu-id="0307e-391">In this section, you copy code files from the downloaded solution into the new solution.</span><span class="sxs-lookup"><span data-stu-id="0307e-391">In this section, you copy code files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="0307e-392">The following sections will show and explain key parts of this code.</span><span class="sxs-lookup"><span data-stu-id="0307e-392">The following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="0307e-393">To add files to a project or a folder, right-click the project or folder and click **Add** - **Existing Item**.</span><span class="sxs-lookup"><span data-stu-id="0307e-393">To add files to a project or a folder, right-click the project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="0307e-394">Select the files you want and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="0307e-394">Select the files you want and then click **Add**.</span></span> <span data-ttu-id="0307e-395">If asked whether you want to replace existing files, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="0307e-395">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="0307e-396">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the *Ad.cs* and *ContosoAdscontext.cs* files from the downloaded project.</span><span class="sxs-lookup"><span data-stu-id="0307e-396">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the *Ad.cs* and *ContosoAdscontext.cs* files from the downloaded project.</span></span>
2. <span data-ttu-id="0307e-397">In the ContosoAdsWeb project, add the following files from the downloaded project.</span><span class="sxs-lookup"><span data-stu-id="0307e-397">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="0307e-398">*Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="0307e-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="0307e-399">In the *Views\Shared* folder: *\_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="0307e-399">In the *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="0307e-400">In the *Views\Home* folder: *Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="0307e-400">In the *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="0307e-401">In the *Controllers* folder: *AdController.cs*.</span><span class="sxs-lookup"><span data-stu-id="0307e-401">In the *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="0307e-402">In the *Views\Ad* folder (create the folder first): five *.cshtml* files.</span><span class="sxs-lookup"><span data-stu-id="0307e-402">In the *Views\Ad* folder (create the folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="0307e-403">In the ContosoAdsWorker project, add *WorkerRole.cs* from the downloaded project.</span><span class="sxs-lookup"><span data-stu-id="0307e-403">In the ContosoAdsWorker project, add *WorkerRole.cs* from the downloaded project.</span></span>

<span data-ttu-id="0307e-404">You can now build and run the application as instructed earlier in the tutorial, and the app will use local database and storage emulator resources.</span><span class="sxs-lookup"><span data-stu-id="0307e-404">You can now build and run the application as instructed earlier in the tutorial, and the app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="0307e-405">The following sections explain the code related to working with the Azure environment, blobs, and queues.</span><span class="sxs-lookup"><span data-stu-id="0307e-405">The following sections explain the code related to working with the Azure environment, blobs, and queues.</span></span> <span data-ttu-id="0307e-406">This tutorial does not explain how to create MVC controllers and views using scaffolding, how to write Entity Framework code that works with SQL Server databases, or the basics of asynchronous programming in ASP.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="0307e-406">This tutorial does not explain how to create MVC controllers and views using scaffolding, how to write Entity Framework code that works with SQL Server databases, or the basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="0307e-407">For information about these topics, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="0307e-407">For information about these topics, see the following resources:</span></span>

* [<span data-ttu-id="0307e-408">Get started with MVC 5</span><span class="sxs-lookup"><span data-stu-id="0307e-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="0307e-409">Get started with EF 6 and MVC 5</span><span class="sxs-lookup"><span data-stu-id="0307e-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="0307e-410">[Introduction to asynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="0307e-410">[Introduction to asynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="0307e-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="0307e-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="0307e-412">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span><span class="sxs-lookup"><span data-stu-id="0307e-412">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="0307e-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="0307e-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="0307e-414">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span><span class="sxs-lookup"><span data-stu-id="0307e-414">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

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

<span data-ttu-id="0307e-415">The class has two constructors.</span><span class="sxs-lookup"><span data-stu-id="0307e-415">The class has two constructors.</span></span> <span data-ttu-id="0307e-416">The first of them is used by the web project, and specifies the name of a connection string that is stored in the Web.config file.</span><span class="sxs-lookup"><span data-stu-id="0307e-416">The first of them is used by the web project, and specifies the name of a connection string that is stored in the Web.config file.</span></span> <span data-ttu-id="0307e-417">The second constructor enables you to pass in the actual connection string used by the worker role project, since it doesn't have a Web.config file.</span><span class="sxs-lookup"><span data-stu-id="0307e-417">The second constructor enables you to pass in the actual connection string used by the worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="0307e-418">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span><span class="sxs-lookup"><span data-stu-id="0307e-418">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="0307e-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="0307e-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="0307e-420">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span><span class="sxs-lookup"><span data-stu-id="0307e-420">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="0307e-421">This ensures that whenever you start using a new storage account, or start using the storage emulator on a new computer, the required blob container and queue will be created automatically.</span><span class="sxs-lookup"><span data-stu-id="0307e-421">This ensures that whenever you start using a new storage account, or start using the storage emulator on a new computer, the required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="0307e-422">The code gets access to the storage account by using the storage connection string from the *.cscfg* file.</span><span class="sxs-lookup"><span data-stu-id="0307e-422">The code gets access to the storage account by using the storage connection string from the *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="0307e-423">Then it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span><span class="sxs-lookup"><span data-stu-id="0307e-423">Then it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="0307e-424">By default, new containers only allow clients with storage account credentials to access blobs.</span><span class="sxs-lookup"><span data-stu-id="0307e-424">By default, new containers only allow clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="0307e-425">The website needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span><span class="sxs-lookup"><span data-stu-id="0307e-425">The website needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

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

<span data-ttu-id="0307e-426">Similar code gets a reference to the *images* queue and creates a new queue.</span><span class="sxs-lookup"><span data-stu-id="0307e-426">Similar code gets a reference to the *images* queue and creates a new queue.</span></span> <span data-ttu-id="0307e-427">In this case, no permissions change is needed.</span><span class="sxs-lookup"><span data-stu-id="0307e-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="0307e-428">ContosoAdsWeb - \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="0307e-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="0307e-429">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span><span class="sxs-lookup"><span data-stu-id="0307e-429">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="0307e-430">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="0307e-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="0307e-431">The *Views\Home\Index.cshtml* file displays category links on the home page.</span><span class="sxs-lookup"><span data-stu-id="0307e-431">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="0307e-432">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span><span class="sxs-lookup"><span data-stu-id="0307e-432">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="0307e-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="0307e-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="0307e-434">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span><span class="sxs-lookup"><span data-stu-id="0307e-434">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="0307e-435">Then the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="0307e-435">Then the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="0307e-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span><span class="sxs-lookup"><span data-stu-id="0307e-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="0307e-437">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span><span class="sxs-lookup"><span data-stu-id="0307e-437">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="0307e-438">The retry policy specified here waits three seconds after each try for up to three tries.</span><span class="sxs-lookup"><span data-stu-id="0307e-438">The retry policy specified here waits three seconds after each try for up to three tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="0307e-439">Similar code gets a reference to the *images* queue.</span><span class="sxs-lookup"><span data-stu-id="0307e-439">Similar code gets a reference to the *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="0307e-440">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span><span class="sxs-lookup"><span data-stu-id="0307e-440">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="0307e-441">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span><span class="sxs-lookup"><span data-stu-id="0307e-441">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="0307e-442">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span><span class="sxs-lookup"><span data-stu-id="0307e-442">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="0307e-443">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span><span class="sxs-lookup"><span data-stu-id="0307e-443">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="0307e-444">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span><span class="sxs-lookup"><span data-stu-id="0307e-444">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="0307e-445">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span><span class="sxs-lookup"><span data-stu-id="0307e-445">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

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

<span data-ttu-id="0307e-446">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform that back-end process that an image is ready for conversion to a thumbnail.</span><span class="sxs-lookup"><span data-stu-id="0307e-446">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform that back-end process that an image is ready for conversion to a thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="0307e-447">The code for the HttpPost `Edit` method is similar except that if the user selects a new image file any blobs that already exist must be deleted.</span><span class="sxs-lookup"><span data-stu-id="0307e-447">The code for the HttpPost `Edit` method is similar except that if the user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="0307e-448">The next example shows the code that deletes blobs when you delete an ad.</span><span class="sxs-lookup"><span data-stu-id="0307e-448">The next example shows the code that deletes blobs when you delete an ad.</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="0307e-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="0307e-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="0307e-450">The *Index.cshtml* file displays thumbnails with the other ad data.</span><span class="sxs-lookup"><span data-stu-id="0307e-450">The *Index.cshtml* file displays thumbnails with the other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="0307e-451">The *Details.cshtml* file displays the full-size image.</span><span class="sxs-lookup"><span data-stu-id="0307e-451">The *Details.cshtml* file displays the full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="0307e-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="0307e-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="0307e-453">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span><span class="sxs-lookup"><span data-stu-id="0307e-453">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="0307e-454">An `<input>` element tells the browser to provide a file selection dialog.</span><span class="sxs-lookup"><span data-stu-id="0307e-454">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="0307e-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span><span class="sxs-lookup"><span data-stu-id="0307e-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="0307e-456">The Azure worker role environment calls the `OnStart` method in the `WorkerRole` class when the worker role is getting started, and it calls the `Run` method when the `OnStart` method finishes.</span><span class="sxs-lookup"><span data-stu-id="0307e-456">The Azure worker role environment calls the `OnStart` method in the `WorkerRole` class when the worker role is getting started, and it calls the `Run` method when the `OnStart` method finishes.</span></span>

<span data-ttu-id="0307e-457">The `OnStart` method gets the database connection string from the *.cscfg* file and passes it to the Entity Framework DbContext class.</span><span class="sxs-lookup"><span data-stu-id="0307e-457">The `OnStart` method gets the database connection string from the *.cscfg* file and passes it to the Entity Framework DbContext class.</span></span> <span data-ttu-id="0307e-458">The SQLClient provider is used by default, so the provider does not have to be specified.</span><span class="sxs-lookup"><span data-stu-id="0307e-458">The SQLClient provider is used by default, so the provider does not have to be specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="0307e-459">After that, the method gets a reference to the storage account and creates the blob container and queue if they don't exist.</span><span class="sxs-lookup"><span data-stu-id="0307e-459">After that, the method gets a reference to the storage account and creates the blob container and queue if they don't exist.</span></span> <span data-ttu-id="0307e-460">The code for that is similar to what you already saw in the web role `Application_Start` method.</span><span class="sxs-lookup"><span data-stu-id="0307e-460">The code for that is similar to what you already saw in the web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="0307e-461">ContosoAdsWorker - WorkerRole.cs - Run method</span><span class="sxs-lookup"><span data-stu-id="0307e-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="0307e-462">The `Run` method is called when the `OnStart` method finishes its initialization work.</span><span class="sxs-lookup"><span data-stu-id="0307e-462">The `Run` method is called when the `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="0307e-463">The method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span><span class="sxs-lookup"><span data-stu-id="0307e-463">The method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

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

<span data-ttu-id="0307e-464">After each iteration of the loop, if no queue message was found, the program sleeps for a second.</span><span class="sxs-lookup"><span data-stu-id="0307e-464">After each iteration of the loop, if no queue message was found, the program sleeps for a second.</span></span> <span data-ttu-id="0307e-465">This prevents the worker role from incurring excessive CPU time and storage transaction costs.</span><span class="sxs-lookup"><span data-stu-id="0307e-465">This prevents the worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="0307e-466">The Microsoft Customer Advisory Team tells a story about a  developer who forgot to include this, deployed to production, and left for vacation.</span><span class="sxs-lookup"><span data-stu-id="0307e-466">The Microsoft Customer Advisory Team tells a story about a  developer who forgot to include this, deployed to production, and left for vacation.</span></span> <span data-ttu-id="0307e-467">When he got back, his oversight cost more than the vacation.</span><span class="sxs-lookup"><span data-stu-id="0307e-467">When he got back, his oversight cost more than the vacation.</span></span>

<span data-ttu-id="0307e-468">Sometimes the content of a queue message causes an error in processing.</span><span class="sxs-lookup"><span data-stu-id="0307e-468">Sometimes the content of a queue message causes an error in processing.</span></span> <span data-ttu-id="0307e-469">This is called a *poison message*, and if you just logged an error and restarted the loop, you could endlessly try to process that message.</span><span class="sxs-lookup"><span data-stu-id="0307e-469">This is called a *poison message*, and if you just logged an error and restarted the loop, you could endlessly try to process that message.</span></span>  <span data-ttu-id="0307e-470">Therefore the catch block includes an if statement that checks to see how many times the app has tried to process the current message, and if it has been more than 5 times, the message is deleted from the queue.</span><span class="sxs-lookup"><span data-stu-id="0307e-470">Therefore the catch block includes an if statement that checks to see how many times the app has tried to process the current message, and if it has been more than 5 times, the message is deleted from the queue.</span></span>

<span data-ttu-id="0307e-471">`ProcessQueueMessage` is called when a queue message is found.</span><span class="sxs-lookup"><span data-stu-id="0307e-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

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

<span data-ttu-id="0307e-472">This code reads the database to get the image URL, converts the image to a thumbnail, saves the thumbnail in a blob, updates the database with the thumbnail blob URL, and deletes the queue message.</span><span class="sxs-lookup"><span data-stu-id="0307e-472">This code reads the database to get the image URL, converts the image to a thumbnail, saves the thumbnail in a blob, updates the database with the thumbnail blob URL, and deletes the queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="0307e-473">The code in the `ConvertImageToThumbnailJPG` method uses classes in the System.Drawing namespace for simplicity.</span><span class="sxs-lookup"><span data-stu-id="0307e-473">The code in the `ConvertImageToThumbnailJPG` method uses classes in the System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="0307e-474">However, the classes in this namespace were designed for use with Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="0307e-474">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="0307e-475">They are not supported for use in a Windows or ASP.NET service.</span><span class="sxs-lookup"><span data-stu-id="0307e-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="0307e-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="0307e-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="0307e-477">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="0307e-477">Troubleshooting</span></span>
<span data-ttu-id="0307e-478">In case something doesn't work while you're following the instructions in this tutorial, here are some common errors and how to resolve them.</span><span class="sxs-lookup"><span data-stu-id="0307e-478">In case something doesn't work while you're following the instructions in this tutorial, here are some common errors and how to resolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="0307e-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="0307e-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="0307e-480">The `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using the Azure compute emulator.</span><span class="sxs-lookup"><span data-stu-id="0307e-480">The `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using the Azure compute emulator.</span></span>  <span data-ttu-id="0307e-481">If you get this error when you're running locally, make sure that you have set the ContosoAdsCloudService project as the startup project.</span><span class="sxs-lookup"><span data-stu-id="0307e-481">If you get this error when you're running locally, make sure that you have set the ContosoAdsCloudService project as the startup project.</span></span> <span data-ttu-id="0307e-482">This sets up the project to run using the Azure compute emulator.</span><span class="sxs-lookup"><span data-stu-id="0307e-482">This sets up the project to run using the Azure compute emulator.</span></span>

<span data-ttu-id="0307e-483">One of the things the application uses the Azure RoleEnvironment for is to get the connection string values that are stored in the *.cscfg* files, so another cause of this exception is a missing connection string.</span><span class="sxs-lookup"><span data-stu-id="0307e-483">One of the things the application uses the Azure RoleEnvironment for is to get the connection string values that are stored in the *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="0307e-484">Make sure that you created the StorageConnectionString setting for both Cloud and Local configurations in the ContosoAdsWeb project, and that you created both connection strings for both configurations in the ContosoAdsWorker project.</span><span class="sxs-lookup"><span data-stu-id="0307e-484">Make sure that you created the StorageConnectionString setting for both Cloud and Local configurations in the ContosoAdsWeb project, and that you created both connection strings for both configurations in the ContosoAdsWorker project.</span></span> <span data-ttu-id="0307e-485">If you do a **Find All** search for StorageConnectionString in the entire solution, you should see it 9 times in 6 files.</span><span class="sxs-lookup"><span data-stu-id="0307e-485">If you do a **Find All** search for StorageConnectionString in the entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-to-port-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="0307e-486">Cannot override to port xxx.</span><span class="sxs-lookup"><span data-stu-id="0307e-486">Cannot override to port xxx.</span></span> <span data-ttu-id="0307e-487">New port below minimum allowed value 8080 for protocol http</span><span class="sxs-lookup"><span data-stu-id="0307e-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="0307e-488">Try changing the port number used by the web project.</span><span class="sxs-lookup"><span data-stu-id="0307e-488">Try changing the port number used by the web project.</span></span> <span data-ttu-id="0307e-489">Right-click the ContosoAdsWeb project, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="0307e-489">Right-click the ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="0307e-490">Click the **Web** tab, and then change the port number in the **Project Url** setting.</span><span class="sxs-lookup"><span data-stu-id="0307e-490">Click the **Web** tab, and then change the port number in the **Project Url** setting.</span></span>

<span data-ttu-id="0307e-491">For another alternative that might resolve the problem, see the following  section.</span><span class="sxs-lookup"><span data-stu-id="0307e-491">For another alternative that might resolve the problem, see the following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="0307e-492">Other errors when running locally</span><span class="sxs-lookup"><span data-stu-id="0307e-492">Other errors when running locally</span></span>
<span data-ttu-id="0307e-493">By default new cloud service projects use the Azure compute emulator express to simulate the Azure environment.</span><span class="sxs-lookup"><span data-stu-id="0307e-493">By default new cloud service projects use the Azure compute emulator express to simulate the Azure environment.</span></span> <span data-ttu-id="0307e-494">This is a lightweight version of the full compute emulator, and under some conditions the full emulator will work when the express version does not.</span><span class="sxs-lookup"><span data-stu-id="0307e-494">This is a lightweight version of the full compute emulator, and under some conditions the full emulator will work when the express version does not.</span></span>  

<span data-ttu-id="0307e-495">To change the project to use the full emulator, right-click the ContosoAdsCloudService project, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="0307e-495">To change the project to use the full emulator, right-click the ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="0307e-496">In the **Properties** window click the **Web** tab, and then click the **Use Full Emulator** radio button.</span><span class="sxs-lookup"><span data-stu-id="0307e-496">In the **Properties** window click the **Web** tab, and then click the **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="0307e-497">In order to run the application with the full emulator, you have to open Visual Studio with administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="0307e-497">In order to run the application with the full emulator, you have to open Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0307e-498">Next steps</span><span class="sxs-lookup"><span data-stu-id="0307e-498">Next steps</span></span>
<span data-ttu-id="0307e-499">The Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span><span class="sxs-lookup"><span data-stu-id="0307e-499">The Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="0307e-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors, and so forth.</span><span class="sxs-lookup"><span data-stu-id="0307e-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors, and so forth.</span></span>

<span data-ttu-id="0307e-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex to more complex:</span><span class="sxs-lookup"><span data-stu-id="0307e-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex to more complex:</span></span>

* <span data-ttu-id="0307e-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span><span class="sxs-lookup"><span data-stu-id="0307e-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="0307e-503">Similar in concept to Contoso Ads but implements more features and more real-world coding practices.</span><span class="sxs-lookup"><span data-stu-id="0307e-503">Similar in concept to Contoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="0307e-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span><span class="sxs-lookup"><span data-stu-id="0307e-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="0307e-505">Introduces Azure Storage tables as well as blobs and queues.</span><span class="sxs-lookup"><span data-stu-id="0307e-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="0307e-506">Based on an older version of the Azure SDK for .NET, will require some modifications to work with the current version.</span><span class="sxs-lookup"><span data-stu-id="0307e-506">Based on an older version of the Azure SDK for .NET, will require some modifications to work with the current version.</span></span>

<span data-ttu-id="0307e-507">For general information about developing for the cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span><span class="sxs-lookup"><span data-stu-id="0307e-507">For general information about developing for the cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="0307e-508">For a video introduction to Azure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span><span class="sxs-lookup"><span data-stu-id="0307e-508">For a video introduction to Azure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="0307e-509">For more information, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="0307e-509">For more information, see the following resources:</span></span>

* [<span data-ttu-id="0307e-510">Azure Cloud Services Part 1: Introduction</span><span class="sxs-lookup"><span data-stu-id="0307e-510">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="0307e-511">How to manage Cloud Services</span><span class="sxs-lookup"><span data-stu-id="0307e-511">How to manage Cloud Services</span></span>](cloud-services-how-to-manage-portal.md)
* [<span data-ttu-id="0307e-512">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0307e-512">Azure Storage</span></span>](https://docs.microsoft.com/azure/storage/)
* [<span data-ttu-id="0307e-513">How to choose a cloud service provider</span><span class="sxs-lookup"><span data-stu-id="0307e-513">How to choose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
