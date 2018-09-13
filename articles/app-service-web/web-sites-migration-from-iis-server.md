---
title: Migrate an enterprise web app to Azure App Service
description: Shows how to use Web Apps Migration Assistant to quickly migrate existing IIS websites to Azure App Service Web Apps
services: app-service
documentationcenter: ''
author: cephalin
writer: cephalin
manager: erikre
editor: ''
ms.assetid: 2e846fc0-37cc-42e6-ac57-ff442ef16e85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 86a185fe7f6f6c989f87ceb0a203156d33da1b26
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554561"
---
# <a name="migrate-an-enterprise-web-app-to-azure-app-service"></a><span data-ttu-id="1abc0-103">Migrate an enterprise web app to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1abc0-103">Migrate an enterprise web app to Azure App Service</span></span>
<span data-ttu-id="1abc0-104">You can easily migrate your existing websites that run on Internet Information Service (IIS) 6 or later to [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="1abc0-104">You can easily migrate your existing websites that run on Internet Information Service (IIS) 6 or later to [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1abc0-105">Windows Server 2003 reached end of support on July 14th 2015.</span><span class="sxs-lookup"><span data-stu-id="1abc0-105">Windows Server 2003 reached end of support on July 14th 2015.</span></span> <span data-ttu-id="1abc0-106">If you are currently hosting your websites on an IIS server that is Windows Server 2003, Web Apps is a low-risk, low-cost, and low-friction way to keep your websites online, and Web Apps Migration Assistant can help automate the migration process for you.</span><span class="sxs-lookup"><span data-stu-id="1abc0-106">If you are currently hosting your websites on an IIS server that is Windows Server 2003, Web Apps is a low-risk, low-cost, and low-friction way to keep your websites online, and Web Apps Migration Assistant can help automate the migration process for you.</span></span> 
> 
> 

<span data-ttu-id="1abc0-107">[Web Apps Migration Assistant](https://www.movemetothecloud.net/) can analyze your IIS server installation, identify which sites can be migrated to App Service, highlight any elements that cannot be migrated or are unsupported on the platform, and then migrate your websites and associated databases to Azure.</span><span class="sxs-lookup"><span data-stu-id="1abc0-107">[Web Apps Migration Assistant](https://www.movemetothecloud.net/) can analyze your IIS server installation, identify which sites can be migrated to App Service, highlight any elements that cannot be migrated or are unsupported on the platform, and then migrate your websites and associated databases to Azure.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a><span data-ttu-id="1abc0-108">Elements Verified During Compatibility Analysis</span><span class="sxs-lookup"><span data-stu-id="1abc0-108">Elements Verified During Compatibility Analysis</span></span>
<span data-ttu-id="1abc0-109">The Migration Assistant creates a readiness report to identify any potential causes for concern or blocking issues which may prevent a successful migration from on-premises IIS to Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="1abc0-109">The Migration Assistant creates a readiness report to identify any potential causes for concern or blocking issues which may prevent a successful migration from on-premises IIS to Azure App Service Web Apps.</span></span> <span data-ttu-id="1abc0-110">Some of the key items to be aware of are:</span><span class="sxs-lookup"><span data-stu-id="1abc0-110">Some of the key items to be aware of are:</span></span>

* <span data-ttu-id="1abc0-111">Port Bindings – Web Apps only supports Port 80 for HTTP and Port 443 for HTTPS traffic.</span><span class="sxs-lookup"><span data-stu-id="1abc0-111">Port Bindings – Web Apps only supports Port 80 for HTTP and Port 443 for HTTPS traffic.</span></span> <span data-ttu-id="1abc0-112">Different port configurations will be ignored and traffic will be routed to 80 or 443.</span><span class="sxs-lookup"><span data-stu-id="1abc0-112">Different port configurations will be ignored and traffic will be routed to 80 or 443.</span></span> 
* <span data-ttu-id="1abc0-113">Authentication – Web Apps supports Anonymous Authentication by default and Forms Authentication where specified by an application.</span><span class="sxs-lookup"><span data-stu-id="1abc0-113">Authentication – Web Apps supports Anonymous Authentication by default and Forms Authentication where specified by an application.</span></span> <span data-ttu-id="1abc0-114">Windows Authentication can be used by integrating with Azure Active Directory and ADFS only.</span><span class="sxs-lookup"><span data-stu-id="1abc0-114">Windows Authentication can be used by integrating with Azure Active Directory and ADFS only.</span></span> <span data-ttu-id="1abc0-115">All other forms of authentication - for example, Basic Authentication - are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="1abc0-115">All other forms of authentication - for example, Basic Authentication - are not currently supported.</span></span> 
* <span data-ttu-id="1abc0-116">Global Assembly Cache (GAC) – The GAC is not supported in Web Apps.</span><span class="sxs-lookup"><span data-stu-id="1abc0-116">Global Assembly Cache (GAC) – The GAC is not supported in Web Apps.</span></span> <span data-ttu-id="1abc0-117">If your application references assemblies which you usually deploy to the GAC, you will need to deploy to the application bin folder in Web Apps.</span><span class="sxs-lookup"><span data-stu-id="1abc0-117">If your application references assemblies which you usually deploy to the GAC, you will need to deploy to the application bin folder in Web Apps.</span></span> 
* <span data-ttu-id="1abc0-118">IIS5 Compatibility Mode – This is not supported in Web Apps.</span><span class="sxs-lookup"><span data-stu-id="1abc0-118">IIS5 Compatibility Mode – This is not supported in Web Apps.</span></span> 
* <span data-ttu-id="1abc0-119">Application Pools – In Web Apps, each site and its child applications run in the same application pool.</span><span class="sxs-lookup"><span data-stu-id="1abc0-119">Application Pools – In Web Apps, each site and its child applications run in the same application pool.</span></span> <span data-ttu-id="1abc0-120">If your site has multiple child applications utilizing multiple application pools, consolidate them to a single application pool with common settings or migrate each application to a separate web app.</span><span class="sxs-lookup"><span data-stu-id="1abc0-120">If your site has multiple child applications utilizing multiple application pools, consolidate them to a single application pool with common settings or migrate each application to a separate web app.</span></span>
* <span data-ttu-id="1abc0-121">COM Components – Web Apps does not allow the registration of COM Components on the platform.</span><span class="sxs-lookup"><span data-stu-id="1abc0-121">COM Components – Web Apps does not allow the registration of COM Components on the platform.</span></span> <span data-ttu-id="1abc0-122">If your websites or applications make use of any COM Components, you must rewrite them in managed code and deploy them with the website or application.</span><span class="sxs-lookup"><span data-stu-id="1abc0-122">If your websites or applications make use of any COM Components, you must rewrite them in managed code and deploy them with the website or application.</span></span>
* <span data-ttu-id="1abc0-123">ISAPI Extensions – Web Apps can support the use of ISAPI Extensions.</span><span class="sxs-lookup"><span data-stu-id="1abc0-123">ISAPI Extensions – Web Apps can support the use of ISAPI Extensions.</span></span> <span data-ttu-id="1abc0-124">You need to do the following:</span><span class="sxs-lookup"><span data-stu-id="1abc0-124">You need to do the following:</span></span>
  
  * <span data-ttu-id="1abc0-125">deploy the DLLs with your web app</span><span class="sxs-lookup"><span data-stu-id="1abc0-125">deploy the DLLs with your web app</span></span> 
  * <span data-ttu-id="1abc0-126">register the DLLs using [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)</span><span class="sxs-lookup"><span data-stu-id="1abc0-126">register the DLLs using [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)</span></span>
  * <span data-ttu-id="1abc0-127">place an applicationHost.xdt file in the site root with the content outlined in "Allowing arbitrart ISAPI extensions to be loaded" [section of this article](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)</span><span class="sxs-lookup"><span data-stu-id="1abc0-127">place an applicationHost.xdt file in the site root with the content outlined in "Allowing arbitrart ISAPI extensions to be loaded" [section of this article](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)</span></span> 
    
  
    
    <span data-ttu-id="1abc0-128">For more examples of how to use XML Document Transformations with your website, see [Transform your Microsoft Azure Web Site](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).</span><span class="sxs-lookup"><span data-stu-id="1abc0-128">For more examples of how to use XML Document Transformations with your website, see [Transform your Microsoft Azure Web Site](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).</span></span>
* <span data-ttu-id="1abc0-129">Other components like SharePoint, front page server extensions (FPSE), FTP, SSL certificates will not be migrated.</span><span class="sxs-lookup"><span data-stu-id="1abc0-129">Other components like SharePoint, front page server extensions (FPSE), FTP, SSL certificates will not be migrated.</span></span>

## <a name="how-to-use-the-web-apps-migration-assistant"></a><span data-ttu-id="1abc0-130">How to use the Web Apps Migration Assistant</span><span class="sxs-lookup"><span data-stu-id="1abc0-130">How to use the Web Apps Migration Assistant</span></span>
<span data-ttu-id="1abc0-131">This section steps through an example to to migrate a few websites that use a SQL Server database and running on an on-premise Windows Server 2003 R2 (IIS 6.0) machine:</span><span class="sxs-lookup"><span data-stu-id="1abc0-131">This section steps through an example to to migrate a few websites that use a SQL Server database and running on an on-premise Windows Server 2003 R2 (IIS 6.0) machine:</span></span>

1. <span data-ttu-id="1abc0-132">On the IIS server or your client machine navigate to [https://www.movemetothecloud.net/](https://www.movemetothecloud.net/)</span><span class="sxs-lookup"><span data-stu-id="1abc0-132">On the IIS server or your client machine navigate to [https://www.movemetothecloud.net/](https://www.movemetothecloud.net/)</span></span> 
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. <span data-ttu-id="1abc0-133">Install Web Apps Migration Assistant by clicking on the **Dedicated IIS Server** button.</span><span class="sxs-lookup"><span data-stu-id="1abc0-133">Install Web Apps Migration Assistant by clicking on the **Dedicated IIS Server** button.</span></span> <span data-ttu-id="1abc0-134">More options will be options in the near future.</span><span class="sxs-lookup"><span data-stu-id="1abc0-134">More options will be options in the near future.</span></span> 
3. <span data-ttu-id="1abc0-135">Click the **Install Tool** button to install Web Apps Migration Assistant on your machine.</span><span class="sxs-lookup"><span data-stu-id="1abc0-135">Click the **Install Tool** button to install Web Apps Migration Assistant on your machine.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > <span data-ttu-id="1abc0-136">You can also click **Download for offline install** to download a ZIP file for installing on servers not connected to the internet.</span><span class="sxs-lookup"><span data-stu-id="1abc0-136">You can also click **Download for offline install** to download a ZIP file for installing on servers not connected to the internet.</span></span> <span data-ttu-id="1abc0-137">Or, you can click **Upload an existing migration readiness report**, which is an advanced option to work with an existing migration readiness report that you previously generated (explained later).</span><span class="sxs-lookup"><span data-stu-id="1abc0-137">Or, you can click **Upload an existing migration readiness report**, which is an advanced option to work with an existing migration readiness report that you previously generated (explained later).</span></span>
   > 
   > 
4. <span data-ttu-id="1abc0-138">In the **Application Install** screen, click **Install** to install on your machine.</span><span class="sxs-lookup"><span data-stu-id="1abc0-138">In the **Application Install** screen, click **Install** to install on your machine.</span></span> <span data-ttu-id="1abc0-139">It will also install corresponding dependencies like Web Deploy, DacFX, and IIS, if needed.</span><span class="sxs-lookup"><span data-stu-id="1abc0-139">It will also install corresponding dependencies like Web Deploy, DacFX, and IIS, if needed.</span></span> 
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-migration-from-iis-server/install-progress.png)
   
   <span data-ttu-id="1abc0-140">Once installed, Web Apps Migration Assistant automatically starts.</span><span class="sxs-lookup"><span data-stu-id="1abc0-140">Once installed, Web Apps Migration Assistant automatically starts.</span></span>
5. <span data-ttu-id="1abc0-141">Choose **Migrate sites and databases from a remote server to Azure**.</span><span class="sxs-lookup"><span data-stu-id="1abc0-141">Choose **Migrate sites and databases from a remote server to Azure**.</span></span> <span data-ttu-id="1abc0-142">Enter the administrative credentials for the remote server and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="1abc0-142">Enter the administrative credentials for the remote server and click **Continue**.</span></span> 
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   <span data-ttu-id="1abc0-143">You can of course choose to migrate from the local server.</span><span class="sxs-lookup"><span data-stu-id="1abc0-143">You can of course choose to migrate from the local server.</span></span> <span data-ttu-id="1abc0-144">The remote option is useful when you want to migrate websites from a production IIS server.</span><span class="sxs-lookup"><span data-stu-id="1abc0-144">The remote option is useful when you want to migrate websites from a production IIS server.</span></span>
   
   <span data-ttu-id="1abc0-145">At this point the migration tool will inspect the your IIS server's configuration, such as Sites, Applications, Application Pools, and dependencies to identify candidate websites for migration.</span><span class="sxs-lookup"><span data-stu-id="1abc0-145">At this point the migration tool will inspect the your IIS server's configuration, such as Sites, Applications, Application Pools, and dependencies to identify candidate websites for migration.</span></span> 
6. <span data-ttu-id="1abc0-146">The screenshot below shows three websites – **Default Web Site**, **TimeTracker**, and **CommerceNet4**.</span><span class="sxs-lookup"><span data-stu-id="1abc0-146">The screenshot below shows three websites – **Default Web Site**, **TimeTracker**, and **CommerceNet4**.</span></span> <span data-ttu-id="1abc0-147">All of them have an associated database that we want to migrate.</span><span class="sxs-lookup"><span data-stu-id="1abc0-147">All of them have an associated database that we want to migrate.</span></span> <span data-ttu-id="1abc0-148">Select all of the sites you would like to assess and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1abc0-148">Select all of the sites you would like to assess and then click **Next**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. <span data-ttu-id="1abc0-149">Click **Upload** to upload the readiness report.</span><span class="sxs-lookup"><span data-stu-id="1abc0-149">Click **Upload** to upload the readiness report.</span></span> <span data-ttu-id="1abc0-150">If you click **save file locally**, you can run the migration tool again later and upload the saved readiness report as noted earlier.</span><span class="sxs-lookup"><span data-stu-id="1abc0-150">If you click **save file locally**, you can run the migration tool again later and upload the saved readiness report as noted earlier.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   <span data-ttu-id="1abc0-151">Once you upload the readiness report, Azure performs readiness analysis and shows you the results.</span><span class="sxs-lookup"><span data-stu-id="1abc0-151">Once you upload the readiness report, Azure performs readiness analysis and shows you the results.</span></span> <span data-ttu-id="1abc0-152">Read the assessment details for each website and make sure that you understand or have addressed all issues before you proceed.</span><span class="sxs-lookup"><span data-stu-id="1abc0-152">Read the assessment details for each website and make sure that you understand or have addressed all issues before you proceed.</span></span> 
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. <span data-ttu-id="1abc0-153">Click **Begin Migration** to start the migration.You will now be redirected to Azure to log into your account.</span><span class="sxs-lookup"><span data-stu-id="1abc0-153">Click **Begin Migration** to start the migration.You will now be redirected to Azure to log into your account.</span></span> <span data-ttu-id="1abc0-154">It is important that you log in with an account that has an active Azure Subscription.</span><span class="sxs-lookup"><span data-stu-id="1abc0-154">It is important that you log in with an account that has an active Azure Subscription.</span></span> <span data-ttu-id="1abc0-155">If you do not have an Azure account then you can sign up for a free trial [here](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_).</span><span class="sxs-lookup"><span data-stu-id="1abc0-155">If you do not have an Azure account then you can sign up for a free trial [here](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_).</span></span> 
9. <span data-ttu-id="1abc0-156">Select the tenant account, Azure subscription and region to use for your migrated Azure web apps and databases, and then click **Start Migration**.</span><span class="sxs-lookup"><span data-stu-id="1abc0-156">Select the tenant account, Azure subscription and region to use for your migrated Azure web apps and databases, and then click **Start Migration**.</span></span> <span data-ttu-id="1abc0-157">You can select the websites to migrate later.</span><span class="sxs-lookup"><span data-stu-id="1abc0-157">You can select the websites to migrate later.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. <span data-ttu-id="1abc0-158">On the next screen you can make changes to the default migration settings, such as:</span><span class="sxs-lookup"><span data-stu-id="1abc0-158">On the next screen you can make changes to the default migration settings, such as:</span></span>
    
    * <span data-ttu-id="1abc0-159">use an existing Azure SQL Database or create a new Azure SQL Database, and configure its credentials</span><span class="sxs-lookup"><span data-stu-id="1abc0-159">use an existing Azure SQL Database or create a new Azure SQL Database, and configure its credentials</span></span>
    * <span data-ttu-id="1abc0-160">select the websites to migrate</span><span class="sxs-lookup"><span data-stu-id="1abc0-160">select the websites to migrate</span></span>
    * <span data-ttu-id="1abc0-161">define names for the Azure web apps and their linked SQL databases</span><span class="sxs-lookup"><span data-stu-id="1abc0-161">define names for the Azure web apps and their linked SQL databases</span></span>
    * <span data-ttu-id="1abc0-162">customize the global settings and site-level settings</span><span class="sxs-lookup"><span data-stu-id="1abc0-162">customize the global settings and site-level settings</span></span>
    
    <span data-ttu-id="1abc0-163">The screenshot below shows all the websites selected for migration with the default settings.</span><span class="sxs-lookup"><span data-stu-id="1abc0-163">The screenshot below shows all the websites selected for migration with the default settings.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > <span data-ttu-id="1abc0-164">the **Enable Azure Active Directory** checkbox in custom settings integrates the Azure web app with [Azure Active Directory](../active-directory/active-directory-whatis.md) (the **Default Directory**).</span><span class="sxs-lookup"><span data-stu-id="1abc0-164">the **Enable Azure Active Directory** checkbox in custom settings integrates the Azure web app with [Azure Active Directory](../active-directory/active-directory-whatis.md) (the **Default Directory**).</span></span> <span data-ttu-id="1abc0-165">For more information on syncing Azure Active Directory with your on-premise Active Directory, see [Directory integration](http://msdn.microsoft.com/library/jj573653).</span><span class="sxs-lookup"><span data-stu-id="1abc0-165">For more information on syncing Azure Active Directory with your on-premise Active Directory, see [Directory integration](http://msdn.microsoft.com/library/jj573653).</span></span>
    > 
    > 
11. <span data-ttu-id="1abc0-166">Once you make all the desired changes, click **Create** to start the migration process.</span><span class="sxs-lookup"><span data-stu-id="1abc0-166">Once you make all the desired changes, click **Create** to start the migration process.</span></span> <span data-ttu-id="1abc0-167">The migration tool will create the Azure SQL Database and Azure web app, and then publish the website content and databases.</span><span class="sxs-lookup"><span data-stu-id="1abc0-167">The migration tool will create the Azure SQL Database and Azure web app, and then publish the website content and databases.</span></span> <span data-ttu-id="1abc0-168">The migration progress is clearly shown in the migration tool, and you will see a summary screen at the end, which details the sites migrated, whether they were successful, links to the newly-created Azure web apps.</span><span class="sxs-lookup"><span data-stu-id="1abc0-168">The migration progress is clearly shown in the migration tool, and you will see a summary screen at the end, which details the sites migrated, whether they were successful, links to the newly-created Azure web apps.</span></span> 
    
    <span data-ttu-id="1abc0-169">If any error occurs during migration, the migration tool will clearly indicate the failure and rollback the changes.</span><span class="sxs-lookup"><span data-stu-id="1abc0-169">If any error occurs during migration, the migration tool will clearly indicate the failure and rollback the changes.</span></span> <span data-ttu-id="1abc0-170">You will also be able to send the error report directly to the engineering team by clicking the **Send Error Report** button, with the captured failure call stack and build message body.</span><span class="sxs-lookup"><span data-stu-id="1abc0-170">You will also be able to send the error report directly to the engineering team by clicking the **Send Error Report** button, with the captured failure call stack and build message body.</span></span> 
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    <span data-ttu-id="1abc0-171">If migrate succeeds without errors, you can also click the **Give Feedback** button to provide any feedback directly.</span><span class="sxs-lookup"><span data-stu-id="1abc0-171">If migrate succeeds without errors, you can also click the **Give Feedback** button to provide any feedback directly.</span></span> 
12. <span data-ttu-id="1abc0-172">Click the links to the Azure web apps and verify that the migration has succeeded.</span><span class="sxs-lookup"><span data-stu-id="1abc0-172">Click the links to the Azure web apps and verify that the migration has succeeded.</span></span>
13. <span data-ttu-id="1abc0-173">You can now manage the migrated web apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="1abc0-173">You can now manage the migrated web apps in Azure App Service.</span></span> <span data-ttu-id="1abc0-174">To do this, log into the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1abc0-174">To do this, log into the [Azure Portal](https://portal.azure.com).</span></span>
14. <span data-ttu-id="1abc0-175">In the Azure Portal, open the Web Apps blade to see your migrated websites (shown as web apps), then click on any one of them to start managing the web app, such as configuring continuous publishing, creating backups, autoscaling, and monitoring usage or performance.</span><span class="sxs-lookup"><span data-stu-id="1abc0-175">In the Azure Portal, open the Web Apps blade to see your migrated websites (shown as web apps), then click on any one of them to start managing the web app, such as configuring continuous publishing, creating backups, autoscaling, and monitoring usage or performance.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> <span data-ttu-id="1abc0-176">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="1abc0-176">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1abc0-177">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="1abc0-177">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="1abc0-178">What's changed</span><span class="sxs-lookup"><span data-stu-id="1abc0-178">What's changed</span></span>
* <span data-ttu-id="1abc0-179">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="1abc0-179">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>












