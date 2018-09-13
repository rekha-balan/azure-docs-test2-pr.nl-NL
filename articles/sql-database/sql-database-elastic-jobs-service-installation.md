---
title: Installing elastic database jobs | Microsoft Docs
description: Walk through installation of the elastic job feature.
services: sql-database
documentationcenter: ''
manager: jhubbard
author: ddove
editor: ''
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: multiple databases
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 97441fbdca9e0c046fa5fcf0b40eb72959cd6dbd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563591"
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="1c754-103">Installing Elastic Database jobs overview</span><span class="sxs-lookup"><span data-stu-id="1c754-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="1c754-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through the Azure Classic Portal.You can gain access to create and manage jobs using the PowerShell API only if you install the PowerShell package.</span><span class="sxs-lookup"><span data-stu-id="1c754-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through the Azure Classic Portal.You can gain access to create and manage jobs using the PowerShell API only if you install the PowerShell package.</span></span> <span data-ttu-id="1c754-105">Additionally, the PowerShell APIs provide significantly more functionality than the portal at this point in time.</span><span class="sxs-lookup"><span data-stu-id="1c754-105">Additionally, the PowerShell APIs provide significantly more functionality than the portal at this point in time.</span></span>

<span data-ttu-id="1c754-106">If you have already installed **Elastic Database jobs** through the Portal from an existing **elastic pool**, the latest Powershell preview includes scripts to upgrade your existing installation.</span><span class="sxs-lookup"><span data-stu-id="1c754-106">If you have already installed **Elastic Database jobs** through the Portal from an existing **elastic pool**, the latest Powershell preview includes scripts to upgrade your existing installation.</span></span> <span data-ttu-id="1c754-107">It is highly recommended to upgrade your installation to the latest **Elastic Database jobs** components in order to take advantage of new functionality exposed via the PowerShell APIs.</span><span class="sxs-lookup"><span data-stu-id="1c754-107">It is highly recommended to upgrade your installation to the latest **Elastic Database jobs** components in order to take advantage of new functionality exposed via the PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c754-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1c754-108">Prerequisites</span></span>
* <span data-ttu-id="1c754-109">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1c754-109">An Azure subscription.</span></span> <span data-ttu-id="1c754-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c754-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1c754-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c754-111">Azure PowerShell.</span></span> <span data-ttu-id="1c754-112">Install the latest version using the [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="1c754-112">Install the latest version using the [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="1c754-113">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="1c754-113">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="1c754-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used to install the Elastic Database jobs package.</span><span class="sxs-lookup"><span data-stu-id="1c754-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used to install the Elastic Database jobs package.</span></span> <span data-ttu-id="1c754-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span><span class="sxs-lookup"><span data-stu-id="1c754-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-the-elastic-database-jobs-powershell-package"></a><span data-ttu-id="1c754-116">Download and import the Elastic Database jobs PowerShell package</span><span class="sxs-lookup"><span data-stu-id="1c754-116">Download and import the Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="1c754-117">Launch Microsoft Azure PowerShell command window and navigate to the directory where you downloaded NuGet Command-line Utility (nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="1c754-117">Launch Microsoft Azure PowerShell command window and navigate to the directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="1c754-118">Download and import **Elastic Database jobs** package into the current directory with the following command:</span><span class="sxs-lookup"><span data-stu-id="1c754-118">Download and import **Elastic Database jobs** package into the current directory with the following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="1c754-119">The **Elastic Database jobs** files are placed in the local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects the version number.</span><span class="sxs-lookup"><span data-stu-id="1c754-119">The **Elastic Database jobs** files are placed in the local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects the version number.</span></span> <span data-ttu-id="1c754-120">The PowerShell cmdlets (including required client .dlls) are located in the **tools\ElasticDatabaseJobs** sub-directory and the PowerShell scripts to install, upgrade and uninstall also reside in the **tools** sub-directory.</span><span class="sxs-lookup"><span data-stu-id="1c754-120">The PowerShell cmdlets (including required client .dlls) are located in the **tools\ElasticDatabaseJobs** sub-directory and the PowerShell scripts to install, upgrade and uninstall also reside in the **tools** sub-directory.</span></span>
3. <span data-ttu-id="1c754-121">Navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span><span class="sxs-lookup"><span data-stu-id="1c754-121">Navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="1c754-122">Execute the .\InstallElasticDatabaseJobsCmdlets.ps1 script to copy the ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span><span class="sxs-lookup"><span data-stu-id="1c754-122">Execute the .\InstallElasticDatabaseJobsCmdlets.ps1 script to copy the ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="1c754-123">This will also automatically import the module for use, for example:</span><span class="sxs-lookup"><span data-stu-id="1c754-123">This will also automatically import the module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-the-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="1c754-124">Install the Elastic Database jobs components using PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c754-124">Install the Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="1c754-125">Launch a Microsoft Azure PowerShell command window and navigate to the \tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span><span class="sxs-lookup"><span data-stu-id="1c754-125">Launch a Microsoft Azure PowerShell command window and navigate to the \tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="1c754-126">Execute the .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span><span class="sxs-lookup"><span data-stu-id="1c754-126">Execute the .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="1c754-127">This script will create the components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring the Azure Cloud Service to appropriately use the dependent components.</span><span class="sxs-lookup"><span data-stu-id="1c754-127">This script will create the components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring the Azure Cloud Service to appropriately use the dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="1c754-128">When you run this command a window opens asking for a **user name** and **password**.</span><span class="sxs-lookup"><span data-stu-id="1c754-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="1c754-129">This is not your Azure credentials, enter the user name and password that will be the administrator credentials you want to create for the new server.</span><span class="sxs-lookup"><span data-stu-id="1c754-129">This is not your Azure credentials, enter the user name and password that will be the administrator credentials you want to create for the new server.</span></span>

<span data-ttu-id="1c754-130">The parameters provided on this sample invocation can be modified for your desired settings.</span><span class="sxs-lookup"><span data-stu-id="1c754-130">The parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="1c754-131">The following provides more information on the behavior of each parameter:</span><span class="sxs-lookup"><span data-stu-id="1c754-131">The following provides more information on the behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="1c754-132">Parameter</span><span class="sxs-lookup"><span data-stu-id="1c754-132">Parameter</span></span></th>
    <th><span data-ttu-id="1c754-133">Description</span><span class="sxs-lookup"><span data-stu-id="1c754-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="1c754-134">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="1c754-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="1c754-135">Provides the Azure resource group name created to contain the newly created Azure components.</span><span class="sxs-lookup"><span data-stu-id="1c754-135">Provides the Azure resource group name created to contain the newly created Azure components.</span></span> <span data-ttu-id="1c754-136">This parameter defaults to “__ElasticDatabaseJob”.</span><span class="sxs-lookup"><span data-stu-id="1c754-136">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="1c754-137">It is not recommended to change this value.</span><span class="sxs-lookup"><span data-stu-id="1c754-137">It is not recommended to change this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="1c754-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="1c754-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="1c754-139">Provides the Azure location to be used for the newly created Azure components.</span><span class="sxs-lookup"><span data-stu-id="1c754-139">Provides the Azure location to be used for the newly created Azure components.</span></span> <span data-ttu-id="1c754-140">This parameter defaults to the Central US location.</span><span class="sxs-lookup"><span data-stu-id="1c754-140">This parameter defaults to the Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="1c754-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="1c754-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="1c754-142">Provides the number of service workers to install.</span><span class="sxs-lookup"><span data-stu-id="1c754-142">Provides the number of service workers to install.</span></span> <span data-ttu-id="1c754-143">This parameter defaults to 1.</span><span class="sxs-lookup"><span data-stu-id="1c754-143">This parameter defaults to 1.</span></span> <span data-ttu-id="1c754-144">A higher number of workers can be used to scale out the service and to provide high availability.</span><span class="sxs-lookup"><span data-stu-id="1c754-144">A higher number of workers can be used to scale out the service and to provide high availability.</span></span> <span data-ttu-id="1c754-145">It is recommended to use “2” for deployments that require high availability of the service.</span><span class="sxs-lookup"><span data-stu-id="1c754-145">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="1c754-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="1c754-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="1c754-147">Provides the VM size for usage within the Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="1c754-147">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="1c754-148">This parameter defaults to A0.</span><span class="sxs-lookup"><span data-stu-id="1c754-148">This parameter defaults to A0.</span></span> <span data-ttu-id="1c754-149">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span><span class="sxs-lookup"><span data-stu-id="1c754-149">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="1c754-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="1c754-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="1c754-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="1c754-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="1c754-152">Provides the service level objective for a Standard edition.</span><span class="sxs-lookup"><span data-stu-id="1c754-152">Provides the service level objective for a Standard edition.</span></span> <span data-ttu-id="1c754-153">This parameter defaults to S0.</span><span class="sxs-lookup"><span data-stu-id="1c754-153">This parameter defaults to S0.</span></span> <span data-ttu-id="1c754-154">Parameter values of S0/S1/S2/S3 are accepted which cause the Azure SQL Database to use the respective SLO.</span><span class="sxs-lookup"><span data-stu-id="1c754-154">Parameter values of S0/S1/S2/S3 are accepted which cause the Azure SQL Database to use the respective SLO.</span></span> <span data-ttu-id="1c754-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="1c754-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="1c754-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="1c754-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="1c754-157">Provides the admin user name for the newly created Azure SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="1c754-157">Provides the admin user name for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="1c754-158">When not specified, a PowerShell credentials window will open to prompt for the credentials.</span><span class="sxs-lookup"><span data-stu-id="1c754-158">When not specified, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="1c754-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="1c754-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="1c754-160">Provides the admin password for the newly created Azure SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="1c754-160">Provides the admin password for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="1c754-161">When not provided, a PowerShell credentials window will open to prompt for the credentials.</span><span class="sxs-lookup"><span data-stu-id="1c754-161">When not provided, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="1c754-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended to specify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="1c754-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended to specify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="1c754-163">Update an existing Elastic Database jobs components installation using PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c754-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="1c754-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span><span class="sxs-lookup"><span data-stu-id="1c754-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="1c754-165">This process allows for future upgrades of service code without having to drop and recreate the control database.</span><span class="sxs-lookup"><span data-stu-id="1c754-165">This process allows for future upgrades of service code without having to drop and recreate the control database.</span></span> <span data-ttu-id="1c754-166">This process can also be used within the same version to modify the service VM size or the server worker count.</span><span class="sxs-lookup"><span data-stu-id="1c754-166">This process can also be used within the same version to modify the service VM size or the server worker count.</span></span>

<span data-ttu-id="1c754-167">To update the VM size of an installation, run the following script with parameters updated to the values of your choice.</span><span class="sxs-lookup"><span data-stu-id="1c754-167">To update the VM size of an installation, run the following script with parameters updated to the values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="1c754-168">Parameter</span><span class="sxs-lookup"><span data-stu-id="1c754-168">Parameter</span></span></th>
  <th><span data-ttu-id="1c754-169">Description</span><span class="sxs-lookup"><span data-stu-id="1c754-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="1c754-170">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="1c754-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="1c754-171">Identifies the Azure resource group name used when the Elastic Database job components were initially installed.</span><span class="sxs-lookup"><span data-stu-id="1c754-171">Identifies the Azure resource group name used when the Elastic Database job components were initially installed.</span></span> <span data-ttu-id="1c754-172">This parameter defaults to “__ElasticDatabaseJob”.</span><span class="sxs-lookup"><span data-stu-id="1c754-172">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="1c754-173">Since it is not recommended to change this value, you shouldn't have to specify this parameter.</span><span class="sxs-lookup"><span data-stu-id="1c754-173">Since it is not recommended to change this value, you shouldn't have to specify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="1c754-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="1c754-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="1c754-175">Provides the number of service workers to install.</span><span class="sxs-lookup"><span data-stu-id="1c754-175">Provides the number of service workers to install.</span></span>  <span data-ttu-id="1c754-176">This parameter defaults to 1.</span><span class="sxs-lookup"><span data-stu-id="1c754-176">This parameter defaults to 1.</span></span>  <span data-ttu-id="1c754-177">A higher number of workers can be used to scale out the service and to provide high availability.</span><span class="sxs-lookup"><span data-stu-id="1c754-177">A higher number of workers can be used to scale out the service and to provide high availability.</span></span>  <span data-ttu-id="1c754-178">It is recommended to use “2” for deployments that require high availability of the service.</span><span class="sxs-lookup"><span data-stu-id="1c754-178">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="1c754-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="1c754-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="1c754-180">Provides the VM size for usage within the Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="1c754-180">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="1c754-181">This parameter defaults to A0.</span><span class="sxs-lookup"><span data-stu-id="1c754-181">This parameter defaults to A0.</span></span> <span data-ttu-id="1c754-182">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span><span class="sxs-lookup"><span data-stu-id="1c754-182">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="1c754-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="1c754-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-the-elastic-database-jobs-components-using-the-portal"></a><span data-ttu-id="1c754-184">Install the Elastic Database jobs components using the Portal</span><span class="sxs-lookup"><span data-stu-id="1c754-184">Install the Elastic Database jobs components using the Portal</span></span>
<span data-ttu-id="1c754-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components to enable execution of administrative tasks against each database in the elastic pool.</span><span class="sxs-lookup"><span data-stu-id="1c754-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components to enable execution of administrative tasks against each database in the elastic pool.</span></span> <span data-ttu-id="1c754-186">Unlike when using the **Elastic Database jobs** PowerShell APIs, the portal interface is currently restricted to only executing against an existing pool.</span><span class="sxs-lookup"><span data-stu-id="1c754-186">Unlike when using the **Elastic Database jobs** PowerShell APIs, the portal interface is currently restricted to only executing against an existing pool.</span></span>

<span data-ttu-id="1c754-187">**Estimated time to complete:** 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="1c754-187">**Estimated time to complete:** 10 minutes.</span></span>

1. <span data-ttu-id="1c754-188">From the dashboard view of the elastic pool via the [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span><span class="sxs-lookup"><span data-stu-id="1c754-188">From the dashboard view of the elastic pool via the [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="1c754-189">If you are creating a job for the first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span><span class="sxs-lookup"><span data-stu-id="1c754-189">If you are creating a job for the first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="1c754-190">Accept the terms by clicking the checkbox.</span><span class="sxs-lookup"><span data-stu-id="1c754-190">Accept the terms by clicking the checkbox.</span></span>
4. <span data-ttu-id="1c754-191">In the "Install services" view, click **JOB CREDENTIALS**.</span><span class="sxs-lookup"><span data-stu-id="1c754-191">In the "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![Installing the services][1]
5. <span data-ttu-id="1c754-193">Type a user name and password for a database admin. As part of the installation, a new Azure SQL Database server is created.</span><span class="sxs-lookup"><span data-stu-id="1c754-193">Type a user name and password for a database admin. As part of the installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="1c754-194">Within this new server, a new database, known as the control database, is created and used to contain the meta data for Elastic Database jobs.</span><span class="sxs-lookup"><span data-stu-id="1c754-194">Within this new server, a new database, known as the control database, is created and used to contain the meta data for Elastic Database jobs.</span></span> <span data-ttu-id="1c754-195">The user name and password created here are used for the purpose of logging in to the control database.</span><span class="sxs-lookup"><span data-stu-id="1c754-195">The user name and password created here are used for the purpose of logging in to the control database.</span></span> <span data-ttu-id="1c754-196">A separate credential is used for script execution against the databases within the pool.</span><span class="sxs-lookup"><span data-stu-id="1c754-196">A separate credential is used for script execution against the databases within the pool.</span></span>
   
    ![Create username and password][2]
6. <span data-ttu-id="1c754-198">Click the OK button.</span><span class="sxs-lookup"><span data-stu-id="1c754-198">Click the OK button.</span></span> <span data-ttu-id="1c754-199">The components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1c754-199">The components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="1c754-200">The new resource group is pinned to the start board, as shown below.</span><span class="sxs-lookup"><span data-stu-id="1c754-200">The new resource group is pinned to the start board, as shown below.</span></span> <span data-ttu-id="1c754-201">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in the group.</span><span class="sxs-lookup"><span data-stu-id="1c754-201">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in the group.</span></span>
   
    ![resource group in start board][3]
7. <span data-ttu-id="1c754-203">If you attempt to create or manage a job while elastic database jobs is installing, when providing **Credentials** you will see the following message.</span><span class="sxs-lookup"><span data-stu-id="1c754-203">If you attempt to create or manage a job while elastic database jobs is installing, when providing **Credentials** you will see the following message.</span></span>
   
    ![Deployment still in progress][4]

<span data-ttu-id="1c754-205">If uninstallation is required, delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="1c754-205">If uninstallation is required, delete the resource group.</span></span> <span data-ttu-id="1c754-206">See [How to uninstall the Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="1c754-206">See [How to uninstall the Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c754-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="1c754-207">Next steps</span></span>
<span data-ttu-id="1c754-208">Ensure a credential with the appropriate rights for script execution is created on each database in the group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="1c754-208">Ensure a credential with the appropriate rights for script execution is created on each database in the group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="1c754-209">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) to get started.</span><span class="sxs-lookup"><span data-stu-id="1c754-209">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) to get started.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-jobs-service-installation/not-done.png




