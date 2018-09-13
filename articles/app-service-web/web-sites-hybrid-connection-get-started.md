---
title: Access on-premises resources using hybrid connections in Azure App Service
description: Create a connection between a web app in Azure App Service and an on-premises resource that uses a static TCP port
services: app-service
documentationcenter: ''
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: 9da6192a3fc597992d54c82933491ba4891b40d7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556163"
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="69f5a-103">Access on-premises resources using hybrid connections in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="69f5a-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="69f5a-104">You can connect an Azure App Service app to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span><span class="sxs-lookup"><span data-stu-id="69f5a-104">You can connect an Azure App Service app to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="69f5a-105">This article shows you how to create a hybrid connection between App Service and an on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="69f5a-105">This article shows you how to create a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="69f5a-106">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="69f5a-106">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="69f5a-107">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="69f5a-107">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="69f5a-108">This content also applies to Mobile Apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="69f5a-108">This content also applies to Mobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="69f5a-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="69f5a-109">Prerequisites</span></span>
* <span data-ttu-id="69f5a-110">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="69f5a-110">An Azure subscription.</span></span> <span data-ttu-id="69f5a-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="69f5a-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="69f5a-112">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="69f5a-112">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="69f5a-113">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="69f5a-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="69f5a-114">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span><span class="sxs-lookup"><span data-stu-id="69f5a-114">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="69f5a-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span><span class="sxs-lookup"><span data-stu-id="69f5a-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="69f5a-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="69f5a-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="69f5a-117">The computer on which you install the on-premises Hybrid Connection Manager agent described later in this article:</span><span class="sxs-lookup"><span data-stu-id="69f5a-117">The computer on which you install the on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="69f5a-118">Must be able to connect to Azure over port 5671</span><span class="sxs-lookup"><span data-stu-id="69f5a-118">Must be able to connect to Azure over port 5671</span></span>
  * <span data-ttu-id="69f5a-119">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span><span class="sxs-lookup"><span data-stu-id="69f5a-119">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="69f5a-120">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span><span class="sxs-lookup"><span data-stu-id="69f5a-120">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="69f5a-121">Create a web app in the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="69f5a-121">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="69f5a-122">If you have already created a web app or Mobile App backend in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span><span class="sxs-lookup"><span data-stu-id="69f5a-122">If you have already created a web app or Mobile App backend in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="69f5a-123">In the upper left corner of the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span><span class="sxs-lookup"><span data-stu-id="69f5a-123">In the upper left corner of the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![New web app][NewWebsite]
2. <span data-ttu-id="69f5a-125">On the **Web app** blade, provide a URL and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="69f5a-125">On the **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="69f5a-127">After a few moments, the web app is created and its web app blade appears.</span><span class="sxs-lookup"><span data-stu-id="69f5a-127">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="69f5a-128">The blade is a vertically scrollable dashboard that lets you manage your site.</span><span class="sxs-lookup"><span data-stu-id="69f5a-128">The blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Website running][WebSiteRunningBlade]
4. <span data-ttu-id="69f5a-130">To verify the site is live, you can click the **Browse** icon to display the default page.</span><span class="sxs-lookup"><span data-stu-id="69f5a-130">To verify the site is live, you can click the **Browse** icon to display the default page.</span></span>
   
    ![Click browse to see your web app][Browse]
   
    ![Default web app page][DefaultWebSitePage]

<span data-ttu-id="69f5a-133">Next, you will create a hybrid connection and a BizTalk service for the web app.</span><span class="sxs-lookup"><span data-stu-id="69f5a-133">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="69f5a-134">Create a Hybrid Connection and a BizTalk Service</span><span class="sxs-lookup"><span data-stu-id="69f5a-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="69f5a-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span><span class="sxs-lookup"><span data-stu-id="69f5a-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Hybrid connections][CreateHCHCIcon]
2. <span data-ttu-id="69f5a-137">On the Hybrid connections blade, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="69f5a-137">On the Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="69f5a-138">The **Add a hybrid connection** blade opens.</span><span class="sxs-lookup"><span data-stu-id="69f5a-138">The **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="69f5a-139">Since this is your first hybrid connection, the **New hybrid connection** option is preselected, and the **Create hybrid connection** blade opens for you.</span><span class="sxs-lookup"><span data-stu-id="69f5a-139">Since this is your first hybrid connection, the **New hybrid connection** option is preselected, and the **Create hybrid connection** blade opens for you.</span></span>
   
    ![Create a hybrid connection][TwinCreateHCBlades]
   
    <span data-ttu-id="69f5a-141">On the **Create hybrid connection blade**:</span><span class="sxs-lookup"><span data-stu-id="69f5a-141">On the **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="69f5a-142">For **Name**, provide a name for the connection.</span><span class="sxs-lookup"><span data-stu-id="69f5a-142">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="69f5a-143">For **Hostname**, enter the name of the on-premises computer that hosts your resource.</span><span class="sxs-lookup"><span data-stu-id="69f5a-143">For **Hostname**, enter the name of the on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="69f5a-144">For **Port**, enter the port number that your on-premises resource uses (1433 for a SQL Server default instance).</span><span class="sxs-lookup"><span data-stu-id="69f5a-144">For **Port**, enter the port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="69f5a-145">Click **Biz Talk Service**</span><span class="sxs-lookup"><span data-stu-id="69f5a-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="69f5a-146">The **Create BizTalk Service** blade opens.</span><span class="sxs-lookup"><span data-stu-id="69f5a-146">The **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="69f5a-147">Enter a name for the BizTalk service, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="69f5a-147">Enter a name for the BizTalk service, and then click **OK**.</span></span>
   
    ![Create BizTalk service][CreateHCCreateBTS]
   
    <span data-ttu-id="69f5a-149">The **Create BizTalk Service** blade closes and you are returned to the **Create hybrid connection** blade.</span><span class="sxs-lookup"><span data-stu-id="69f5a-149">The **Create BizTalk Service** blade closes and you are returned to the **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="69f5a-150">On the Create hybrid connection blade, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="69f5a-150">On the Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Click OK][CreateBTScomplete]
6. <span data-ttu-id="69f5a-152">When the process completes, the notifications area in the Portal informs you that the connection has been successfully created.</span><span class="sxs-lookup"><span data-stu-id="69f5a-152">When the process completes, the notifications area in the Portal informs you that the connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in the dogfood portal. I switch to the classic portal
    (full portal) and created the BizTalk service but it doesn't seem to let you connnect them - When you finish the
    Create hybrid conn step, you get the following error
    Failed to create hybrid connection RelecIoudHC. The 
    resource type could not be found in the namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    The error indicates it couldn't find the type, not the instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="69f5a-153">On the web app's blade, the **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span><span class="sxs-lookup"><span data-stu-id="69f5a-153">On the web app's blade, the **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="69f5a-155">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span><span class="sxs-lookup"><span data-stu-id="69f5a-155">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="69f5a-156">Next, you will create a corresponding on-premises piece.</span><span class="sxs-lookup"><span data-stu-id="69f5a-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="69f5a-157">Install the on-premises Hybrid Connection Manager to complete the connection</span><span class="sxs-lookup"><span data-stu-id="69f5a-157">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
1. <span data-ttu-id="69f5a-158">On the web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span><span class="sxs-lookup"><span data-stu-id="69f5a-158">On the web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Hybrid connections icon][HCIcon]
2. <span data-ttu-id="69f5a-160">On the **Hybrid connections** blade, the **Status** column for the recently added endpoint shows **Not connected**.</span><span class="sxs-lookup"><span data-stu-id="69f5a-160">On the **Hybrid connections** blade, the **Status** column for the recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="69f5a-161">Click the connection to configure it.</span><span class="sxs-lookup"><span data-stu-id="69f5a-161">Click the connection to configure it.</span></span>
   
    ![Not connected][NotConnected]
   
    <span data-ttu-id="69f5a-163">The Hybrid connection blade opens.</span><span class="sxs-lookup"><span data-stu-id="69f5a-163">The Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="69f5a-165">On the blade, click **Listener Setup**.</span><span class="sxs-lookup"><span data-stu-id="69f5a-165">On the blade, click **Listener Setup**.</span></span>
   
    ![Click Listener Setup][ClickListenerSetup]
4. <span data-ttu-id="69f5a-167">The **Hybrid connection properties** blade opens.</span><span class="sxs-lookup"><span data-stu-id="69f5a-167">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="69f5a-168">Under **On-premises Hybrid Connection Manager**, choose **Click here to install**.</span><span class="sxs-lookup"><span data-stu-id="69f5a-168">Under **On-premises Hybrid Connection Manager**, choose **Click here to install**.</span></span>
   
    ![Click here to install][ClickToInstallHCM]
5. <span data-ttu-id="69f5a-170">In the Application Run security warning dialog, choose **Run** to continue.</span><span class="sxs-lookup"><span data-stu-id="69f5a-170">In the Application Run security warning dialog, choose **Run** to continue.</span></span>
   
    ![Choose Run to continue][ApplicationRunWarning]
6. <span data-ttu-id="69f5a-172">In the **User Account Control** dialog, choose **Yes**.</span><span class="sxs-lookup"><span data-stu-id="69f5a-172">In the **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Choose Yes][UAC]
7. <span data-ttu-id="69f5a-174">The Hybrid Connection Manager is downloaded and installed for you.</span><span class="sxs-lookup"><span data-stu-id="69f5a-174">The Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Installing][HCMInstalling]
8. <span data-ttu-id="69f5a-176">When the install completes, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="69f5a-176">When the install completes, click **Close**.</span></span>
   
    ![Click Close][HCMInstallComplete]
   
    <span data-ttu-id="69f5a-178">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span><span class="sxs-lookup"><span data-stu-id="69f5a-178">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Connected Status][HCStatusConnected]

<span data-ttu-id="69f5a-180">Now that the hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span><span class="sxs-lookup"><span data-stu-id="69f5a-180">Now that the hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="69f5a-181">The following sections show you how to use a hybrid connection with a Mobile Apps .NET backend project.</span><span class="sxs-lookup"><span data-stu-id="69f5a-181">The following sections show you how to use a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-the-mobile-app-net-backend-project-to-connect-to-the-sql-server-database"></a><span data-ttu-id="69f5a-182">Configure the Mobile App .NET backend project to connect to the SQL Server database</span><span class="sxs-lookup"><span data-stu-id="69f5a-182">Configure the Mobile App .NET backend project to connect to the SQL Server database</span></span>
<span data-ttu-id="69f5a-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span><span class="sxs-lookup"><span data-stu-id="69f5a-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="69f5a-184">To use your web app as a Mobile Apps backend, you must [download and initialize the Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="69f5a-184">To use your web app as a Mobile Apps backend, you must [download and initialize the Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="69f5a-185">For Mobile Apps, you also need to define a connection string for the on-premises database and modify the backend to use this connection.</span><span class="sxs-lookup"><span data-stu-id="69f5a-185">For Mobile Apps, you also need to define a connection string for the on-premises database and modify the backend to use this connection.</span></span> 

1. <span data-ttu-id="69f5a-186">In Solution Explorer in Visual Studio, open the Web.config file for your Mobile App .NET backend, locate the **connectionStrings** section, add a new SqlClient entry like the following, which points to the on-premises SQL Server database:</span><span class="sxs-lookup"><span data-stu-id="69f5a-186">In Solution Explorer in Visual Studio, open the Web.config file for your Mobile App .NET backend, locate the **connectionStrings** section, add a new SqlClient entry like the following, which points to the on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="69f5a-187">Remember to replace `<**secure_password**>` in this string with the password you created for  *HybridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="69f5a-187">Remember to replace `<**secure_password**>` in this string with the password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="69f5a-188">Click **Save** in Visual Studio to save the Web.config file.</span><span class="sxs-lookup"><span data-stu-id="69f5a-188">Click **Save** in Visual Studio to save the Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="69f5a-189">This connection setting is used when running on the local computer.</span><span class="sxs-lookup"><span data-stu-id="69f5a-189">This connection setting is used when running on the local computer.</span></span> <span data-ttu-id="69f5a-190">When running in Azure, this setting is overriden by the connection setting defined in the portal.</span><span class="sxs-lookup"><span data-stu-id="69f5a-190">When running in Azure, this setting is overriden by the connection setting defined in the portal.</span></span>
   > 
   > 
3. <span data-ttu-id="69f5a-191">Expand the **Models** folder and open the data model file, which ends in *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="69f5a-191">Expand the **Models** folder and open the data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="69f5a-192">Modify the **DbContext** instance constructor to pass the value `OnPremisesDBConnection` to the base **DbContext** constructor, similar to the following snippet:</span><span class="sxs-lookup"><span data-stu-id="69f5a-192">Modify the **DbContext** instance constructor to pass the value `OnPremisesDBConnection` to the base **DbContext** constructor, similar to the following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="69f5a-193">The service will now use the new connection to the SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="69f5a-193">The service will now use the new connection to the SQL Server database.</span></span>

## <a name="update-the-mobile-app-backend-to-use-the-on-premises-connection-string"></a><span data-ttu-id="69f5a-194">Update the Mobile App backend to use the on-premises connection string</span><span class="sxs-lookup"><span data-stu-id="69f5a-194">Update the Mobile App backend to use the on-premises connection string</span></span>
<span data-ttu-id="69f5a-195">Next, you need to add an app setting for this new connection string so that it can be used from Azure.</span><span class="sxs-lookup"><span data-stu-id="69f5a-195">Next, you need to add an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="69f5a-196">Back in the [Azure portal](https://portal.azure.com) in the web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span><span class="sxs-lookup"><span data-stu-id="69f5a-196">Back in the [Azure portal](https://portal.azure.com) in the web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="69f5a-197">In the **Web app settings** blade, scroll down to **Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="69f5a-197">In the **Web app settings** blade, scroll down to **Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="69f5a-198">Replace `<**secure_password**>` with the secure password for your on-premises database.</span><span class="sxs-lookup"><span data-stu-id="69f5a-198">Replace `<**secure_password**>` with the secure password for your on-premises database.</span></span>
   
    ![Connection string for on-premises database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="69f5a-200">Press **Save** to save the hybrid connection and connection string you just created.</span><span class="sxs-lookup"><span data-stu-id="69f5a-200">Press **Save** to save the hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="69f5a-201">At this point you can republish the server project and test the new connection with your existing Mobile Apps clients.</span><span class="sxs-lookup"><span data-stu-id="69f5a-201">At this point you can republish the server project and test the new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="69f5a-202">Data will be read from and written to the on-premises database using the hybrid connection.</span><span class="sxs-lookup"><span data-stu-id="69f5a-202">Data will be read from and written to the on-premises database using the hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="69f5a-203">Next Steps</span><span class="sxs-lookup"><span data-stu-id="69f5a-203">Next Steps</span></span>
* <span data-ttu-id="69f5a-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="69f5a-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="69f5a-205">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="69f5a-205">Additional Resources</span></span>
[<span data-ttu-id="69f5a-206">Hybrid Connections overview</span><span class="sxs-lookup"><span data-stu-id="69f5a-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="69f5a-207">Josh Twist introduces hybrid connections (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="69f5a-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="69f5a-208">Hybrid Connections web site</span><span class="sxs-lookup"><span data-stu-id="69f5a-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="69f5a-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span><span class="sxs-lookup"><span data-stu-id="69f5a-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="69f5a-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="69f5a-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="69f5a-211">Connect to an on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="69f5a-211">Connect to an on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="69f5a-212">What's changed</span><span class="sxs-lookup"><span data-stu-id="69f5a-212">What's changed</span></span>
* <span data-ttu-id="69f5a-213">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="69f5a-213">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[New]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
























