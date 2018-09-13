---
title: Create a .NET WebJob in Azure App Service | Microsoft Docs
description: Create a multi-tier app using ASP.NET MVC and Azure. The front end runs in a web app in Azure App Service, and the backend runs as a WebJob. The app uses Entity Framework, SQL Database, and Azure storage queues and blobs.
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: glenga
ms.openlocfilehash: 8a05ffa86228d114b249ccfd22427021fd8301ca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564638"
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="3599c-105">Create a .NET WebJob in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3599c-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="3599c-106">This tutorial shows how to write code for a simple multi-tier ASP.NET MVC 5 application that uses the [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="3599c-106">This tutorial shows how to write code for a simple multi-tier ASP.NET MVC 5 application that uses the [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="3599c-107">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span><span class="sxs-lookup"><span data-stu-id="3599c-107">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="3599c-108">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span><span class="sxs-lookup"><span data-stu-id="3599c-108">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="3599c-109">In addition, it's designed to be extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="3599c-109">In addition, it's designed to be extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="3599c-110">The sample application is an advertising bulletin board.</span><span class="sxs-lookup"><span data-stu-id="3599c-110">The sample application is an advertising bulletin board.</span></span> <span data-ttu-id="3599c-111">Users can upload images for ads, and a backend process converts the images to thumbnails.</span><span class="sxs-lookup"><span data-stu-id="3599c-111">Users can upload images for ads, and a backend process converts the images to thumbnails.</span></span> <span data-ttu-id="3599c-112">The ad list page shows the thumbnails, and the ad details page shows the full size image.</span><span class="sxs-lookup"><span data-stu-id="3599c-112">The ad list page shows the thumbnails, and the ad details page shows the full size image.</span></span> <span data-ttu-id="3599c-113">Here's a screenshot:</span><span class="sxs-lookup"><span data-stu-id="3599c-113">Here's a screenshot:</span></span>

![Ad list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="3599c-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="3599c-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="3599c-116">The tutorial shows how to deploy the application to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="3599c-116">The tutorial shows how to deploy the application to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <a id="prerequisites"></a><span data-ttu-id="3599c-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3599c-117">Prerequisites</span></span>
<span data-ttu-id="3599c-118">The tutorial assumes that you know how to work with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3599c-118">The tutorial assumes that you know how to work with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="3599c-119">The tutorial was written for Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="3599c-119">The tutorial was written for Visual Studio 2013.</span></span> <span data-ttu-id="3599c-120">If you don't have Visual Studio already, it will be installed for you automatically when you install the Azure SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="3599c-120">If you don't have Visual Studio already, it will be installed for you automatically when you install the Azure SDK for .NET.</span></span>

<span data-ttu-id="3599c-121">The tutorial can be used with Visual Studio 2015, but before you run the application locally you have to change the `Data Source` part of the SQL Server LocalDB connection string in the Web.config and App.config files from `Data Source=(localdb)\v11.0` to `Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="3599c-121">The tutorial can be used with Visual Studio 2015, but before you run the application locally you have to change the `Data Source` part of the SQL Server LocalDB connection string in the Web.config and App.config files from `Data Source=(localdb)\v11.0` to `Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <a name="note"></a><span data-ttu-id="3599c-122">You need an Azure account to complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="3599c-122">You need an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="3599c-123">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span><span class="sxs-lookup"><span data-stu-id="3599c-123">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="3599c-124">Your credit card will never be charged, unless you explicitly change your settings and ask to be charged.</span><span class="sxs-lookup"><span data-stu-id="3599c-124">Your credit card will never be charged, unless you explicitly change your settings and ask to be charged.</span></span>
> * <span data-ttu-id="3599c-125">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span><span class="sxs-lookup"><span data-stu-id="3599c-125">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="3599c-126">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="3599c-126">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="3599c-127">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="3599c-127">No credit cards required; no commitments.</span></span>
>
>

## <a id="learn"></a><span data-ttu-id="3599c-128">What you'll learn</span><span class="sxs-lookup"><span data-stu-id="3599c-128">What you'll learn</span></span>
<span data-ttu-id="3599c-129">The tutorial shows how to do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="3599c-129">The tutorial shows how to do the following tasks:</span></span>

* <span data-ttu-id="3599c-130">Enable your machine for Azure development by installing the Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="3599c-130">Enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="3599c-131">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy the associated web project.</span><span class="sxs-lookup"><span data-stu-id="3599c-131">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy the associated web project.</span></span>
* <span data-ttu-id="3599c-132">Test a WebJobs SDK backend locally on the development computer.</span><span class="sxs-lookup"><span data-stu-id="3599c-132">Test a WebJobs SDK backend locally on the development computer.</span></span>
* <span data-ttu-id="3599c-133">Publish an application with a WebJobs backend to a web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="3599c-133">Publish an application with a WebJobs backend to a web app in App Service.</span></span>
* <span data-ttu-id="3599c-134">Upload files and store them in the Azure Blob service.</span><span class="sxs-lookup"><span data-stu-id="3599c-134">Upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="3599c-135">Use the Azure WebJobs SDK to work with Azure Storage queues and blobs.</span><span class="sxs-lookup"><span data-stu-id="3599c-135">Use the Azure WebJobs SDK to work with Azure Storage queues and blobs.</span></span>

## <a id="contosoads"></a><span data-ttu-id="3599c-136">Application architecture</span><span class="sxs-lookup"><span data-stu-id="3599c-136">Application architecture</span></span>
<span data-ttu-id="3599c-137">The sample application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a backend process.</span><span class="sxs-lookup"><span data-stu-id="3599c-137">The sample application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a backend process.</span></span>

<span data-ttu-id="3599c-138">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span><span class="sxs-lookup"><span data-stu-id="3599c-138">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="3599c-139">For each ad, the database stores two URLs: one for the full-size image and one for the thumbnail.</span><span class="sxs-lookup"><span data-stu-id="3599c-139">For each ad, the database stores two URLs: one for the full-size image and one for the thumbnail.</span></span>

![Ad table](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="3599c-141">When a user uploads an image, the web app stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span><span class="sxs-lookup"><span data-stu-id="3599c-141">When a user uploads an image, the web app stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="3599c-142">At the same time, it writes a message to an Azure queue.</span><span class="sxs-lookup"><span data-stu-id="3599c-142">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="3599c-143">In a backend process running as an Azure WebJob, the WebJobs SDK polls the queue for new messages.</span><span class="sxs-lookup"><span data-stu-id="3599c-143">In a backend process running as an Azure WebJob, the WebJobs SDK polls the queue for new messages.</span></span> <span data-ttu-id="3599c-144">When a new message appears, the WebJob creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span><span class="sxs-lookup"><span data-stu-id="3599c-144">When a new message appears, the WebJob creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="3599c-145">Here's a diagram that shows how the parts of the application interact:</span><span class="sxs-lookup"><span data-stu-id="3599c-145">Here's a diagram that shows how the parts of the application interact:</span></span>

![Contoso Ads architecture](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2015-2013.md)]

<span data-ttu-id="3599c-147">The tutorial instructions apply to Azure SDK for .NET 2.7.1 or later.</span><span class="sxs-lookup"><span data-stu-id="3599c-147">The tutorial instructions apply to Azure SDK for .NET 2.7.1 or later.</span></span>

## <a id="storage"></a><span data-ttu-id="3599c-148">Create an Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="3599c-148">Create an Azure Storage account</span></span>
<span data-ttu-id="3599c-149">An Azure storage account provides resources for storing queue and blob data in the cloud.</span><span class="sxs-lookup"><span data-stu-id="3599c-149">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span> <span data-ttu-id="3599c-150">It's also used by the WebJobs SDK to store logging data for the dashboard.</span><span class="sxs-lookup"><span data-stu-id="3599c-150">It's also used by the WebJobs SDK to store logging data for the dashboard.</span></span>

<span data-ttu-id="3599c-151">In a real-world application, you typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span><span class="sxs-lookup"><span data-stu-id="3599c-151">In a real-world application, you typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="3599c-152">For this tutorial you'll use just one account.</span><span class="sxs-lookup"><span data-stu-id="3599c-152">For this tutorial you'll use just one account.</span></span>

1. <span data-ttu-id="3599c-153">Open the **Server Explorer** window in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3599c-153">Open the **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="3599c-154">Right-click the **Azure** node, and then click **Connect to Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="3599c-154">Right-click the **Azure** node, and then click **Connect to Microsoft Azure**.</span></span>
   <span data-ttu-id="3599c-155">![Connect to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/connaz.png)</span><span class="sxs-lookup"><span data-stu-id="3599c-155">![Connect to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/connaz.png)</span></span>
3. <span data-ttu-id="3599c-156">Sign in using your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="3599c-156">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="3599c-157">Right-click **Storage** under the Azure node, and then click **Create Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="3599c-157">Right-click **Storage** under the Azure node, and then click **Create Storage Account**.</span></span>
   <span data-ttu-id="3599c-158">![Create Storage Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/createstor.png)</span><span class="sxs-lookup"><span data-stu-id="3599c-158">![Create Storage Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/createstor.png)</span></span>
5. <span data-ttu-id="3599c-159">In the **Create Storage Account** dialog, enter a name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="3599c-159">In the **Create Storage Account** dialog, enter a name for the storage account.</span></span>

    <span data-ttu-id="3599c-160">The name must be must be unique (no other Azure storage account can have the same name).</span><span class="sxs-lookup"><span data-stu-id="3599c-160">The name must be must be unique (no other Azure storage account can have the same name).</span></span> <span data-ttu-id="3599c-161">If the name you enter is already in use you'll get a chance to change it.</span><span class="sxs-lookup"><span data-stu-id="3599c-161">If the name you enter is already in use you'll get a chance to change it.</span></span>

    <span data-ttu-id="3599c-162">The URL to access your storage account will be *{name}*.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="3599c-162">The URL to access your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="3599c-163">Set the **Region or Affinity Group** drop-down list to the region closest to you.</span><span class="sxs-lookup"><span data-stu-id="3599c-163">Set the **Region or Affinity Group** drop-down list to the region closest to you.</span></span>

    <span data-ttu-id="3599c-164">This setting specifies which Azure datacenter will host your storage account.</span><span class="sxs-lookup"><span data-stu-id="3599c-164">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="3599c-165">For this tutorial, your choice won't make a noticeable difference.</span><span class="sxs-lookup"><span data-stu-id="3599c-165">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="3599c-166">However, for a production web app, you want your web server and your storage account to be in the same region to minimize latency and data egress charges.</span><span class="sxs-lookup"><span data-stu-id="3599c-166">However, for a production web app, you want your web server and your storage account to be in the same region to minimize latency and data egress charges.</span></span> <span data-ttu-id="3599c-167">The web app (which you'll create later) datacenter should be as close as possible to the browsers accessing the web app in order to minimize latency.</span><span class="sxs-lookup"><span data-stu-id="3599c-167">The web app (which you'll create later) datacenter should be as close as possible to the browsers accessing the web app in order to minimize latency.</span></span>
7. <span data-ttu-id="3599c-168">Set the **Replication** drop-down list to **Locally redundant**.</span><span class="sxs-lookup"><span data-stu-id="3599c-168">Set the **Replication** drop-down list to **Locally redundant**.</span></span>

    <span data-ttu-id="3599c-169">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span><span class="sxs-lookup"><span data-stu-id="3599c-169">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span></span> <span data-ttu-id="3599c-170">Geo-replication can incur additional costs.</span><span class="sxs-lookup"><span data-stu-id="3599c-170">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="3599c-171">For test and development accounts, you generally don't want to pay for geo-replication.</span><span class="sxs-lookup"><span data-stu-id="3599c-171">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="3599c-172">For more information, see [Create, manage, or delete a storage account](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="3599c-172">For more information, see [Create, manage, or delete a storage account](../storage/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="3599c-173">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3599c-173">Click **Create**.</span></span>

    ![New storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <a id="download"></a><span data-ttu-id="3599c-175">Download the application</span><span class="sxs-lookup"><span data-stu-id="3599c-175">Download the application</span></span>
1. <span data-ttu-id="3599c-176">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span><span class="sxs-lookup"><span data-stu-id="3599c-176">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="3599c-177">Start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3599c-177">Start Visual Studio.</span></span>
3. <span data-ttu-id="3599c-178">From the **File** menu choose **Open > Project/Solution**, navigate to where you downloaded the solution, and then open the solution file.</span><span class="sxs-lookup"><span data-stu-id="3599c-178">From the **File** menu choose **Open > Project/Solution**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="3599c-179">Press CTRL+SHIFT+B to build the solution.</span><span class="sxs-lookup"><span data-stu-id="3599c-179">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="3599c-180">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span><span class="sxs-lookup"><span data-stu-id="3599c-180">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="3599c-181">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog and clicking the **Restore** button at the top right.</span><span class="sxs-lookup"><span data-stu-id="3599c-181">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="3599c-182">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as the startup project.</span><span class="sxs-lookup"><span data-stu-id="3599c-182">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as the startup project.</span></span>

## <a id="configurestorage"></a><span data-ttu-id="3599c-183">Configure the application to use your storage account</span><span class="sxs-lookup"><span data-stu-id="3599c-183">Configure the application to use your storage account</span></span>
1. <span data-ttu-id="3599c-184">Open the application *Web.config* file in the ContosoAdsWeb project.</span><span class="sxs-lookup"><span data-stu-id="3599c-184">Open the application *Web.config* file in the ContosoAdsWeb project.</span></span>

    <span data-ttu-id="3599c-185">The file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span><span class="sxs-lookup"><span data-stu-id="3599c-185">The file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="3599c-186">The SQL connection string points to a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span><span class="sxs-lookup"><span data-stu-id="3599c-186">The SQL connection string points to a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="3599c-187">The storage connection string is an example that has placeholders for the storage account name and access key.</span><span class="sxs-lookup"><span data-stu-id="3599c-187">The storage connection string is an example that has placeholders for the storage account name and access key.</span></span> <span data-ttu-id="3599c-188">You'll replace this with a connection string that has the name and key of your storage account.</span><span class="sxs-lookup"><span data-stu-id="3599c-188">You'll replace this with a connection string that has the name and key of your storage account.</span></span>  

    <pre class="prettyprint">&lt;connectionStrings&gt;
      &lt;add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" /&gt;
      &lt;add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=<mark>[accountname]</mark>;AccountKey=<mark>[accesskey]</mark>"/&gt;
    &lt;/connectionStrings&gt;</pre>

    <span data-ttu-id="3599c-189">The storage connection string is named AzureWebJobsStorage because that's the name the WebJobs SDK uses by default.</span><span class="sxs-lookup"><span data-stu-id="3599c-189">The storage connection string is named AzureWebJobsStorage because that's the name the WebJobs SDK uses by default.</span></span> <span data-ttu-id="3599c-190">The same name is used here so you have to set only one connection string value in the Azure environment.</span><span class="sxs-lookup"><span data-stu-id="3599c-190">The same name is used here so you have to set only one connection string value in the Azure environment.</span></span>
2. <span data-ttu-id="3599c-191">In **Server Explorer**, right-click your storage account under the **Storage** node, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="3599c-191">In **Server Explorer**, right-click your storage account under the **Storage** node, and then click **Properties**.</span></span>

    ![Click Storage Account Properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="3599c-193">In the **Properties** window, click **Storage Account Keys**, and then click the ellipsis.</span><span class="sxs-lookup"><span data-stu-id="3599c-193">In the **Properties** window, click **Storage Account Keys**, and then click the ellipsis.</span></span>

    ![New storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)
4. <span data-ttu-id="3599c-195">Copy the **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="3599c-195">Copy the **Connection String**.</span></span>

    ![Storage Account Keys dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="3599c-197">Replace the storage connection string in the *Web.config* file with the connection string you just copied.</span><span class="sxs-lookup"><span data-stu-id="3599c-197">Replace the storage connection string in the *Web.config* file with the connection string you just copied.</span></span> <span data-ttu-id="3599c-198">Make sure you select everything inside the quotation marks but not including the quotation marks before pasting.</span><span class="sxs-lookup"><span data-stu-id="3599c-198">Make sure you select everything inside the quotation marks but not including the quotation marks before pasting.</span></span>
6. <span data-ttu-id="3599c-199">Open the *App.config* file in the ContosoAdsWebJob project.</span><span class="sxs-lookup"><span data-stu-id="3599c-199">Open the *App.config* file in the ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="3599c-200">This file has two storage connection strings, one for application data and one for logging.</span><span class="sxs-lookup"><span data-stu-id="3599c-200">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="3599c-201">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="3599c-201">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="3599c-202">For this tutorial you'll use a single storage account.</span><span class="sxs-lookup"><span data-stu-id="3599c-202">For this tutorial you'll use a single storage account.</span></span> <span data-ttu-id="3599c-203">The connection strings have placeholders for the storage account keys.</span><span class="sxs-lookup"><span data-stu-id="3599c-203">The connection strings have placeholders for the storage account keys.</span></span>

      <pre class="prettyprint">&lt;configuration&gt;
    &lt;connectionStrings&gt;
        &lt;add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=<mark>[accountname]</mark>;AccountKey=<mark>[accesskey]</mark>"/&gt;
        &lt;add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=<mark>[accountname]</mark>;AccountKey=<mark>[accesskey]</mark>"/&gt;
        &lt;add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/&gt;
    &lt;/connectionStrings&gt;
        &lt;startup&gt;
            &lt;supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" /&gt;
    &lt;/startup&gt;
   &lt;/configuration&gt;</pre>

    <span data-ttu-id="3599c-204">By default, the WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="3599c-204">By default, the WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="3599c-205">As an alternative, you can [store the connection string however you want and pass it in explicitly to the `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="3599c-205">As an alternative, you can [store the connection string however you want and pass it in explicitly to the `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="3599c-206">Replace both storage connection strings with the connection string you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="3599c-206">Replace both storage connection strings with the connection string you copied earlier.</span></span>
8. <span data-ttu-id="3599c-207">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="3599c-207">Save your changes.</span></span>

## <a id="run"></a><span data-ttu-id="3599c-208">Run the application locally</span><span class="sxs-lookup"><span data-stu-id="3599c-208">Run the application locally</span></span>
1. <span data-ttu-id="3599c-209">To start the web frontend of the application, press CTRL+F5.</span><span class="sxs-lookup"><span data-stu-id="3599c-209">To start the web frontend of the application, press CTRL+F5.</span></span>

    <span data-ttu-id="3599c-210">The default browser opens to the home page.</span><span class="sxs-lookup"><span data-stu-id="3599c-210">The default browser opens to the home page.</span></span> <span data-ttu-id="3599c-211">(The web project runs because you've made it the startup project.)</span><span class="sxs-lookup"><span data-stu-id="3599c-211">(The web project runs because you've made it the startup project.)</span></span>

    ![Contoso Ads home page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="3599c-213">To start the WebJob backend of the application, right-click the ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span><span class="sxs-lookup"><span data-stu-id="3599c-213">To start the WebJob backend of the application, right-click the ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="3599c-214">A console application window opens and displays logging messages indicating the WebJobs SDK JobHost object has started to run.</span><span class="sxs-lookup"><span data-stu-id="3599c-214">A console application window opens and displays logging messages indicating the WebJobs SDK JobHost object has started to run.</span></span>

    ![Console application window showing that the backend is running](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="3599c-216">In your browser, click  **Create an Ad**.</span><span class="sxs-lookup"><span data-stu-id="3599c-216">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="3599c-217">Enter some test data and select an image to upload, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3599c-217">Enter some test data and select an image to upload, and then click **Create**.</span></span>

    ![Create page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="3599c-219">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span><span class="sxs-lookup"><span data-stu-id="3599c-219">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="3599c-220">Meanwhile, after a short wait a logging message in the console application window shows that a queue message was received and has been processed.</span><span class="sxs-lookup"><span data-stu-id="3599c-220">Meanwhile, after a short wait a logging message in the console application window shows that a queue message was received and has been processed.</span></span>

    ![Console application window showing that a queue message has been processed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="3599c-222">After you see the logging messages in the console application window, refresh the Index page to see the thumbnail.</span><span class="sxs-lookup"><span data-stu-id="3599c-222">After you see the logging messages in the console application window, refresh the Index page to see the thumbnail.</span></span>

    ![Index page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="3599c-224">Click **Details** for your ad to see the full-size image.</span><span class="sxs-lookup"><span data-stu-id="3599c-224">Click **Details** for your ad to see the full-size image.</span></span>

    ![Details page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="3599c-226">You've been running the application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in the cloud.</span><span class="sxs-lookup"><span data-stu-id="3599c-226">You've been running the application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in the cloud.</span></span> <span data-ttu-id="3599c-227">In the following section you'll run the application in the cloud, using a cloud database as well as cloud blobs and queues.</span><span class="sxs-lookup"><span data-stu-id="3599c-227">In the following section you'll run the application in the cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <a id="runincloud"></a><span data-ttu-id="3599c-228">Run the application in the cloud</span><span class="sxs-lookup"><span data-stu-id="3599c-228">Run the application in the cloud</span></span>
<span data-ttu-id="3599c-229">You'll do the following steps to run the application in the cloud:</span><span class="sxs-lookup"><span data-stu-id="3599c-229">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="3599c-230">Deploy to Web Apps.</span><span class="sxs-lookup"><span data-stu-id="3599c-230">Deploy to Web Apps.</span></span> <span data-ttu-id="3599c-231">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span><span class="sxs-lookup"><span data-stu-id="3599c-231">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="3599c-232">Configure the web app to use your Azure SQL database and storage account.</span><span class="sxs-lookup"><span data-stu-id="3599c-232">Configure the web app to use your Azure SQL database and storage account.</span></span>

<span data-ttu-id="3599c-233">After you've created some ads while running in the cloud, you'll view the WebJobs SDK dashboard to see the rich monitoring features it has to offer.</span><span class="sxs-lookup"><span data-stu-id="3599c-233">After you've created some ads while running in the cloud, you'll view the WebJobs SDK dashboard to see the rich monitoring features it has to offer.</span></span>

### <a name="deploy-to-web-apps"></a><span data-ttu-id="3599c-234">Deploy to Web Apps</span><span class="sxs-lookup"><span data-stu-id="3599c-234">Deploy to Web Apps</span></span>
1. <span data-ttu-id="3599c-235">Close the browser and the console application window.</span><span class="sxs-lookup"><span data-stu-id="3599c-235">Close the browser and the console application window.</span></span>
2. <span data-ttu-id="3599c-236">In **Solution Explorer**, right-click the ContosoAdsWeb project, and then click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="3599c-236">In **Solution Explorer**, right-click the ContosoAdsWeb project, and then click **Publish**.</span></span>
3. <span data-ttu-id="3599c-237">In the **Profile** step of the **Publish Web** wizard, click **Microsoft Azure web apps**.</span><span class="sxs-lookup"><span data-stu-id="3599c-237">In the **Profile** step of the **Publish Web** wizard, click **Microsoft Azure web apps**.</span></span>

    ![Select Azure web app publish target](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/pubweb.png)
4. <span data-ttu-id="3599c-239">Sign in to Azure if you aren't still signed in.</span><span class="sxs-lookup"><span data-stu-id="3599c-239">Sign in to Azure if you aren't still signed in.</span></span>
5. <span data-ttu-id="3599c-240">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="3599c-240">Click **New**.</span></span>

    <span data-ttu-id="3599c-241">The dialog box may look slightly different depending on which version of the Azure SDK for .NET you have installed.</span><span class="sxs-lookup"><span data-stu-id="3599c-241">The dialog box may look slightly different depending on which version of the Azure SDK for .NET you have installed.</span></span>

    ![Click New](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/clicknew.png)
6. <span data-ttu-id="3599c-243">In the **Create web app on Microsoft Azure** dialog box, enter a unique name in the **Web app name** box.</span><span class="sxs-lookup"><span data-stu-id="3599c-243">In the **Create web app on Microsoft Azure** dialog box, enter a unique name in the **Web app name** box.</span></span>

    <span data-ttu-id="3599c-244">The complete URL will consist of what you enter here plus .azurewebsites.net (as shown next to the **Web app name** text box).</span><span class="sxs-lookup"><span data-stu-id="3599c-244">The complete URL will consist of what you enter here plus .azurewebsites.net (as shown next to the **Web app name** text box).</span></span> <span data-ttu-id="3599c-245">For example, if the web app name is ContosoAds, the URL will be ContosoAds.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="3599c-245">For example, if the web app name is ContosoAds, the URL will be ContosoAds.azurewebsites.net.</span></span>
7. <span data-ttu-id="3599c-246">In the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) drop-down list choose **Create new App Service plan**.</span><span class="sxs-lookup"><span data-stu-id="3599c-246">In the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) drop-down list choose **Create new App Service plan**.</span></span> <span data-ttu-id="3599c-247">Enter a name for the App Service plan, such as ContosoAdsPlan.</span><span class="sxs-lookup"><span data-stu-id="3599c-247">Enter a name for the App Service plan, such as ContosoAdsPlan.</span></span>
8. <span data-ttu-id="3599c-248">In the [Resource group](../azure-resource-manager/resource-group-overview.md) drop-down list choose **Create new resource group**.</span><span class="sxs-lookup"><span data-stu-id="3599c-248">In the [Resource group](../azure-resource-manager/resource-group-overview.md) drop-down list choose **Create new resource group**.</span></span>
9. <span data-ttu-id="3599c-249">Enter a name for the resource group, such as ContosoAdsGroup.</span><span class="sxs-lookup"><span data-stu-id="3599c-249">Enter a name for the resource group, such as ContosoAdsGroup.</span></span>
10. <span data-ttu-id="3599c-250">In the **Region** drop-down list, choose the same region you chose for your storage account.</span><span class="sxs-lookup"><span data-stu-id="3599c-250">In the **Region** drop-down list, choose the same region you chose for your storage account.</span></span>

    <span data-ttu-id="3599c-251">This setting specifies which Azure datacenter your web app will run in.</span><span class="sxs-lookup"><span data-stu-id="3599c-251">This setting specifies which Azure datacenter your web app will run in.</span></span> <span data-ttu-id="3599c-252">Keeping the web app and storage account in the same datacenter minimizes latency and data egress charges.</span><span class="sxs-lookup"><span data-stu-id="3599c-252">Keeping the web app and storage account in the same datacenter minimizes latency and data egress charges.</span></span>
11. <span data-ttu-id="3599c-253">In the **Database server** drop-down list choose **Create new server**.</span><span class="sxs-lookup"><span data-stu-id="3599c-253">In the **Database server** drop-down list choose **Create new server**.</span></span>
12. <span data-ttu-id="3599c-254">Enter a name for the database server, such as contosoadsserver + a number or your name to make the server name unique.</span><span class="sxs-lookup"><span data-stu-id="3599c-254">Enter a name for the database server, such as contosoadsserver + a number or your name to make the server name unique.</span></span>

    <span data-ttu-id="3599c-255">The server name must be unique.</span><span class="sxs-lookup"><span data-stu-id="3599c-255">The server name must be unique.</span></span> <span data-ttu-id="3599c-256">It can contain lower-case letters, numeric digits, and hyphens.</span><span class="sxs-lookup"><span data-stu-id="3599c-256">It can contain lower-case letters, numeric digits, and hyphens.</span></span> <span data-ttu-id="3599c-257">It cannot contain a trailing hyphen.</span><span class="sxs-lookup"><span data-stu-id="3599c-257">It cannot contain a trailing hyphen.</span></span>

    <span data-ttu-id="3599c-258">Alternatively, if your subscription already has a server, you can select that server from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="3599c-258">Alternatively, if your subscription already has a server, you can select that server from the drop-down list.</span></span>
13. <span data-ttu-id="3599c-259">Enter an administrator **Database username** and **Database password**.</span><span class="sxs-lookup"><span data-stu-id="3599c-259">Enter an administrator **Database username** and **Database password**.</span></span>

    <span data-ttu-id="3599c-260">If you selected **New SQL Database server** you aren't entering an existing name and password here, you're entering a new name and password that you're defining now to use later when you access the database.</span><span class="sxs-lookup"><span data-stu-id="3599c-260">If you selected **New SQL Database server** you aren't entering an existing name and password here, you're entering a new name and password that you're defining now to use later when you access the database.</span></span> <span data-ttu-id="3599c-261">If you selected a server that you created previously, you'll be prompted for the password to the administrative user account you already created.</span><span class="sxs-lookup"><span data-stu-id="3599c-261">If you selected a server that you created previously, you'll be prompted for the password to the administrative user account you already created.</span></span>
14. <span data-ttu-id="3599c-262">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3599c-262">Click **Create**.</span></span>

    ![Create web app on Microsoft Azure dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/newdb.png)

    <span data-ttu-id="3599c-264">Visual Studio creates the solution, the web project, the web app in Azure, and the Azure SQL Database instance.</span><span class="sxs-lookup"><span data-stu-id="3599c-264">Visual Studio creates the solution, the web project, the web app in Azure, and the Azure SQL Database instance.</span></span>
15. <span data-ttu-id="3599c-265">In the **Connection** step of the **Publish Web** wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3599c-265">In the **Connection** step of the **Publish Web** wizard, click **Next**.</span></span>

    ![Connection step](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/connstep.png)
16. <span data-ttu-id="3599c-267">In the **Settings** step, clear the **Use this connection string at runtime** check box, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3599c-267">In the **Settings** step, clear the **Use this connection string at runtime** check box, and then click **Next**.</span></span>

    ![Settings step](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/settingsstep.png)

    <span data-ttu-id="3599c-269">You don't need to use the publish dialog to set the SQL connection string because you'll set that value in the Azure environment later.</span><span class="sxs-lookup"><span data-stu-id="3599c-269">You don't need to use the publish dialog to set the SQL connection string because you'll set that value in the Azure environment later.</span></span>

    <span data-ttu-id="3599c-270">You can ignore the warnings on this page.</span><span class="sxs-lookup"><span data-stu-id="3599c-270">You can ignore the warnings on this page.</span></span>

    * <span data-ttu-id="3599c-271">Normally the storage account you use when running in Azure would be different from the one you use when running locally, but for this tutorial you're using the same one in both environments.</span><span class="sxs-lookup"><span data-stu-id="3599c-271">Normally the storage account you use when running in Azure would be different from the one you use when running locally, but for this tutorial you're using the same one in both environments.</span></span> <span data-ttu-id="3599c-272">So the AzureWebJobsStorage connection string does not need to be transformed.</span><span class="sxs-lookup"><span data-stu-id="3599c-272">So the AzureWebJobsStorage connection string does not need to be transformed.</span></span> <span data-ttu-id="3599c-273">Even if you did want to use a different storage account in the cloud, you wouldn't need to transform the connection string because the app uses an Azure environment setting when it runs in Azure.</span><span class="sxs-lookup"><span data-stu-id="3599c-273">Even if you did want to use a different storage account in the cloud, you wouldn't need to transform the connection string because the app uses an Azure environment setting when it runs in Azure.</span></span> <span data-ttu-id="3599c-274">You'll see this later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="3599c-274">You'll see this later in the tutorial.</span></span>
    * <span data-ttu-id="3599c-275">For this tutorial you aren't going to be making changes to the data model used for the ContosoAdsContext database, so there is no need to use Entity Framework Code First Migrations for deployment.</span><span class="sxs-lookup"><span data-stu-id="3599c-275">For this tutorial you aren't going to be making changes to the data model used for the ContosoAdsContext database, so there is no need to use Entity Framework Code First Migrations for deployment.</span></span> <span data-ttu-id="3599c-276">Code First automatically creates a new database the first time the app tries to access SQL data.</span><span class="sxs-lookup"><span data-stu-id="3599c-276">Code First automatically creates a new database the first time the app tries to access SQL data.</span></span>

    <span data-ttu-id="3599c-277">For this tutorial, the default values of the options under **File Publish Options** are fine.</span><span class="sxs-lookup"><span data-stu-id="3599c-277">For this tutorial, the default values of the options under **File Publish Options** are fine.</span></span>
17. <span data-ttu-id="3599c-278">In the **Preview** step, click **Start Preview**.</span><span class="sxs-lookup"><span data-stu-id="3599c-278">In the **Preview** step, click **Start Preview**.</span></span>

    ![Click Start Preview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/previewstep.png)

    <span data-ttu-id="3599c-280">You can ignore the warning about no databases being published.</span><span class="sxs-lookup"><span data-stu-id="3599c-280">You can ignore the warning about no databases being published.</span></span> <span data-ttu-id="3599c-281">Entity Framework Code First creates the database; it doesn't need to be published.</span><span class="sxs-lookup"><span data-stu-id="3599c-281">Entity Framework Code First creates the database; it doesn't need to be published.</span></span>

    <span data-ttu-id="3599c-282">The preview window shows that binaries and configuration files from the WebJob project will be copied to the *app_data\jobs\continuous* folder of the web app.</span><span class="sxs-lookup"><span data-stu-id="3599c-282">The preview window shows that binaries and configuration files from the WebJob project will be copied to the *app_data\jobs\continuous* folder of the web app.</span></span>

    ![WebJobs files in preview window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/previewwjfiles.png)
18. <span data-ttu-id="3599c-284">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="3599c-284">Click **Publish**.</span></span>

    <span data-ttu-id="3599c-285">Visual Studio deploys the application and opens the home page URL in the browser.</span><span class="sxs-lookup"><span data-stu-id="3599c-285">Visual Studio deploys the application and opens the home page URL in the browser.</span></span>

    <span data-ttu-id="3599c-286">You won't be able to use the web app until you set connection strings in the Azure environment in the next section.</span><span class="sxs-lookup"><span data-stu-id="3599c-286">You won't be able to use the web app until you set connection strings in the Azure environment in the next section.</span></span> <span data-ttu-id="3599c-287">You'll see either an error page or the home page depending on web app and database creation options you chose earlier.</span><span class="sxs-lookup"><span data-stu-id="3599c-287">You'll see either an error page or the home page depending on web app and database creation options you chose earlier.</span></span>

### <a name="configure-the-web-app-to-use-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="3599c-288">Configure the web app to use your Azure SQL database and storage account.</span><span class="sxs-lookup"><span data-stu-id="3599c-288">Configure the web app to use your Azure SQL database and storage account.</span></span>
<span data-ttu-id="3599c-289">It's a security best practice to [avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="3599c-289">It's a security best practice to [avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="3599c-290">Azure provides a way to do that: you can set connection string and other setting values in the Azure environment, and ASP.NET configuration APIs automatically pick up these values when the app runs in Azure.</span><span class="sxs-lookup"><span data-stu-id="3599c-290">Azure provides a way to do that: you can set connection string and other setting values in the Azure environment, and ASP.NET configuration APIs automatically pick up these values when the app runs in Azure.</span></span> <span data-ttu-id="3599c-291">You can set these values in Azure by using **Server Explorer**, the Azure Portal, Windows PowerShell, or the cross-platform command-line interface.</span><span class="sxs-lookup"><span data-stu-id="3599c-291">You can set these values in Azure by using **Server Explorer**, the Azure Portal, Windows PowerShell, or the cross-platform command-line interface.</span></span> <span data-ttu-id="3599c-292">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="3599c-292">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="3599c-293">In this section you use **Server Explorer** to set connection string values in Azure.</span><span class="sxs-lookup"><span data-stu-id="3599c-293">In this section you use **Server Explorer** to set connection string values in Azure.</span></span>

1. <span data-ttu-id="3599c-294">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span><span class="sxs-lookup"><span data-stu-id="3599c-294">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="3599c-295">The **Azure Web App** window opens on the **Configuration** tab.</span><span class="sxs-lookup"><span data-stu-id="3599c-295">The **Azure Web App** window opens on the **Configuration** tab.</span></span>
2. <span data-ttu-id="3599c-296">Change the name of the DefaultConnection connection string to ContosoAdsContext.</span><span class="sxs-lookup"><span data-stu-id="3599c-296">Change the name of the DefaultConnection connection string to ContosoAdsContext.</span></span>

    <span data-ttu-id="3599c-297">Azure automatically created this connection string when you created the web app with an associated database, so it already has the right connection string value.</span><span class="sxs-lookup"><span data-stu-id="3599c-297">Azure automatically created this connection string when you created the web app with an associated database, so it already has the right connection string value.</span></span> <span data-ttu-id="3599c-298">You're changing just the name to what your code is looking for.</span><span class="sxs-lookup"><span data-stu-id="3599c-298">You're changing just the name to what your code is looking for.</span></span>
3. <span data-ttu-id="3599c-299">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="3599c-299">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="3599c-300">Set type to Custom, and set the connection string value to the same value that you used earlier for the *Web.config* and *App.config* files.</span><span class="sxs-lookup"><span data-stu-id="3599c-300">Set type to Custom, and set the connection string value to the same value that you used earlier for the *Web.config* and *App.config* files.</span></span> <span data-ttu-id="3599c-301">(Make sure you include the entire connection string, not just the access key, and don't include the quotation marks.)</span><span class="sxs-lookup"><span data-stu-id="3599c-301">(Make sure you include the entire connection string, not just the access key, and don't include the quotation marks.)</span></span>

    <span data-ttu-id="3599c-302">These connection strings are used by the WebJobs SDK, one for application data and one for logging.</span><span class="sxs-lookup"><span data-stu-id="3599c-302">These connection strings are used by the WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="3599c-303">As you saw earlier, the one for application data is also used by the web front end code.</span><span class="sxs-lookup"><span data-stu-id="3599c-303">As you saw earlier, the one for application data is also used by the web front end code.</span></span>
4. <span data-ttu-id="3599c-304">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3599c-304">Click **Save**.</span></span>

    ![Connection strings in Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="3599c-306">In **Server Explorer**, right-click the web app, and then click **Stop**.</span><span class="sxs-lookup"><span data-stu-id="3599c-306">In **Server Explorer**, right-click the web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="3599c-307">After the web app stops, right-click the web app again, and then click **Start**.</span><span class="sxs-lookup"><span data-stu-id="3599c-307">After the web app stops, right-click the web app again, and then click **Start**.</span></span>

   <span data-ttu-id="3599c-308">The WebJob automatically starts when you publish, but it stops when you make a configuration change.</span><span class="sxs-lookup"><span data-stu-id="3599c-308">The WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="3599c-309">To restart it you can either restart the web app or restart the WebJob in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="3599c-309">To restart it you can either restart the web app or restart the WebJob in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="3599c-310">It's generally recommended to restart the web app after a configuration change.</span><span class="sxs-lookup"><span data-stu-id="3599c-310">It's generally recommended to restart the web app after a configuration change.</span></span>
7. <span data-ttu-id="3599c-311">Refresh the browser window that has the web app URL in its address bar.</span><span class="sxs-lookup"><span data-stu-id="3599c-311">Refresh the browser window that has the web app URL in its address bar.</span></span>

    <span data-ttu-id="3599c-312">The home page appears.</span><span class="sxs-lookup"><span data-stu-id="3599c-312">The home page appears.</span></span>
8. <span data-ttu-id="3599c-313">Create an ad, as you did when you ran the application locally.</span><span class="sxs-lookup"><span data-stu-id="3599c-313">Create an ad, as you did when you ran the application locally.</span></span>

   <span data-ttu-id="3599c-314">The Index page shows without a thumbnail at first.</span><span class="sxs-lookup"><span data-stu-id="3599c-314">The Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="3599c-315">Refresh the page after a few seconds, and the thumbnail appears.</span><span class="sxs-lookup"><span data-stu-id="3599c-315">Refresh the page after a few seconds, and the thumbnail appears.</span></span>

   <span data-ttu-id="3599c-316">If the thumbnail doesn't appear, you may have to wait a minute or so for the WebJob to restart.</span><span class="sxs-lookup"><span data-stu-id="3599c-316">If the thumbnail doesn't appear, you may have to wait a minute or so for the WebJob to restart.</span></span> <span data-ttu-id="3599c-317">If after a a while you still don't see the thumbnail when you refresh the page, the WebJob may not have started automatically.</span><span class="sxs-lookup"><span data-stu-id="3599c-317">If after a a while you still don't see the thumbnail when you refresh the page, the WebJob may not have started automatically.</span></span> <span data-ttu-id="3599c-318">In that case, go to the WebJobs tab in the [classic portal](https://manage.windowsazure.com) page for your web app, and then click **Start**.</span><span class="sxs-lookup"><span data-stu-id="3599c-318">In that case, go to the WebJobs tab in the [classic portal](https://manage.windowsazure.com) page for your web app, and then click **Start**.</span></span>

### <a name="view-the-webjobs-sdk-dashboard"></a><span data-ttu-id="3599c-319">View the WebJobs SDK dashboard</span><span class="sxs-lookup"><span data-stu-id="3599c-319">View the WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="3599c-320">In the [classic portal](https://manage.windowsazure.com), select your web app.</span><span class="sxs-lookup"><span data-stu-id="3599c-320">In the [classic portal](https://manage.windowsazure.com), select your web app.</span></span>
2. <span data-ttu-id="3599c-321">Click the **WebJobs** tab.</span><span class="sxs-lookup"><span data-stu-id="3599c-321">Click the **WebJobs** tab.</span></span>
3. <span data-ttu-id="3599c-322">Click the URL in the Logs column for your WebJob.</span><span class="sxs-lookup"><span data-stu-id="3599c-322">Click the URL in the Logs column for your WebJob.</span></span>

    ![WebJobs tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/wjtab.png)

    <span data-ttu-id="3599c-324">A new browser tab opens to the WebJobs SDK dashboard.</span><span class="sxs-lookup"><span data-stu-id="3599c-324">A new browser tab opens to the WebJobs SDK dashboard.</span></span> <span data-ttu-id="3599c-325">The dashboard shows that the WebJob is running and shows a list of functions in your code that the WebJobs SDK triggered.</span><span class="sxs-lookup"><span data-stu-id="3599c-325">The dashboard shows that the WebJob is running and shows a list of functions in your code that the WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="3599c-326">Click one of the functions to see details about its execution.</span><span class="sxs-lookup"><span data-stu-id="3599c-326">Click one of the functions to see details about its execution.</span></span>

    ![WebJobs SDK dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJobs SDK dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="3599c-329">The **Replay Function** button on this page causes the WebJobs SDK framework to call the function again, and it gives you a chance to change the data passed to the function first.</span><span class="sxs-lookup"><span data-stu-id="3599c-329">The **Replay Function** button on this page causes the WebJobs SDK framework to call the function again, and it gives you a chance to change the data passed to the function first.</span></span>

> [!NOTE]
> <span data-ttu-id="3599c-330">When you're finished testing, delete the web app and the SQL Database instance.</span><span class="sxs-lookup"><span data-stu-id="3599c-330">When you're finished testing, delete the web app and the SQL Database instance.</span></span> <span data-ttu-id="3599c-331">The web app is free, but the SQL Database instance and storage account accrue charges (minimal due to small size).</span><span class="sxs-lookup"><span data-stu-id="3599c-331">The web app is free, but the SQL Database instance and storage account accrue charges (minimal due to small size).</span></span> <span data-ttu-id="3599c-332">Also, if you leave the web app running, anyone who finds your URL can create and view ads.</span><span class="sxs-lookup"><span data-stu-id="3599c-332">Also, if you leave the web app running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="3599c-333">In the classic portal, go to the **Dashboard** tab for your web app, and then click the **Delete** button at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="3599c-333">In the classic portal, go to the **Dashboard** tab for your web app, and then click the **Delete** button at the bottom of the page.</span></span> <span data-ttu-id="3599c-334">You can then select a check box to delete the SQL Database instance at the same time.</span><span class="sxs-lookup"><span data-stu-id="3599c-334">You can then select a check box to delete the SQL Database instance at the same time.</span></span> <span data-ttu-id="3599c-335">If you just want to temporarily prevent others from accessing the web app, click **Stop** instead.</span><span class="sxs-lookup"><span data-stu-id="3599c-335">If you just want to temporarily prevent others from accessing the web app, click **Stop** instead.</span></span> <span data-ttu-id="3599c-336">In that case, charges will continue to accrue for the SQL Database and Storage account.</span><span class="sxs-lookup"><span data-stu-id="3599c-336">In that case, charges will continue to accrue for the SQL Database and Storage account.</span></span> <span data-ttu-id="3599c-337">You can follow a similar procedure to delete the SQL database and storage account when you no longer need them.</span><span class="sxs-lookup"><span data-stu-id="3599c-337">You can follow a similar procedure to delete the SQL database and storage account when you no longer need them.</span></span>
>
>

## <a id="create"></a><span data-ttu-id="3599c-338">Create the application from scratch</span><span class="sxs-lookup"><span data-stu-id="3599c-338">Create the application from scratch</span></span>
<span data-ttu-id="3599c-339">In this section you'll do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="3599c-339">In this section you'll do the following tasks:</span></span>

* <span data-ttu-id="3599c-340">Create a Visual Studio solution with a web project.</span><span class="sxs-lookup"><span data-stu-id="3599c-340">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="3599c-341">Add a class library project for the data access layer that is shared between front end and backend.</span><span class="sxs-lookup"><span data-stu-id="3599c-341">Add a class library project for the data access layer that is shared between front end and backend.</span></span>
* <span data-ttu-id="3599c-342">Add a Console Application project for the backend, with WebJobs deployment enabled.</span><span class="sxs-lookup"><span data-stu-id="3599c-342">Add a Console Application project for the backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="3599c-343">Add NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="3599c-343">Add NuGet packages.</span></span>
* <span data-ttu-id="3599c-344">Set project references.</span><span class="sxs-lookup"><span data-stu-id="3599c-344">Set project references.</span></span>
* <span data-ttu-id="3599c-345">Copy application code and configuration files from the downloaded application that you worked with in the previous section of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="3599c-345">Copy application code and configuration files from the downloaded application that you worked with in the previous section of the tutorial.</span></span>
* <span data-ttu-id="3599c-346">Review the parts of the code that work with Azure blobs and queues and the WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="3599c-346">Review the parts of the code that work with Azure blobs and queues and the WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="3599c-347">Create a Visual Studio solution with a web project and class library project</span><span class="sxs-lookup"><span data-stu-id="3599c-347">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="3599c-348">In Visual Studio, choose **New** > **Project** from the **File** menu.</span><span class="sxs-lookup"><span data-stu-id="3599c-348">In Visual Studio, choose **New** > **Project** from the **File** menu.</span></span>
2. <span data-ttu-id="3599c-349">In the **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application**.</span><span class="sxs-lookup"><span data-stu-id="3599c-349">In the **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application**.</span></span>
3. <span data-ttu-id="3599c-350">Name the project ContosoAdsWeb, name the solution ContosoAdsWebJobsSDK (change the solution name if you're putting it in the same folder as the downloaded solution), and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3599c-350">Name the project ContosoAdsWeb, name the solution ContosoAdsWebJobsSDK (change the solution name if you're putting it in the same folder as the downloaded solution), and then click **OK**.</span></span>

    ![New Project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="3599c-352">In the **New ASP.NET Project** dialog, choose the MVC template, and clear the **Host in the cloud** check box under **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="3599c-352">In the **New ASP.NET Project** dialog, choose the MVC template, and clear the **Host in the cloud** check box under **Microsoft Azure**.</span></span>

    <span data-ttu-id="3599c-353">Selecting **Host in the cloud** enables Visual Studio to automatically create a new Azure web app and SQL Database.</span><span class="sxs-lookup"><span data-stu-id="3599c-353">Selecting **Host in the cloud** enables Visual Studio to automatically create a new Azure web app and SQL Database.</span></span> <span data-ttu-id="3599c-354">Since you already created these earlier, you don't need to do so now while creating the project.</span><span class="sxs-lookup"><span data-stu-id="3599c-354">Since you already created these earlier, you don't need to do so now while creating the project.</span></span> <span data-ttu-id="3599c-355">If you want to create a new one, select the check box.</span><span class="sxs-lookup"><span data-stu-id="3599c-355">If you want to create a new one, select the check box.</span></span> <span data-ttu-id="3599c-356">You can then configure the new web app and SQL database the same way you did earlier when you deployed the application.</span><span class="sxs-lookup"><span data-stu-id="3599c-356">You can then configure the new web app and SQL database the same way you did earlier when you deployed the application.</span></span>
5. <span data-ttu-id="3599c-357">Click **Change Authentication**.</span><span class="sxs-lookup"><span data-stu-id="3599c-357">Click **Change Authentication**.</span></span>

    ![Change Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
6. <span data-ttu-id="3599c-359">In the **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3599c-359">In the **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![No Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
7. <span data-ttu-id="3599c-361">In the **New ASP.NET Project** dialog, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3599c-361">In the **New ASP.NET Project** dialog, click **OK**.</span></span>

    <span data-ttu-id="3599c-362">Visual Studio creates the solution and the web project.</span><span class="sxs-lookup"><span data-stu-id="3599c-362">Visual Studio creates the solution and the web project.</span></span>
8. <span data-ttu-id="3599c-363">In **Solution Explorer**, right-click the solution (not the project), and choose **Add** > **New Project**.</span><span class="sxs-lookup"><span data-stu-id="3599c-363">In **Solution Explorer**, right-click the solution (not the project), and choose **Add** > **New Project**.</span></span>
9. <span data-ttu-id="3599c-364">In the **Add New Project** dialog, choose **Visual C#** > **Windows Desktop** > **Class Library** template.</span><span class="sxs-lookup"><span data-stu-id="3599c-364">In the **Add New Project** dialog, choose **Visual C#** > **Windows Desktop** > **Class Library** template.</span></span>  
10. <span data-ttu-id="3599c-365">Name the project *ContosoAdsCommon*, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3599c-365">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="3599c-366">This project will contain the Entity Framework context and the data model which both the front end and back end will use.</span><span class="sxs-lookup"><span data-stu-id="3599c-366">This project will contain the Entity Framework context and the data model which both the front end and back end will use.</span></span> <span data-ttu-id="3599c-367">As an alternative you could define the EF-related classes in the web project and reference that project from the WebJob project.</span><span class="sxs-lookup"><span data-stu-id="3599c-367">As an alternative you could define the EF-related classes in the web project and reference that project from the WebJob project.</span></span> <span data-ttu-id="3599c-368">But then your WebJob project would have a reference to web assemblies which it doesn't need.</span><span class="sxs-lookup"><span data-stu-id="3599c-368">But then your WebJob project would have a reference to web assemblies which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="3599c-369">Add a Console Application project that has WebJobs deployment enabled</span><span class="sxs-lookup"><span data-stu-id="3599c-369">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="3599c-370">Right-click the web project (not the solution or the class library project), and then click **Add** > **New Azure WebJob Project**.</span><span class="sxs-lookup"><span data-stu-id="3599c-370">Right-click the web project (not the solution or the class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![New Azure WebJob Project menu selection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="3599c-372">In the **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both the **Project name** and the **WebJob name**.</span><span class="sxs-lookup"><span data-stu-id="3599c-372">In the **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both the **Project name** and the **WebJob name**.</span></span> <span data-ttu-id="3599c-373">Leave **WebJob run mode** set to **Run Continuously**.</span><span class="sxs-lookup"><span data-stu-id="3599c-373">Leave **WebJob run mode** set to **Run Continuously**.</span></span>
3. <span data-ttu-id="3599c-374">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3599c-374">Click **OK**.</span></span>

   <span data-ttu-id="3599c-375">Visual Studio creates a Console application that is configured to deploy as a WebJob whenever you deploy the web project.</span><span class="sxs-lookup"><span data-stu-id="3599c-375">Visual Studio creates a Console application that is configured to deploy as a WebJob whenever you deploy the web project.</span></span> <span data-ttu-id="3599c-376">To do that, it performed the following tasks after creating the project:</span><span class="sxs-lookup"><span data-stu-id="3599c-376">To do that, it performed the following tasks after creating the project:</span></span>

   * <span data-ttu-id="3599c-377">Added a *webjob-publish-settings.json* file in the WebJob project Properties folder.</span><span class="sxs-lookup"><span data-stu-id="3599c-377">Added a *webjob-publish-settings.json* file in the WebJob project Properties folder.</span></span>
   * <span data-ttu-id="3599c-378">Added a *webjobs-list.json* file in the web project Properties folder.</span><span class="sxs-lookup"><span data-stu-id="3599c-378">Added a *webjobs-list.json* file in the web project Properties folder.</span></span>
   * <span data-ttu-id="3599c-379">Installed the Microsoft.Web.WebJobs.Publish NuGet package in the WebJob project.</span><span class="sxs-lookup"><span data-stu-id="3599c-379">Installed the Microsoft.Web.WebJobs.Publish NuGet package in the WebJob project.</span></span>

   <span data-ttu-id="3599c-380">For more information about these changes, see [How to deploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="3599c-380">For more information about these changes, see [How to deploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="3599c-381">Add NuGet packages</span><span class="sxs-lookup"><span data-stu-id="3599c-381">Add NuGet packages</span></span>
<span data-ttu-id="3599c-382">The new-project template for a WebJob project automatically installs the WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="3599c-382">The new-project template for a WebJob project automatically installs the WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="3599c-383">One of the WebJobs SDK dependencies that is installed automatically in the WebJob project is the Azure Storage Client Library (SCL).</span><span class="sxs-lookup"><span data-stu-id="3599c-383">One of the WebJobs SDK dependencies that is installed automatically in the WebJob project is the Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="3599c-384">However, you need to add it to the web project to work with blobs and queues.</span><span class="sxs-lookup"><span data-stu-id="3599c-384">However, you need to add it to the web project to work with blobs and queues.</span></span>

1. <span data-ttu-id="3599c-385">Open the **Manage NuGet Packages** dialog for the solution.</span><span class="sxs-lookup"><span data-stu-id="3599c-385">Open the **Manage NuGet Packages** dialog for the solution.</span></span>
2. <span data-ttu-id="3599c-386">In the left pane, select **Installed packages**.</span><span class="sxs-lookup"><span data-stu-id="3599c-386">In the left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="3599c-387">Find the *Azure Storage* package, and then click **Manage**.</span><span class="sxs-lookup"><span data-stu-id="3599c-387">Find the *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="3599c-388">In the **Select Projects** box, select the **ContosoAdsWeb** check box, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3599c-388">In the **Select Projects** box, select the **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="3599c-389">All three projects use the Entity Framework to work with data in SQL Database.</span><span class="sxs-lookup"><span data-stu-id="3599c-389">All three projects use the Entity Framework to work with data in SQL Database.</span></span>
5. <span data-ttu-id="3599c-390">In the left pane, select **Online**.</span><span class="sxs-lookup"><span data-stu-id="3599c-390">In the left pane, select **Online**.</span></span>
6. <span data-ttu-id="3599c-391">Find the *EntityFramework* NuGet package, and install it in all three projects.</span><span class="sxs-lookup"><span data-stu-id="3599c-391">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="3599c-392">Set project references</span><span class="sxs-lookup"><span data-stu-id="3599c-392">Set project references</span></span>
<span data-ttu-id="3599c-393">Both web and WebJob projects work with the SQL database, so both need a reference to the ContosoAdsCommon project.</span><span class="sxs-lookup"><span data-stu-id="3599c-393">Both web and WebJob projects work with the SQL database, so both need a reference to the ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="3599c-394">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span><span class="sxs-lookup"><span data-stu-id="3599c-394">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="3599c-395">(Right-click the ContosoAdsWeb project, and then click **Add** > **Reference**.</span><span class="sxs-lookup"><span data-stu-id="3599c-395">(Right-click the ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> <span data-ttu-id="3599c-396">In the **Reference Manager** dialog box, select **Solution** > **Projects** > **ContosoAdsCommon**, and then click **OK**.)</span><span class="sxs-lookup"><span data-stu-id="3599c-396">In the **Reference Manager** dialog box, select **Solution** > **Projects** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
2. <span data-ttu-id="3599c-397">In the ContosoAdsWebJob project, set a reference to the ContosAdsCommon project.</span><span class="sxs-lookup"><span data-stu-id="3599c-397">In the ContosoAdsWebJob project, set a reference to the ContosAdsCommon project.</span></span>

    <span data-ttu-id="3599c-398">The WebJob project needs references for working with images and for accessing connection strings.</span><span class="sxs-lookup"><span data-stu-id="3599c-398">The WebJob project needs references for working with images and for accessing connection strings.</span></span>
3. <span data-ttu-id="3599c-399">In the ContosoAdsWebJob project, set a reference to `System.Drawing` and `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="3599c-399">In the ContosoAdsWebJob project, set a reference to `System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="3599c-400">Add code and configuration files</span><span class="sxs-lookup"><span data-stu-id="3599c-400">Add code and configuration files</span></span>
<span data-ttu-id="3599c-401">This tutorial does not show how to [create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how to [write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [the basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="3599c-401">This tutorial does not show how to [create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how to [write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [the basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="3599c-402">So all that remains to do is copy code and configuration files from the downloaded solution into the new solution.</span><span class="sxs-lookup"><span data-stu-id="3599c-402">So all that remains to do is copy code and configuration files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="3599c-403">After you do that, the following sections show and explain key parts of the code.</span><span class="sxs-lookup"><span data-stu-id="3599c-403">After you do that, the following sections show and explain key parts of the code.</span></span>

<span data-ttu-id="3599c-404">To add files to a project or a folder, right-click the project or folder and click **Add** > **Existing Item**.</span><span class="sxs-lookup"><span data-stu-id="3599c-404">To add files to a project or a folder, right-click the project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="3599c-405">Select the files you want and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="3599c-405">Select the files you want and click **Add**.</span></span> <span data-ttu-id="3599c-406">If asked whether you want to replace existing files, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="3599c-406">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="3599c-407">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the following files from the downloaded project.</span><span class="sxs-lookup"><span data-stu-id="3599c-407">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the following files from the downloaded project.</span></span>

   * <span data-ttu-id="3599c-408">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="3599c-408">*Ad.cs*</span></span>
   * <span data-ttu-id="3599c-409">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="3599c-409">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="3599c-410">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="3599c-410">*BlobInformation.cs*</span></span><br/><br/>
2. <span data-ttu-id="3599c-411">In the ContosoAdsWeb project, add the following files from the downloaded project.</span><span class="sxs-lookup"><span data-stu-id="3599c-411">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="3599c-412">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="3599c-412">*Web.config*</span></span>
   * <span data-ttu-id="3599c-413">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="3599c-413">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="3599c-414">In the *Controllers* folder: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="3599c-414">In the *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="3599c-415">In the *Views\Shared* folder: *_Layout.cshtml* file</span><span class="sxs-lookup"><span data-stu-id="3599c-415">In the *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="3599c-416">In the *Views\Home* folder: *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="3599c-416">In the *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="3599c-417">In the *Views\Ad* folder (create the folder first): five *.cshtml* files</span><span class="sxs-lookup"><span data-stu-id="3599c-417">In the *Views\Ad* folder (create the folder first): five *.cshtml* files</span></span><br/><br/>
3. <span data-ttu-id="3599c-418">In the ContosoAdsWebJob project, add the following files from the downloaded project.</span><span class="sxs-lookup"><span data-stu-id="3599c-418">In the ContosoAdsWebJob project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="3599c-419">*App.config* (change the file type filter to **All Files**)</span><span class="sxs-lookup"><span data-stu-id="3599c-419">*App.config* (change the file type filter to **All Files**)</span></span>
   * <span data-ttu-id="3599c-420">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="3599c-420">*Program.cs*</span></span>
   * <span data-ttu-id="3599c-421">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="3599c-421">*Functions.cs*</span></span>

<span data-ttu-id="3599c-422">You can now build, run, and deploy the application as instructed earlier in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="3599c-422">You can now build, run, and deploy the application as instructed earlier in the tutorial.</span></span> <span data-ttu-id="3599c-423">Before you do that, however, stop the WebJob that is still running in the first web app you deployed to.</span><span class="sxs-lookup"><span data-stu-id="3599c-423">Before you do that, however, stop the WebJob that is still running in the first web app you deployed to.</span></span> <span data-ttu-id="3599c-424">Otherwise that WebJob will process queue messages created locally or by the app running in a new web app, since all are using the same storage account.</span><span class="sxs-lookup"><span data-stu-id="3599c-424">Otherwise that WebJob will process queue messages created locally or by the app running in a new web app, since all are using the same storage account.</span></span>

## <a id="code"></a><span data-ttu-id="3599c-425">Review the application code</span><span class="sxs-lookup"><span data-stu-id="3599c-425">Review the application code</span></span>
<span data-ttu-id="3599c-426">The following sections explain the code related to working with the WebJobs SDK and Azure Storage blobs and queues.</span><span class="sxs-lookup"><span data-stu-id="3599c-426">The following sections explain the code related to working with the WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="3599c-427">For the code specific to the WebJobs SDK, go to the [Program.cs and Functions.cs](#programcs) sections.</span><span class="sxs-lookup"><span data-stu-id="3599c-427">For the code specific to the WebJobs SDK, go to the [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="3599c-428">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="3599c-428">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="3599c-429">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span><span class="sxs-lookup"><span data-stu-id="3599c-429">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="3599c-430">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="3599c-430">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="3599c-431">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span><span class="sxs-lookup"><span data-stu-id="3599c-431">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="3599c-432">The class has two constructors.</span><span class="sxs-lookup"><span data-stu-id="3599c-432">The class has two constructors.</span></span> <span data-ttu-id="3599c-433">The first is used by the web project, and specifies the name of a connection string that is stored in the Web.config file or the Azure runtime environment.</span><span class="sxs-lookup"><span data-stu-id="3599c-433">The first is used by the web project, and specifies the name of a connection string that is stored in the Web.config file or the Azure runtime environment.</span></span> <span data-ttu-id="3599c-434">The second constructor enables you to pass in the actual connection string.</span><span class="sxs-lookup"><span data-stu-id="3599c-434">The second constructor enables you to pass in the actual connection string.</span></span> <span data-ttu-id="3599c-435">That is needed by the WebJob project since it doesn't have a Web.config file.</span><span class="sxs-lookup"><span data-stu-id="3599c-435">That is needed by the WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="3599c-436">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span><span class="sxs-lookup"><span data-stu-id="3599c-436">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="3599c-437">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="3599c-437">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="3599c-438">The `BlobInformation` class is used to store information about an image blob in a queue message.</span><span class="sxs-lookup"><span data-stu-id="3599c-438">The `BlobInformation` class is used to store information about an image blob in a queue message.</span></span>

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="3599c-439">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="3599c-439">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="3599c-440">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span><span class="sxs-lookup"><span data-stu-id="3599c-440">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="3599c-441">This ensures that whenever you start using a new storage account, the required blob container and queue are created automatically.</span><span class="sxs-lookup"><span data-stu-id="3599c-441">This ensures that whenever you start using a new storage account, the required blob container and queue are created automatically.</span></span>

<span data-ttu-id="3599c-442">The code gets access to the storage account by using the storage connection string from the *Web.config* file or Azure runtime environment.</span><span class="sxs-lookup"><span data-stu-id="3599c-442">The code gets access to the storage account by using the storage connection string from the *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="3599c-443">Then it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span><span class="sxs-lookup"><span data-stu-id="3599c-443">Then it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="3599c-444">By default new containers allow only clients with storage account credentials to access blobs.</span><span class="sxs-lookup"><span data-stu-id="3599c-444">By default new containers allow only clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="3599c-445">The web app needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span><span class="sxs-lookup"><span data-stu-id="3599c-445">The web app needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

<span data-ttu-id="3599c-446">Similar code gets a reference to the *thumbnailrequest* queue and creates a new queue.</span><span class="sxs-lookup"><span data-stu-id="3599c-446">Similar code gets a reference to the *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="3599c-447">In this case no permissions change is needed.</span><span class="sxs-lookup"><span data-stu-id="3599c-447">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="3599c-448">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="3599c-448">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="3599c-449">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span><span class="sxs-lookup"><span data-stu-id="3599c-449">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="3599c-450">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="3599c-450">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="3599c-451">The *Views\Home\Index.cshtml* file displays category links on the home page.</span><span class="sxs-lookup"><span data-stu-id="3599c-451">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="3599c-452">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span><span class="sxs-lookup"><span data-stu-id="3599c-452">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="3599c-453">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="3599c-453">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="3599c-454">In the *AdController.cs* file the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span><span class="sxs-lookup"><span data-stu-id="3599c-454">In the *AdController.cs* file the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="3599c-455">Then the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="3599c-455">Then the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="3599c-456">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span><span class="sxs-lookup"><span data-stu-id="3599c-456">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="3599c-457">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span><span class="sxs-lookup"><span data-stu-id="3599c-457">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="3599c-458">The retry policy specified here waits 3 seconds after each try for up to 3 tries.</span><span class="sxs-lookup"><span data-stu-id="3599c-458">The retry policy specified here waits 3 seconds after each try for up to 3 tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="3599c-459">Similar code gets a reference to the *images* queue.</span><span class="sxs-lookup"><span data-stu-id="3599c-459">Similar code gets a reference to the *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="3599c-460">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span><span class="sxs-lookup"><span data-stu-id="3599c-460">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="3599c-461">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span><span class="sxs-lookup"><span data-stu-id="3599c-461">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="3599c-462">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span><span class="sxs-lookup"><span data-stu-id="3599c-462">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="3599c-463">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span><span class="sxs-lookup"><span data-stu-id="3599c-463">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="3599c-464">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span><span class="sxs-lookup"><span data-stu-id="3599c-464">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="3599c-465">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span><span class="sxs-lookup"><span data-stu-id="3599c-465">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

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

<span data-ttu-id="3599c-466">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform the back-end process that an image is ready for conversion to a thumbnail.</span><span class="sxs-lookup"><span data-stu-id="3599c-466">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform the back-end process that an image is ready for conversion to a thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="3599c-467">The code for the HttpPost `Edit` method is similar except that if the user selects a new image file any blobs that already exist for this ad must be deleted.</span><span class="sxs-lookup"><span data-stu-id="3599c-467">The code for the HttpPost `Edit` method is similar except that if the user selects a new image file any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="3599c-468">Here is the code that deletes blobs when you delete an ad:</span><span class="sxs-lookup"><span data-stu-id="3599c-468">Here is the code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="3599c-469">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="3599c-469">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="3599c-470">The *Index.cshtml* file displays thumbnails with the other ad data:</span><span class="sxs-lookup"><span data-stu-id="3599c-470">The *Index.cshtml* file displays thumbnails with the other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="3599c-471">The *Details.cshtml* file displays the full-size image:</span><span class="sxs-lookup"><span data-stu-id="3599c-471">The *Details.cshtml* file displays the full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="3599c-472">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="3599c-472">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="3599c-473">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span><span class="sxs-lookup"><span data-stu-id="3599c-473">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="3599c-474">An `<input>` element tells the browser to provide a file selection dialog.</span><span class="sxs-lookup"><span data-stu-id="3599c-474">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <a id="programcs"></a><span data-ttu-id="3599c-475">ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="3599c-475">ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="3599c-476">When the WebJob starts, the `Main` method calls the WebJobs SDK `JobHost.RunAndBlock` method to begin execution of triggered functions on the current thread.</span><span class="sxs-lookup"><span data-stu-id="3599c-476">When the WebJob starts, the `Main` method calls the WebJobs SDK `JobHost.RunAndBlock` method to begin execution of triggered functions on the current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <a id="generatethumbnail"></a><span data-ttu-id="3599c-477">ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span><span class="sxs-lookup"><span data-stu-id="3599c-477">ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="3599c-478">The WebJobs SDK calls this method when a queue message is received.</span><span class="sxs-lookup"><span data-stu-id="3599c-478">The WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="3599c-479">The method creates a thumbnail and puts the thumbnail URL in the database.</span><span class="sxs-lookup"><span data-stu-id="3599c-479">The method creates a thumbnail and puts the thumbnail URL in the database.</span></span>

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within the function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* <span data-ttu-id="3599c-480">The `QueueTrigger` attribute directs the WebJobs SDK to call this method when a new message is received on the thumbnailrequest queue.</span><span class="sxs-lookup"><span data-stu-id="3599c-480">The `QueueTrigger` attribute directs the WebJobs SDK to call this method when a new message is received on the thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="3599c-481">The `BlobInformation` object in the queue message is automatically deserialized into the `blobInfo` parameter.</span><span class="sxs-lookup"><span data-stu-id="3599c-481">The `BlobInformation` object in the queue message is automatically deserialized into the `blobInfo` parameter.</span></span> <span data-ttu-id="3599c-482">When the method completes, the queue message is deleted.</span><span class="sxs-lookup"><span data-stu-id="3599c-482">When the method completes, the queue message is deleted.</span></span> <span data-ttu-id="3599c-483">If the method fails before completing, the queue message is not deleted; after a 10-minute lease expires, the message is released to be picked up again and processed.</span><span class="sxs-lookup"><span data-stu-id="3599c-483">If the method fails before completing, the queue message is not deleted; after a 10-minute lease expires, the message is released to be picked up again and processed.</span></span> <span data-ttu-id="3599c-484">This sequence won't be repeated indefinitely if a message always causes an exception.</span><span class="sxs-lookup"><span data-stu-id="3599c-484">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="3599c-485">After 5 unsuccessful attempts to process a message, the message is moved to a queue named {queuename}-poison.</span><span class="sxs-lookup"><span data-stu-id="3599c-485">After 5 unsuccessful attempts to process a message, the message is moved to a queue named {queuename}-poison.</span></span> <span data-ttu-id="3599c-486">The maximum number of attempts is configurable.</span><span class="sxs-lookup"><span data-stu-id="3599c-486">The maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="3599c-487">The two `Blob` attributes provide objects that are bound to blobs: one to the existing image blob and one to a new thumbnail blob that the method creates.</span><span class="sxs-lookup"><span data-stu-id="3599c-487">The two `Blob` attributes provide objects that are bound to blobs: one to the existing image blob and one to a new thumbnail blob that the method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="3599c-488">Blob names come from properties of the `BlobInformation` object received in the queue message (`BlobName` and `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="3599c-488">Blob names come from properties of the `BlobInformation` object received in the queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="3599c-489">To get the full functionality of the Storage Client Library you can use the `CloudBlockBlob` class to work with blobs.</span><span class="sxs-lookup"><span data-stu-id="3599c-489">To get the full functionality of the Storage Client Library you can use the `CloudBlockBlob` class to work with blobs.</span></span> <span data-ttu-id="3599c-490">If you want to reuse code that was written to work with `Stream` objects, you can use the `Stream` class.</span><span class="sxs-lookup"><span data-stu-id="3599c-490">If you want to reuse code that was written to work with `Stream` objects, you can use the `Stream` class.</span></span>

<span data-ttu-id="3599c-491">For more information about how to write functions that use  WebJobs SDK attributes, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="3599c-491">For more information about how to write functions that use  WebJobs SDK attributes, see the following resources:</span></span>

* [<span data-ttu-id="3599c-492">How to use Azure queue storage with the WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="3599c-492">How to use Azure queue storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="3599c-493">How to use Azure blob storage with the WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="3599c-493">How to use Azure blob storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="3599c-494">How to use Azure table storage with the WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="3599c-494">How to use Azure table storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="3599c-495">How to use Azure Service Bus with the WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="3599c-495">How to use Azure Service Bus with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="3599c-496">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in the same data getting processed multiple times.</span><span class="sxs-lookup"><span data-stu-id="3599c-496">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in the same data getting processed multiple times.</span></span> <span data-ttu-id="3599c-497">This is not a problem if you use the built-in queue, blob, and Service Bus triggers.</span><span class="sxs-lookup"><span data-stu-id="3599c-497">This is not a problem if you use the built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="3599c-498">The SDK ensures that your functions will be processed only once for each message or blob.</span><span class="sxs-lookup"><span data-stu-id="3599c-498">The SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="3599c-499">For information about how to implement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="3599c-499">For information about how to implement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="3599c-500">The code in the `ConvertImageToThumbnailJPG` method (not shown) uses classes in the `System.Drawing` namespace for simplicity.</span><span class="sxs-lookup"><span data-stu-id="3599c-500">The code in the `ConvertImageToThumbnailJPG` method (not shown) uses classes in the `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="3599c-501">However, the classes in this namespace were designed for use with Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="3599c-501">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="3599c-502">They are not supported for use in a Windows or ASP.NET service.</span><span class="sxs-lookup"><span data-stu-id="3599c-502">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="3599c-503">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="3599c-503">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3599c-504">Next steps</span><span class="sxs-lookup"><span data-stu-id="3599c-504">Next steps</span></span>
<span data-ttu-id="3599c-505">In this tutorial you've seen a simple multi-tier application that uses the WebJobs SDK for backend processing.</span><span class="sxs-lookup"><span data-stu-id="3599c-505">In this tutorial you've seen a simple multi-tier application that uses the WebJobs SDK for backend processing.</span></span> <span data-ttu-id="3599c-506">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span><span class="sxs-lookup"><span data-stu-id="3599c-506">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="3599c-507">Missing features</span><span class="sxs-lookup"><span data-stu-id="3599c-507">Missing features</span></span>
<span data-ttu-id="3599c-508">The application has been kept simple for a getting-started tutorial.</span><span class="sxs-lookup"><span data-stu-id="3599c-508">The application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="3599c-509">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors.</span><span class="sxs-lookup"><span data-stu-id="3599c-509">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="3599c-510">Scaling WebJobs</span><span class="sxs-lookup"><span data-stu-id="3599c-510">Scaling WebJobs</span></span>
<span data-ttu-id="3599c-511">WebJobs run in the context of a web app and are not scalable separately.</span><span class="sxs-lookup"><span data-stu-id="3599c-511">WebJobs run in the context of a web app and are not scalable separately.</span></span> <span data-ttu-id="3599c-512">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of the server resources (CPU, memory, etc.) that otherwise would be available to serve web content.</span><span class="sxs-lookup"><span data-stu-id="3599c-512">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of the server resources (CPU, memory, etc.) that otherwise would be available to serve web content.</span></span>

<span data-ttu-id="3599c-513">If traffic varies by time of day or day of week, and if the backend processing you need to do can wait, you could schedule your WebJobs to run at low-traffic times.</span><span class="sxs-lookup"><span data-stu-id="3599c-513">If traffic varies by time of day or day of week, and if the backend processing you need to do can wait, you could schedule your WebJobs to run at low-traffic times.</span></span> <span data-ttu-id="3599c-514">If the load is still too high for that solution, you can run the backend as a WebJob in a separate web app dedicated for that purpose.</span><span class="sxs-lookup"><span data-stu-id="3599c-514">If the load is still too high for that solution, you can run the backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="3599c-515">You can then scale your backend web app independently from your frontend web app.</span><span class="sxs-lookup"><span data-stu-id="3599c-515">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="3599c-516">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="3599c-516">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="3599c-517">Avoiding web app timeout shut-downs</span><span class="sxs-lookup"><span data-stu-id="3599c-517">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="3599c-518">To make sure your WebJobs are always running, and running on all instances of your web app, you have to enable the [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span><span class="sxs-lookup"><span data-stu-id="3599c-518">To make sure your WebJobs are always running, and running on all instances of your web app, you have to enable the [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-the-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="3599c-519">Using the WebJobs SDK outside of WebJobs</span><span class="sxs-lookup"><span data-stu-id="3599c-519">Using the WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="3599c-520">A program that uses the WebJobs SDK doesn't have to run in Azure in a WebJob.</span><span class="sxs-lookup"><span data-stu-id="3599c-520">A program that uses the WebJobs SDK doesn't have to run in Azure in a WebJob.</span></span> <span data-ttu-id="3599c-521">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span><span class="sxs-lookup"><span data-stu-id="3599c-521">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="3599c-522">However, you can only access the WebJobs SDK dashboard through an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="3599c-522">However, you can only access the WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="3599c-523">To use the dashboard you have to connect the web app to the storage account you're using by setting the AzureWebJobsDashboard connection string on the **Configure** tab of the classic portal.</span><span class="sxs-lookup"><span data-stu-id="3599c-523">To use the dashboard you have to connect the web app to the storage account you're using by setting the AzureWebJobsDashboard connection string on the **Configure** tab of the classic portal.</span></span> <span data-ttu-id="3599c-524">Then you can get to the Dashboard by using the following URL:</span><span class="sxs-lookup"><span data-stu-id="3599c-524">Then you can get to the Dashboard by using the following URL:</span></span>

<span data-ttu-id="3599c-525">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span><span class="sxs-lookup"><span data-stu-id="3599c-525">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="3599c-526">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span><span class="sxs-lookup"><span data-stu-id="3599c-526">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="3599c-527">More WebJobs documentation</span><span class="sxs-lookup"><span data-stu-id="3599c-527">More WebJobs documentation</span></span>
<span data-ttu-id="3599c-528">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="3599c-528">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>






























