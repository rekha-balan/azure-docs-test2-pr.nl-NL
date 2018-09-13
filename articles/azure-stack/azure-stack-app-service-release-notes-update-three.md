---
title: App Service on Azure Stack update 3 release notes | Microsoft Docs
description: Learn about what's in update three for App Service on Azure Stack, the known issues, and where to download the update.
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/20/2018
ms.author: anwestg
ms.reviewer: brenduns
ms.openlocfilehash: f825a2a343d9b5ad8f9802042b7aca2ba1544dfb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871442"
---
# <a name="app-service-on-azure-stack-update-3-release-notes"></a><span data-ttu-id="a460e-103">App Service on Azure Stack update 3 release notes</span><span class="sxs-lookup"><span data-stu-id="a460e-103">App Service on Azure Stack update 3 release notes</span></span>

<span data-ttu-id="a460e-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="a460e-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="a460e-105">These release notes describe the improvements and fixes in Azure App Service on Azure Stack Update 3 and any known issues.</span><span class="sxs-lookup"><span data-stu-id="a460e-105">These release notes describe the improvements and fixes in Azure App Service on Azure Stack Update 3 and any known issues.</span></span> <span data-ttu-id="a460e-106">Known issues are divided into issues directly related to the deployment, update process, and issues with the build (post-installation).</span><span class="sxs-lookup"><span data-stu-id="a460e-106">Known issues are divided into issues directly related to the deployment, update process, and issues with the build (post-installation).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a460e-107">Apply the 1807 update to your Azure Stack integrated system or deploy the latest Azure Stack development kit before deploying Azure App Service 1.3.</span><span class="sxs-lookup"><span data-stu-id="a460e-107">Apply the 1807 update to your Azure Stack integrated system or deploy the latest Azure Stack development kit before deploying Azure App Service 1.3.</span></span>
>
>

## <a name="build-reference"></a><span data-ttu-id="a460e-108">Build reference</span><span class="sxs-lookup"><span data-stu-id="a460e-108">Build reference</span></span>

<span data-ttu-id="a460e-109">The App Service on Azure Stack Update 3 build number is **74.0.13698.31**</span><span class="sxs-lookup"><span data-stu-id="a460e-109">The App Service on Azure Stack Update 3 build number is **74.0.13698.31**</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a460e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a460e-110">Prerequisites</span></span>

<span data-ttu-id="a460e-111">Refer to the [Before You Get Started documentation](azure-stack-app-service-before-you-get-started.md) before beginning deployment.</span><span class="sxs-lookup"><span data-stu-id="a460e-111">Refer to the [Before You Get Started documentation](azure-stack-app-service-before-you-get-started.md) before beginning deployment.</span></span>

<span data-ttu-id="a460e-112">Before you begin the upgrade of Azure App Service on Azure Stack to 1.3, ensure all roles are Ready in the Azure App Service Administration in the Azure Stack Admin Portal</span><span class="sxs-lookup"><span data-stu-id="a460e-112">Before you begin the upgrade of Azure App Service on Azure Stack to 1.3, ensure all roles are Ready in the Azure App Service Administration in the Azure Stack Admin Portal</span></span>

![App Service role status](media/azure-stack-app-service-release-notes-update-three/image01.png)

### <a name="new-features-and-fixes"></a><span data-ttu-id="a460e-114">New features and fixes</span><span class="sxs-lookup"><span data-stu-id="a460e-114">New features and fixes</span></span>

<span data-ttu-id="a460e-115">Azure App Service on Azure Stack Update 3 includes the following improvements and fixes:</span><span class="sxs-lookup"><span data-stu-id="a460e-115">Azure App Service on Azure Stack Update 3 includes the following improvements and fixes:</span></span>

- <span data-ttu-id="a460e-116">Support for use of SQL Server Always On for Azure App Service Resource Provider databases.</span><span class="sxs-lookup"><span data-stu-id="a460e-116">Support for use of SQL Server Always On for Azure App Service Resource Provider databases.</span></span>

- <span data-ttu-id="a460e-117">Added new Environment parameter to the Create-AADIdentityApp helper script to assist targeting different AAD regions.</span><span class="sxs-lookup"><span data-stu-id="a460e-117">Added new Environment parameter to the Create-AADIdentityApp helper script to assist targeting different AAD regions.</span></span>

- <span data-ttu-id="a460e-118">Updates to **App Service Tenant, Admin, Functions portals and Kudu tools**.</span><span class="sxs-lookup"><span data-stu-id="a460e-118">Updates to **App Service Tenant, Admin, Functions portals and Kudu tools**.</span></span> <span data-ttu-id="a460e-119">Consistent with Azure Stack Portal SDK version.</span><span class="sxs-lookup"><span data-stu-id="a460e-119">Consistent with Azure Stack Portal SDK version.</span></span>

- <span data-ttu-id="a460e-120">Updates to core service to improve reliability and error messaging enabling easier diagnosis of common issues.</span><span class="sxs-lookup"><span data-stu-id="a460e-120">Updates to core service to improve reliability and error messaging enabling easier diagnosis of common issues.</span></span>

- <span data-ttu-id="a460e-121">**Updates to the following application frameworks and tools**:</span><span class="sxs-lookup"><span data-stu-id="a460e-121">**Updates to the following application frameworks and tools**:</span></span>
  - <span data-ttu-id="a460e-122">Added ASP.Net Core 2.1.2</span><span class="sxs-lookup"><span data-stu-id="a460e-122">Added ASP.Net Core 2.1.2</span></span>
  - <span data-ttu-id="a460e-123">Added NodeJS 10.0.0</span><span class="sxs-lookup"><span data-stu-id="a460e-123">Added NodeJS 10.0.0</span></span>
  - <span data-ttu-id="a460e-124">Added Zulu OpenJDK 8.30.0.1</span><span class="sxs-lookup"><span data-stu-id="a460e-124">Added Zulu OpenJDK 8.30.0.1</span></span>
  - <span data-ttu-id="a460e-125">Added Tomcat 8.5.31 and 9.0.8</span><span class="sxs-lookup"><span data-stu-id="a460e-125">Added Tomcat 8.5.31 and 9.0.8</span></span>
  - <span data-ttu-id="a460e-126">Added PHP Versions:</span><span class="sxs-lookup"><span data-stu-id="a460e-126">Added PHP Versions:</span></span>
    - <span data-ttu-id="a460e-127">5.6.36</span><span class="sxs-lookup"><span data-stu-id="a460e-127">5.6.36</span></span>
    - <span data-ttu-id="a460e-128">7.0.30</span><span class="sxs-lookup"><span data-stu-id="a460e-128">7.0.30</span></span>
    - <span data-ttu-id="a460e-129">7.1.17</span><span class="sxs-lookup"><span data-stu-id="a460e-129">7.1.17</span></span>
    - <span data-ttu-id="a460e-130">7.2.5</span><span class="sxs-lookup"><span data-stu-id="a460e-130">7.2.5</span></span>
  - <span data-ttu-id="a460e-131">Added Wincache 2.0.0.8</span><span class="sxs-lookup"><span data-stu-id="a460e-131">Added Wincache 2.0.0.8</span></span>
  - <span data-ttu-id="a460e-132">Updated Git for Windows to v 2.17.1.2</span><span class="sxs-lookup"><span data-stu-id="a460e-132">Updated Git for Windows to v 2.17.1.2</span></span>
  - <span data-ttu-id="a460e-133">Updated Kudu to 74.10611.3437</span><span class="sxs-lookup"><span data-stu-id="a460e-133">Updated Kudu to 74.10611.3437</span></span>
  
- <span data-ttu-id="a460e-134">**Updates to underlying operating system of all roles**:</span><span class="sxs-lookup"><span data-stu-id="a460e-134">**Updates to underlying operating system of all roles**:</span></span>
  - [<span data-ttu-id="a460e-135">Servicing stack update for Windows Server 2016 for x64-based Systems (KB4132216)</span><span class="sxs-lookup"><span data-stu-id="a460e-135">Servicing stack update for Windows Server 2016 for x64-based Systems (KB4132216)</span></span>](https://support.microsoft.com/help/4132216/servicing-stack-update-for-windows-10-1607-may-17-2018)
  - [<span data-ttu-id="a460e-136">2018-07 Cumulative Update for Windows Server 2016 for x64-based Systems (KB4338822)</span><span class="sxs-lookup"><span data-stu-id="a460e-136">2018-07 Cumulative Update for Windows Server 2016 for x64-based Systems (KB4338822)</span></span>](https://support.microsoft.com/help/4338822/windows-10-update-kb4338822)

### <a name="post-update-steps-optional"></a><span data-ttu-id="a460e-137">Post Update Steps (optional)</span><span class="sxs-lookup"><span data-stu-id="a460e-137">Post Update Steps (optional)</span></span>

<span data-ttu-id="a460e-138">For customers wishing to migrate to contained database for existing Azure App Service on Azure Stack deployments, execute these steps after the Azure App Service on Azure Stack 1.3 update has completed:</span><span class="sxs-lookup"><span data-stu-id="a460e-138">For customers wishing to migrate to contained database for existing Azure App Service on Azure Stack deployments, execute these steps after the Azure App Service on Azure Stack 1.3 update has completed:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a460e-139">This procedure takes approximately 5-10 minutes.</span><span class="sxs-lookup"><span data-stu-id="a460e-139">This procedure takes approximately 5-10 minutes.</span></span>  <span data-ttu-id="a460e-140">This procedure involves killing the existing database login sessions.</span><span class="sxs-lookup"><span data-stu-id="a460e-140">This procedure involves killing the existing database login sessions.</span></span>  <span data-ttu-id="a460e-141">Plan for downtime to migrate and validate Azure App Service on Azure Stack post migration</span><span class="sxs-lookup"><span data-stu-id="a460e-141">Plan for downtime to migrate and validate Azure App Service on Azure Stack post migration</span></span>
>
>

1. <span data-ttu-id="a460e-142">Add [AppService databases (appservice_hosting and appservice_metering) to an Availability group](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/availability-group-add-a-database)</span><span class="sxs-lookup"><span data-stu-id="a460e-142">Add [AppService databases (appservice_hosting and appservice_metering) to an Availability group](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/availability-group-add-a-database)</span></span>

1. <span data-ttu-id="a460e-143">Enable contained database</span><span class="sxs-lookup"><span data-stu-id="a460e-143">Enable contained database</span></span>
    ```sql

        sp_configure 'contained database authentication', 1;
        GO
        RECONFIGURE;
            GO
    ```

1. <span data-ttu-id="a460e-144">Converting a Database to Partially Contained.</span><span class="sxs-lookup"><span data-stu-id="a460e-144">Converting a Database to Partially Contained.</span></span>  <span data-ttu-id="a460e-145">This step will incur downtime as all active sessions need to be killed</span><span class="sxs-lookup"><span data-stu-id="a460e-145">This step will incur downtime as all active sessions need to be killed</span></span>

    ```sql
        /******** [appservice_metering] Migration Start********/
            USE [master];

            -- kill all active sessions
            DECLARE @kill varchar(8000) = '';  
            SELECT @kill = @kill + 'kill ' + CONVERT(varchar(5), session_id) + ';'  
            FROM sys.dm_exec_sessions
            WHERE database_id  = db_id('appservice_metering')

            EXEC(@kill);

            USE [master]  
            GO  
            ALTER DATABASE [appservice_metering] SET CONTAINMENT = PARTIAL  
            GO  

        /********[appservice_metering] Migration End********/

        /********[appservice_hosting] Migration Start********/

            -- kill all active sessions
            USE [master];

            DECLARE @kill varchar(8000) = '';  
            SELECT @kill = @kill + 'kill ' + CONVERT(varchar(5), session_id) + ';'  
            FROM sys.dm_exec_sessions
            WHERE database_id  = db_id('appservice_hosting')

            EXEC(@kill);

            -- Convert database to contained
            USE [master]  
            GO  
            ALTER DATABASE [appservice_hosting] SET CONTAINMENT = PARTIAL  
            GO  

            /********[appservice_hosting] Migration End********/
    '''

1. Migrate Logins to Contained Database Users

    ```sql
        IF EXISTS(SELECT * FROM sys.databases WHERE Name=DB_NAME() AND containment = 1)
        BEGIN
        DECLARE @username sysname ;  
        DECLARE user_cursor CURSOR  
        FOR
            SELECT dp.name
            FROM sys.database_principals AS dp  
            JOIN sys.server_principals AS sp
                ON dp.sid = sp.sid  
                WHERE dp.authentication_type = 1 AND dp.name NOT IN ('dbo','sys','guest','INFORMATION_SCHEMA');
            OPEN user_cursor  
            FETCH NEXT FROM user_cursor INTO @username  
                WHILE @@FETCH_STATUS = 0  
                BEGIN  
                    EXECUTE sp_migrate_user_to_contained
                    @username = @username,  
                    @rename = N'copy_login_name',  
                    @disablelogin = N'do_not_disable_login';  
                FETCH NEXT FROM user_cursor INTO @username  
            END  
            CLOSE user_cursor ;  
            DEALLOCATE user_cursor ;
            END
        GO
    ```

<span data-ttu-id="a460e-146">Validate</span><span class="sxs-lookup"><span data-stu-id="a460e-146">Validate</span></span>

1. <span data-ttu-id="a460e-147">Check if SQL Server has containment enabled</span><span class="sxs-lookup"><span data-stu-id="a460e-147">Check if SQL Server has containment enabled</span></span>

    ```sql
        sp_configure  @configname='contained database authentication'
    ```

1. <span data-ttu-id="a460e-148">Check existing contained behavior</span><span class="sxs-lookup"><span data-stu-id="a460e-148">Check existing contained behavior</span></span>
    ```sql
        SELECT containment FROM sys.databases WHERE NAME LIKE (SELECT DB_NAME())
    ```

### <a name="known-issues-post-installation"></a><span data-ttu-id="a460e-149">Known issues (post-installation)</span><span class="sxs-lookup"><span data-stu-id="a460e-149">Known issues (post-installation)</span></span>

- <span data-ttu-id="a460e-150">Workers are unable to reach file server when App Service is deployed in an existing virtual network and the file server is only available on the private network.</span><span class="sxs-lookup"><span data-stu-id="a460e-150">Workers are unable to reach file server when App Service is deployed in an existing virtual network and the file server is only available on the private network.</span></span>  <span data-ttu-id="a460e-151">This is also called out in the Azure App Service on Azure Stack deployment documentation.</span><span class="sxs-lookup"><span data-stu-id="a460e-151">This is also called out in the Azure App Service on Azure Stack deployment documentation.</span></span>

<span data-ttu-id="a460e-152">If you chose to deploy into an existing virtual network and an internal IP address to connect to your file server, you must add an outbound security rule, enabling SMB traffic between the worker subnet and the file server.</span><span class="sxs-lookup"><span data-stu-id="a460e-152">If you chose to deploy into an existing virtual network and an internal IP address to connect to your file server, you must add an outbound security rule, enabling SMB traffic between the worker subnet and the file server.</span></span> <span data-ttu-id="a460e-153">To do this, go to the WorkersNsg in the Admin Portal and add an outbound security rule with the following properties:</span><span class="sxs-lookup"><span data-stu-id="a460e-153">To do this, go to the WorkersNsg in the Admin Portal and add an outbound security rule with the following properties:</span></span>
 * <span data-ttu-id="a460e-154">Source: Any</span><span class="sxs-lookup"><span data-stu-id="a460e-154">Source: Any</span></span>
 * <span data-ttu-id="a460e-155">Source port range: \*</span><span class="sxs-lookup"><span data-stu-id="a460e-155">Source port range: \*</span></span>
 * <span data-ttu-id="a460e-156">Destination: IP Addresses</span><span class="sxs-lookup"><span data-stu-id="a460e-156">Destination: IP Addresses</span></span>
 * <span data-ttu-id="a460e-157">Destination IP address range: Range of IPs for your file server</span><span class="sxs-lookup"><span data-stu-id="a460e-157">Destination IP address range: Range of IPs for your file server</span></span>
 * <span data-ttu-id="a460e-158">Destination port range: 445</span><span class="sxs-lookup"><span data-stu-id="a460e-158">Destination port range: 445</span></span>
 * <span data-ttu-id="a460e-159">Protocol: TCP</span><span class="sxs-lookup"><span data-stu-id="a460e-159">Protocol: TCP</span></span>
 * <span data-ttu-id="a460e-160">Action: Allow</span><span class="sxs-lookup"><span data-stu-id="a460e-160">Action: Allow</span></span>
 * <span data-ttu-id="a460e-161">Priority: 700</span><span class="sxs-lookup"><span data-stu-id="a460e-161">Priority: 700</span></span>
 * <span data-ttu-id="a460e-162">Name: Outbound_Allow_SMB445</span><span class="sxs-lookup"><span data-stu-id="a460e-162">Name: Outbound_Allow_SMB445</span></span>

### <a name="known-issues-for-cloud-admins-operating-azure-app-service-on-azure-stack"></a><span data-ttu-id="a460e-163">Known issues for Cloud Admins operating Azure App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a460e-163">Known issues for Cloud Admins operating Azure App Service on Azure Stack</span></span>

<span data-ttu-id="a460e-164">Refer to the documentation in the [Azure Stack 1807 Release Notes](azure-stack-update-1807.md)</span><span class="sxs-lookup"><span data-stu-id="a460e-164">Refer to the documentation in the [Azure Stack 1807 Release Notes](azure-stack-update-1807.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a460e-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="a460e-165">Next steps</span></span>

- <span data-ttu-id="a460e-166">For an overview of Azure App Service, see [Azure App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a460e-166">For an overview of Azure App Service, see [Azure App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span></span>
- <span data-ttu-id="a460e-167">For more information about how to prepare to deploy App Service on Azure Stack, see [Before you get started with App Service on Azure Stack](azure-stack-app-service-before-you-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a460e-167">For more information about how to prepare to deploy App Service on Azure Stack, see [Before you get started with App Service on Azure Stack](azure-stack-app-service-before-you-get-started.md).</span></span>
