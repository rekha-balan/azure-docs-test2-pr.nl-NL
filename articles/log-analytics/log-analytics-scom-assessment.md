---
title: Optimize your System Center Operations Manager environment with Azure Log Analytics | Microsoft Docs
description: You can use the System Center Operations Manager Assessment solution to assess the risk and health of your server environments on a regular interval.
services: log-analytics
documentationcenter: ''
author: bandersmsft
manager: carmonm
editor: tysonn
ms.assetid: 49aad8b1-3e05-4588-956c-6fdd7715cda1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6eafbf613bcd4006a8df6471be6b5262b15bdc36
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670394"
---
# <a name="optimize-your-environment-with-the-system-center-operations-manager-assessment-preview-solution"></a><span data-ttu-id="98b92-103">Optimize your environment with the System Center Operations Manager Assessment (Preview) solution</span><span class="sxs-lookup"><span data-stu-id="98b92-103">Optimize your environment with the System Center Operations Manager Assessment (Preview) solution</span></span>

<span data-ttu-id="98b92-104">You can use the System Center Operations Manager Assessment solution to assess the risk and health of your System Center Operations Manager server environments on a regular interval.</span><span class="sxs-lookup"><span data-stu-id="98b92-104">You can use the System Center Operations Manager Assessment solution to assess the risk and health of your System Center Operations Manager server environments on a regular interval.</span></span> <span data-ttu-id="98b92-105">This article helps you install, configure, and use the solution so that you can take corrective actions for potential problems.</span><span class="sxs-lookup"><span data-stu-id="98b92-105">This article helps you install, configure, and use the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="98b92-106">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span><span class="sxs-lookup"><span data-stu-id="98b92-106">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="98b92-107">The recommendations are categorized across four focus areas, which help you quickly understand the risk and take corrective action.</span><span class="sxs-lookup"><span data-stu-id="98b92-107">The recommendations are categorized across four focus areas, which help you quickly understand the risk and take corrective action.</span></span>

<span data-ttu-id="98b92-108">The recommendations made are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span><span class="sxs-lookup"><span data-stu-id="98b92-108">The recommendations made are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="98b92-109">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span><span class="sxs-lookup"><span data-stu-id="98b92-109">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="98b92-110">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span><span class="sxs-lookup"><span data-stu-id="98b92-110">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="98b92-111">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **System Center Operations Manager Assessment** dashboard for your infrastructure.</span><span class="sxs-lookup"><span data-stu-id="98b92-111">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **System Center Operations Manager Assessment** dashboard for your infrastructure.</span></span> <span data-ttu-id="98b92-112">The following sections describe how to use the information on the **System Center Operations Manager Assessment** dashboard, where you can view and then take recommended actions for your SCOM infrastructure.</span><span class="sxs-lookup"><span data-stu-id="98b92-112">The following sections describe how to use the information on the **System Center Operations Manager Assessment** dashboard, where you can view and then take recommended actions for your SCOM infrastructure.</span></span>

![System Center Operations Manager solution tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/scom-tile.png)

![System Center Operations Manager Assessment dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="98b92-115">Installing and configuring the solution</span><span class="sxs-lookup"><span data-stu-id="98b92-115">Installing and configuring the solution</span></span>

<span data-ttu-id="98b92-116">The solution works with Microsoft System Operations Manager 2012 R2 and 2012 SP1.</span><span class="sxs-lookup"><span data-stu-id="98b92-116">The solution works with Microsoft System Operations Manager 2012 R2 and 2012 SP1.</span></span>

<span data-ttu-id="98b92-117">Use the following information to install and configure the solution.</span><span class="sxs-lookup"><span data-stu-id="98b92-117">Use the following information to install and configure the solution.</span></span>

 - <span data-ttu-id="98b92-118">Before you can use an assessment solution in OMS, you must have the solution installed.</span><span class="sxs-lookup"><span data-stu-id="98b92-118">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="98b92-119">Install the solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) or by following the instructions in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="98b92-119">Install the solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) or by following the instructions in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

 - <span data-ttu-id="98b92-120">After adding the solution to the workspace, the System Center Operations Manager Assessment tile on the dashboard displays the additional configuration required message.</span><span class="sxs-lookup"><span data-stu-id="98b92-120">After adding the solution to the workspace, the System Center Operations Manager Assessment tile on the dashboard displays the additional configuration required message.</span></span> <span data-ttu-id="98b92-121">Click on the tile and follow the configuration steps mentioned in the page</span><span class="sxs-lookup"><span data-stu-id="98b92-121">Click on the tile and follow the configuration steps mentioned in the page</span></span>

 ![System Center Operations Manager dashboard tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/scom-configrequired-tile.PNG)

 <span data-ttu-id="98b92-123">Configuration of the System Center Operations Manager can be done through the script by following the steps mentioned in the configuration page of the solution in OMS.</span><span class="sxs-lookup"><span data-stu-id="98b92-123">Configuration of the System Center Operations Manager can be done through the script by following the steps mentioned in the configuration page of the solution in OMS.</span></span>

 <span data-ttu-id="98b92-124">Instead, to configure the assessment through SCOM Console, follow the below steps in the same order</span><span class="sxs-lookup"><span data-stu-id="98b92-124">Instead, to configure the assessment through SCOM Console, follow the below steps in the same order</span></span>
1. [<span data-ttu-id="98b92-125">Set the Run As account for System Center Operations Manager Assessment</span><span class="sxs-lookup"><span data-stu-id="98b92-125">Set the Run As account for System Center Operations Manager Assessment</span></span>](#operations-manager-run-as-accounts-for-oms)  
2. [<span data-ttu-id="98b92-126">Configure the System Center Operations Manager Assessment rule</span><span class="sxs-lookup"><span data-stu-id="98b92-126">Configure the System Center Operations Manager Assessment rule</span></span>](#configure-the-assessment-rule)

# <a name="system-center-operations-manager-assessment-data-collection-details"></a><span data-ttu-id="98b92-127">System Center Operations Manager assessment data collection details</span><span class="sxs-lookup"><span data-stu-id="98b92-127">System Center Operations Manager assessment data collection details</span></span>

<span data-ttu-id="98b92-128">The System Center Operations Manager assessment collects WMI data, Registry data, EventLog data, Operations Manager data through Windows PowerShell, SQL Queries, File information collector using the server that you have enabled.</span><span class="sxs-lookup"><span data-stu-id="98b92-128">The System Center Operations Manager assessment collects WMI data, Registry data, EventLog data, Operations Manager data through Windows PowerShell, SQL Queries, File information collector using the server that you have enabled.</span></span>

<span data-ttu-id="98b92-129">The following table shows data collection methods for System Center Operations Manager Assessment, and how often data is collected by an agent.</span><span class="sxs-lookup"><span data-stu-id="98b92-129">The following table shows data collection methods for System Center Operations Manager Assessment, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="98b92-130">platform</span><span class="sxs-lookup"><span data-stu-id="98b92-130">platform</span></span> | <span data-ttu-id="98b92-131">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="98b92-131">Direct Agent</span></span> | <span data-ttu-id="98b92-132">SCOM agent</span><span class="sxs-lookup"><span data-stu-id="98b92-132">SCOM agent</span></span> | <span data-ttu-id="98b92-133">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="98b92-133">Azure Storage</span></span> | <span data-ttu-id="98b92-134">SCOM required?</span><span class="sxs-lookup"><span data-stu-id="98b92-134">SCOM required?</span></span> | <span data-ttu-id="98b92-135">SCOM agent data sent via management group</span><span class="sxs-lookup"><span data-stu-id="98b92-135">SCOM agent data sent via management group</span></span> | <span data-ttu-id="98b92-136">collection frequency</span><span class="sxs-lookup"><span data-stu-id="98b92-136">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="98b92-137">Windows</span><span class="sxs-lookup"><span data-stu-id="98b92-137">Windows</span></span> |  ![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/oms-bullet-red.png) | ![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/oms-bullet-red.png)  | ![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/oms-bullet-red.png)  |  ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/oms-bullet-green.png) | ![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/oms-bullet-red.png)  | <span data-ttu-id="98b92-143">seven days</span><span class="sxs-lookup"><span data-stu-id="98b92-143">seven days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="98b92-144">Operations Manager run-as accounts for OMS</span><span class="sxs-lookup"><span data-stu-id="98b92-144">Operations Manager run-as accounts for OMS</span></span>

<span data-ttu-id="98b92-145">OMS builds on management packs for workloads to provide value-add services.</span><span class="sxs-lookup"><span data-stu-id="98b92-145">OMS builds on management packs for workloads to provide value-add services.</span></span> <span data-ttu-id="98b92-146">Each workload requires workload-specific privileges to run management packs in a different security context, such as a domain account.</span><span class="sxs-lookup"><span data-stu-id="98b92-146">Each workload requires workload-specific privileges to run management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="98b92-147">Configure an Operations Manager Run As account to provide credential information.</span><span class="sxs-lookup"><span data-stu-id="98b92-147">Configure an Operations Manager Run As account to provide credential information.</span></span>

<span data-ttu-id="98b92-148">Use the following information to set the Operations Manager run-as account for System Center Operations Manager Assessment.</span><span class="sxs-lookup"><span data-stu-id="98b92-148">Use the following information to set the Operations Manager run-as account for System Center Operations Manager Assessment.</span></span>

### <a name="set-the-run-as-account"></a><span data-ttu-id="98b92-149">Set the Run As account</span><span class="sxs-lookup"><span data-stu-id="98b92-149">Set the Run As account</span></span>

1. <span data-ttu-id="98b92-150">In the Operations Manager Console, go to the **Administration** tab.</span><span class="sxs-lookup"><span data-stu-id="98b92-150">In the Operations Manager Console, go to the **Administration** tab.</span></span>
2. <span data-ttu-id="98b92-151">Under the **Run As Configuration**, click **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="98b92-151">Under the **Run As Configuration**, click **Accounts**.</span></span>
3. <span data-ttu-id="98b92-152">Create the Run As Account, following through the Wizard, creating a Windows account.</span><span class="sxs-lookup"><span data-stu-id="98b92-152">Create the Run As Account, following through the Wizard, creating a Windows account.</span></span> <span data-ttu-id="98b92-153">The account to use is the one identified and having all the prerequisites below:</span><span class="sxs-lookup"><span data-stu-id="98b92-153">The account to use is the one identified and having all the prerequisites below:</span></span>

    >[!NOTE]
    <span data-ttu-id="98b92-154">The Run As account must meet following requirements:</span><span class="sxs-lookup"><span data-stu-id="98b92-154">The Run As account must meet following requirements:</span></span>
    - <span data-ttu-id="98b92-155">A domain account member of the local Administrators group on all servers in the environment (All Operations Manager Roles - Management Server, OpsMgr Database, Data Warehouse, Reporting, Web Console, Gateway)</span><span class="sxs-lookup"><span data-stu-id="98b92-155">A domain account member of the local Administrators group on all servers in the environment (All Operations Manager Roles - Management Server, OpsMgr Database, Data Warehouse, Reporting, Web Console, Gateway)</span></span>
    - <span data-ttu-id="98b92-156">Operation Manager Administrator Role for the management group being assessed</span><span class="sxs-lookup"><span data-stu-id="98b92-156">Operation Manager Administrator Role for the management group being assessed</span></span>
    - <span data-ttu-id="98b92-157">Execute the [script](#sql-script-to-grant-granular-permissions-to-the-run-as-account) to grant granular permissions to the account on SQL instance used by Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="98b92-157">Execute the [script](#sql-script-to-grant-granular-permissions-to-the-run-as-account) to grant granular permissions to the account on SQL instance used by Operations Manager.</span></span>
      <span data-ttu-id="98b92-158">Note: If this account has sysadmin rights already, then skip the script execution.</span><span class="sxs-lookup"><span data-stu-id="98b92-158">Note: If this account has sysadmin rights already, then skip the script execution.</span></span>

4. <span data-ttu-id="98b92-159">Under **Distribution Security**, select **More secure**.</span><span class="sxs-lookup"><span data-stu-id="98b92-159">Under **Distribution Security**, select **More secure**.</span></span>
5. <span data-ttu-id="98b92-160">Specify the management server where the account is distributed.</span><span class="sxs-lookup"><span data-stu-id="98b92-160">Specify the management server where the account is distributed.</span></span>
3. <span data-ttu-id="98b92-161">Go back to the Run As Configuration and click **Profiles**.</span><span class="sxs-lookup"><span data-stu-id="98b92-161">Go back to the Run As Configuration and click **Profiles**.</span></span>
4. <span data-ttu-id="98b92-162">Search for the *SCOM Assessment Profile*.</span><span class="sxs-lookup"><span data-stu-id="98b92-162">Search for the *SCOM Assessment Profile*.</span></span>
5. <span data-ttu-id="98b92-163">The profile name should be: *Microsoft System Center Advisor SCOM Assessment Run As Profile*.</span><span class="sxs-lookup"><span data-stu-id="98b92-163">The profile name should be: *Microsoft System Center Advisor SCOM Assessment Run As Profile*.</span></span>
6. <span data-ttu-id="98b92-164">Right-click and update its properties and add the recently created Run As Account you created in step 3.</span><span class="sxs-lookup"><span data-stu-id="98b92-164">Right-click and update its properties and add the recently created Run As Account you created in step 3.</span></span>

### <a name="sql-script-to-grant-granular-permissions-to-the-run-as-account"></a><span data-ttu-id="98b92-165">SQL script to grant granular permissions to the Run As account</span><span class="sxs-lookup"><span data-stu-id="98b92-165">SQL script to grant granular permissions to the Run As account</span></span>

<span data-ttu-id="98b92-166">Execute the following SQL script to grant required permissions to the Run As account on the SQL instance used by Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="98b92-166">Execute the following SQL script to grant required permissions to the Run As account on the SQL instance used by Operations Manager.</span></span>

```
-- Replace <UserName> with the actual user name being used as Run As Account.
USE master

-- Create login for the user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions to user.
GRANT VIEW SERVER STATE TO [UserName]
GRANT VIEW ANY DEFINITION TO [UserName]
GRANT VIEW ANY DATABASE TO [UserName]

-- Add database user for all the databases on SQL Server Instance, this is required for connecting to individual databases.
-- NOTE: This command must be run anytime new databases are added to SQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT To [UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace the Operations Manager database name with the one in your environment
Use [OperationsManager];
GRANT SELECT To [UserName]
GO

--Replace the Operations Manager DatawareHouse database name with the one in your environment
Use [OperationsManagerDW];
GRANT SELECT To [UserName]
GO

--Replace the Operations Manager Audit Collection database name with the one in your environment
Use [OperationsManagerAC];
GRANT SELECT To [UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace the Operations Manager database name with the one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-the-assessment-rule"></a><span data-ttu-id="98b92-167">Configure the assessment rule</span><span class="sxs-lookup"><span data-stu-id="98b92-167">Configure the assessment rule</span></span>

<span data-ttu-id="98b92-168">The System Center Operations Manager Assessment solution’s management pack includes a rule named *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule*.</span><span class="sxs-lookup"><span data-stu-id="98b92-168">The System Center Operations Manager Assessment solution’s management pack includes a rule named *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule*.</span></span> <span data-ttu-id="98b92-169">This rule is responsible for running the assessment.</span><span class="sxs-lookup"><span data-stu-id="98b92-169">This rule is responsible for running the assessment.</span></span> <span data-ttu-id="98b92-170">To enable the rule and configure the frequency, use the procedures below.</span><span class="sxs-lookup"><span data-stu-id="98b92-170">To enable the rule and configure the frequency, use the procedures below.</span></span>

<span data-ttu-id="98b92-171">By default, the Microsoft System Center Advisor SCOM Assessment Run Assessment Rule is disabled.</span><span class="sxs-lookup"><span data-stu-id="98b92-171">By default, the Microsoft System Center Advisor SCOM Assessment Run Assessment Rule is disabled.</span></span> <span data-ttu-id="98b92-172">To run the assessment, you must enable the rule on a management server.</span><span class="sxs-lookup"><span data-stu-id="98b92-172">To run the assessment, you must enable the rule on a management server.</span></span> <span data-ttu-id="98b92-173">Use the following steps.</span><span class="sxs-lookup"><span data-stu-id="98b92-173">Use the following steps.</span></span>

#### <a name="enable-the-rule-for-a-specific-management-server"></a><span data-ttu-id="98b92-174">Enable the rule for a specific management server</span><span class="sxs-lookup"><span data-stu-id="98b92-174">Enable the rule for a specific management server</span></span>

1. <span data-ttu-id="98b92-175">In the **Authoring** workspace of the Operations Manager console, search for the rule *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule* in the **Rules** pane.</span><span class="sxs-lookup"><span data-stu-id="98b92-175">In the **Authoring** workspace of the Operations Manager console, search for the rule *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule* in the **Rules** pane.</span></span>
2. <span data-ttu-id="98b92-176">In the search results, select the one that includes the text *Type: Management Server*.</span><span class="sxs-lookup"><span data-stu-id="98b92-176">In the search results, select the one that includes the text *Type: Management Server*.</span></span>
3. <span data-ttu-id="98b92-177">Right-click the rule and then click **Overrides** > **For a specific object of class: Management Server**.</span><span class="sxs-lookup"><span data-stu-id="98b92-177">Right-click the rule and then click **Overrides** > **For a specific object of class: Management Server**.</span></span>
4.  <span data-ttu-id="98b92-178">In the available management servers list, select the management server where the rule should run.</span><span class="sxs-lookup"><span data-stu-id="98b92-178">In the available management servers list, select the management server where the rule should run.</span></span>
5.  <span data-ttu-id="98b92-179">Ensure that you change override value to **True** for the **Enabled** parameter value.</span><span class="sxs-lookup"><span data-stu-id="98b92-179">Ensure that you change override value to **True** for the **Enabled** parameter value.</span></span>  
    <span data-ttu-id="98b92-180">![override parameter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/rule.png)</span><span class="sxs-lookup"><span data-stu-id="98b92-180">![override parameter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/rule.png)</span></span>

<span data-ttu-id="98b92-181">While still in this window, configure the frequency of the run using the next procedure.</span><span class="sxs-lookup"><span data-stu-id="98b92-181">While still in this window, configure the frequency of the run using the next procedure.</span></span>

#### <a name="configure-the-run-frequency"></a><span data-ttu-id="98b92-182">Configure the run frequency</span><span class="sxs-lookup"><span data-stu-id="98b92-182">Configure the run frequency</span></span>

<span data-ttu-id="98b92-183">The assessment is configured to run every 10,080 minutes (or seven days), the default interval.</span><span class="sxs-lookup"><span data-stu-id="98b92-183">The assessment is configured to run every 10,080 minutes (or seven days), the default interval.</span></span> <span data-ttu-id="98b92-184">You can override the value to a minimum value of 1440 minutes (or one day).</span><span class="sxs-lookup"><span data-stu-id="98b92-184">You can override the value to a minimum value of 1440 minutes (or one day).</span></span> <span data-ttu-id="98b92-185">The value represents the minimum time gap required between successive assessment runs.</span><span class="sxs-lookup"><span data-stu-id="98b92-185">The value represents the minimum time gap required between successive assessment runs.</span></span> <span data-ttu-id="98b92-186">To override the interval, use the steps below.</span><span class="sxs-lookup"><span data-stu-id="98b92-186">To override the interval, use the steps below.</span></span>

1. <span data-ttu-id="98b92-187">In the **Authoring** workspace of the Operations Manager console, search for the rule *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule* in the **Rules** pane.</span><span class="sxs-lookup"><span data-stu-id="98b92-187">In the **Authoring** workspace of the Operations Manager console, search for the rule *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule* in the **Rules** pane.</span></span>
2. <span data-ttu-id="98b92-188">In the search results, select the one that includes the text *Type: Management Server*.</span><span class="sxs-lookup"><span data-stu-id="98b92-188">In the search results, select the one that includes the text *Type: Management Server*.</span></span>
3. <span data-ttu-id="98b92-189">Right-click the rule and then click **Override the Rule** > **For all objects of class: Management Server**.</span><span class="sxs-lookup"><span data-stu-id="98b92-189">Right-click the rule and then click **Override the Rule** > **For all objects of class: Management Server**.</span></span>
4. <span data-ttu-id="98b92-190">Change the **Interval** parameter value to your desired interval value.</span><span class="sxs-lookup"><span data-stu-id="98b92-190">Change the **Interval** parameter value to your desired interval value.</span></span> <span data-ttu-id="98b92-191">In the example below, the value is set to 1440 minutes (one day).</span><span class="sxs-lookup"><span data-stu-id="98b92-191">In the example below, the value is set to 1440 minutes (one day).</span></span>  
    <span data-ttu-id="98b92-192">![interval parameter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/interval.png)</span><span class="sxs-lookup"><span data-stu-id="98b92-192">![interval parameter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/interval.png)</span></span>  
    <span data-ttu-id="98b92-193">If the value is set to less than 1440 minutes, then the rule runs at a one day interval.</span><span class="sxs-lookup"><span data-stu-id="98b92-193">If the value is set to less than 1440 minutes, then the rule runs at a one day interval.</span></span> <span data-ttu-id="98b92-194">In this example, the rule ignores the interval value and runs at a frequency of one day.</span><span class="sxs-lookup"><span data-stu-id="98b92-194">In this example, the rule ignores the interval value and runs at a frequency of one day.</span></span>


## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="98b92-195">Understanding how recommendations are prioritized</span><span class="sxs-lookup"><span data-stu-id="98b92-195">Understanding how recommendations are prioritized</span></span>

<span data-ttu-id="98b92-196">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span><span class="sxs-lookup"><span data-stu-id="98b92-196">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="98b92-197">Only the 10 most important recommendations are shown.</span><span class="sxs-lookup"><span data-stu-id="98b92-197">Only the 10 most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="98b92-198">How weights are calculated</span><span class="sxs-lookup"><span data-stu-id="98b92-198">How weights are calculated</span></span>

<span data-ttu-id="98b92-199">Weightings are aggregate values based on three key factors:</span><span class="sxs-lookup"><span data-stu-id="98b92-199">Weightings are aggregate values based on three key factors:</span></span>

- <span data-ttu-id="98b92-200">The *probability* that an issue identified will cause problems.</span><span class="sxs-lookup"><span data-stu-id="98b92-200">The *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="98b92-201">A higher probability equates to a larger overall score for the recommendation.</span><span class="sxs-lookup"><span data-stu-id="98b92-201">A higher probability equates to a larger overall score for the recommendation.</span></span>
- <span data-ttu-id="98b92-202">The *impact* of the issue on your organization if it does cause a problem.</span><span class="sxs-lookup"><span data-stu-id="98b92-202">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="98b92-203">A higher impact equates to a larger overall score for the recommendation.</span><span class="sxs-lookup"><span data-stu-id="98b92-203">A higher impact equates to a larger overall score for the recommendation.</span></span>
- <span data-ttu-id="98b92-204">The *effort* required to implement the recommendation.</span><span class="sxs-lookup"><span data-stu-id="98b92-204">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="98b92-205">A higher effort equates to a smaller overall score for the recommendation.</span><span class="sxs-lookup"><span data-stu-id="98b92-205">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="98b92-206">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span><span class="sxs-lookup"><span data-stu-id="98b92-206">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="98b92-207">For example, if a recommendation in the Availability and Business Continuity focus area has a score of 5%, implementing that recommendation increases your overall Availability and Business Continuity score by 5%.</span><span class="sxs-lookup"><span data-stu-id="98b92-207">For example, if a recommendation in the Availability and Business Continuity focus area has a score of 5%, implementing that recommendation increases your overall Availability and Business Continuity score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="98b92-208">Focus areas</span><span class="sxs-lookup"><span data-stu-id="98b92-208">Focus areas</span></span>

<span data-ttu-id="98b92-209">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span><span class="sxs-lookup"><span data-stu-id="98b92-209">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="98b92-210">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span><span class="sxs-lookup"><span data-stu-id="98b92-210">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="98b92-211">**Upgrade, Migration, and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy SQL Server to your existing infrastructure.</span><span class="sxs-lookup"><span data-stu-id="98b92-211">**Upgrade, Migration, and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy SQL Server to your existing infrastructure.</span></span>

<span data-ttu-id="98b92-212">**Operations and Monitoring** - This focus area shows recommendations to help streamline your IT operations, implement preventative maintenance, and maximize performance.</span><span class="sxs-lookup"><span data-stu-id="98b92-212">**Operations and Monitoring** - This focus area shows recommendations to help streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="98b92-213">Should you aim to score 100% in every focus area?</span><span class="sxs-lookup"><span data-stu-id="98b92-213">Should you aim to score 100% in every focus area?</span></span>

<span data-ttu-id="98b92-214">Not necessarily.</span><span class="sxs-lookup"><span data-stu-id="98b92-214">Not necessarily.</span></span> <span data-ttu-id="98b92-215">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span><span class="sxs-lookup"><span data-stu-id="98b92-215">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="98b92-216">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span><span class="sxs-lookup"><span data-stu-id="98b92-216">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="98b92-217">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span><span class="sxs-lookup"><span data-stu-id="98b92-217">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="98b92-218">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span><span class="sxs-lookup"><span data-stu-id="98b92-218">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="98b92-219">Issues that are important to a mature business may be less important to a start-up.</span><span class="sxs-lookup"><span data-stu-id="98b92-219">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="98b92-220">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span><span class="sxs-lookup"><span data-stu-id="98b92-220">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="98b92-221">Every recommendation includes guidance about why it is important.</span><span class="sxs-lookup"><span data-stu-id="98b92-221">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="98b92-222">Use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span><span class="sxs-lookup"><span data-stu-id="98b92-222">Use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="98b92-223">Use assessment focus area recommendations</span><span class="sxs-lookup"><span data-stu-id="98b92-223">Use assessment focus area recommendations</span></span>

<span data-ttu-id="98b92-224">Before you can use an assessment solution in OMS, you must have the solution installed.</span><span class="sxs-lookup"><span data-stu-id="98b92-224">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="98b92-225">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="98b92-225">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="98b92-226">After it is installed, you can view the summary of recommendations by using the System Center Operations Manager Assessment tile on the Overview page in OMS.</span><span class="sxs-lookup"><span data-stu-id="98b92-226">After it is installed, you can view the summary of recommendations by using the System Center Operations Manager Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="98b92-227">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span><span class="sxs-lookup"><span data-stu-id="98b92-227">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="98b92-228">To view recommendations for a focus area and take corrective action</span><span class="sxs-lookup"><span data-stu-id="98b92-228">To view recommendations for a focus area and take corrective action</span></span>

1. <span data-ttu-id="98b92-229">On the **Overview** page, click the **System Center Operations Manager Assessment** tile.</span><span class="sxs-lookup"><span data-stu-id="98b92-229">On the **Overview** page, click the **System Center Operations Manager Assessment** tile.</span></span>
2. <span data-ttu-id="98b92-230">On the **System Center Operations Manager Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span><span class="sxs-lookup"><span data-stu-id="98b92-230">On the **System Center Operations Manager Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="98b92-231">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span><span class="sxs-lookup"><span data-stu-id="98b92-231">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="98b92-232">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span><span class="sxs-lookup"><span data-stu-id="98b92-232">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="98b92-233">![focus area](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/focus-area.png)</span><span class="sxs-lookup"><span data-stu-id="98b92-233">![focus area](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/focus-area.png)</span></span>
4. <span data-ttu-id="98b92-234">You can take corrective actions suggested in **Suggested Actions**.</span><span class="sxs-lookup"><span data-stu-id="98b92-234">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="98b92-235">When the item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span><span class="sxs-lookup"><span data-stu-id="98b92-235">When the item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="98b92-236">Corrected items appear as **Passed Objects**.</span><span class="sxs-lookup"><span data-stu-id="98b92-236">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="98b92-237">Ignore recommendations</span><span class="sxs-lookup"><span data-stu-id="98b92-237">Ignore recommendations</span></span>

<span data-ttu-id="98b92-238">If you have recommendations that you want to ignore, you can create a text file that OMS uses to prevent recommendations from appearing in your assessment results.</span><span class="sxs-lookup"><span data-stu-id="98b92-238">If you have recommendations that you want to ignore, you can create a text file that OMS uses to prevent recommendations from appearing in your assessment results.</span></span>

### <a name="to-identify-recommendations-that-you-want-to-ignore"></a><span data-ttu-id="98b92-239">To identify recommendations that you want to ignore</span><span class="sxs-lookup"><span data-stu-id="98b92-239">To identify recommendations that you want to ignore</span></span>

1. <span data-ttu-id="98b92-240">Sign in to your workspace and open Log Search.</span><span class="sxs-lookup"><span data-stu-id="98b92-240">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="98b92-241">Use the following query to list recommendations that have failed for computers in your environment.</span><span class="sxs-lookup"><span data-stu-id="98b92-241">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    <span data-ttu-id="98b92-242">Here's a screen shot showing the Log Search query:</span><span class="sxs-lookup"><span data-stu-id="98b92-242">Here's a screen shot showing the Log Search query:</span></span>  
    ![log search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-scom-assessment/scom-log-search.png)

2. <span data-ttu-id="98b92-244">Choose recommendations that you want to ignore.</span><span class="sxs-lookup"><span data-stu-id="98b92-244">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="98b92-245">You'll use the values for RecommendationId in the next procedure.</span><span class="sxs-lookup"><span data-stu-id="98b92-245">You'll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="98b92-246">To create and use an IgnoreRecommendations.txt text file</span><span class="sxs-lookup"><span data-stu-id="98b92-246">To create and use an IgnoreRecommendations.txt text file</span></span>

1. <span data-ttu-id="98b92-247">Create a file named IgnoreRecommendations.txt.</span><span class="sxs-lookup"><span data-stu-id="98b92-247">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="98b92-248">Paste or type each RecommendationId for each recommendation that you want OMS to ignore on a separate line and then save and close the file.</span><span class="sxs-lookup"><span data-stu-id="98b92-248">Paste or type each RecommendationId for each recommendation that you want OMS to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="98b92-249">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span><span class="sxs-lookup"><span data-stu-id="98b92-249">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
4. <span data-ttu-id="98b92-250">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server.</span><span class="sxs-lookup"><span data-stu-id="98b92-250">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server.</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="98b92-251">To verify that recommendations are ignored</span><span class="sxs-lookup"><span data-stu-id="98b92-251">To verify that recommendations are ignored</span></span>

1. <span data-ttu-id="98b92-252">After the next scheduled assessment runs, by default every seven days, the specified recommendations are marked Ignored and will not appear on the assessment dashboard.</span><span class="sxs-lookup"><span data-stu-id="98b92-252">After the next scheduled assessment runs, by default every seven days, the specified recommendations are marked Ignored and will not appear on the assessment dashboard.</span></span>
2. <span data-ttu-id="98b92-253">You can use the following Log Search queries to list all the ignored recommendations.</span><span class="sxs-lookup"><span data-stu-id="98b92-253">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. <span data-ttu-id="98b92-254">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span><span class="sxs-lookup"><span data-stu-id="98b92-254">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="system-center-operations-manager-assessment-solution-faq"></a><span data-ttu-id="98b92-255">System Center Operations Manager Assessment solution FAQ</span><span class="sxs-lookup"><span data-stu-id="98b92-255">System Center Operations Manager Assessment solution FAQ</span></span>

<span data-ttu-id="98b92-256">*I added the assessment solution to my OMS workspace. But I don’t see the recommendations. Why not?*</span><span class="sxs-lookup"><span data-stu-id="98b92-256">*I added the assessment solution to my OMS workspace. But I don’t see the recommendations. Why not?*</span></span> <span data-ttu-id="98b92-257">After adding the solution, use the following steps view the recommendations on the OMS dashboard.</span><span class="sxs-lookup"><span data-stu-id="98b92-257">After adding the solution, use the following steps view the recommendations on the OMS dashboard.</span></span>  

- [<span data-ttu-id="98b92-258">Set the Run As account for System Center Operations Manager Assessment</span><span class="sxs-lookup"><span data-stu-id="98b92-258">Set the Run As account for System Center Operations Manager Assessment</span></span>](#operations-manager-run-as-accounts-for-oms)  
- [<span data-ttu-id="98b92-259">Configure the System Center Operations Manager Assessment rule</span><span class="sxs-lookup"><span data-stu-id="98b92-259">Configure the System Center Operations Manager Assessment rule</span></span>](#configure-the-assessment-rule)


<span data-ttu-id="98b92-260">*Is there a way to configure how often the assessment runs?*</span><span class="sxs-lookup"><span data-stu-id="98b92-260">*Is there a way to configure how often the assessment runs?*</span></span> <span data-ttu-id="98b92-261">Yes.</span><span class="sxs-lookup"><span data-stu-id="98b92-261">Yes.</span></span> <span data-ttu-id="98b92-262">See [Configure the run frequency](#configure-the-run-frequency).</span><span class="sxs-lookup"><span data-stu-id="98b92-262">See [Configure the run frequency](#configure-the-run-frequency).</span></span>

<span data-ttu-id="98b92-263">*If another server is discovered after I’ve added the System Center Operations Manager Assessment solution, will it be assessed?*</span><span class="sxs-lookup"><span data-stu-id="98b92-263">*If another server is discovered after I’ve added the System Center Operations Manager Assessment solution, will it be assessed?*</span></span> <span data-ttu-id="98b92-264">Yes, after discovery, it is assessed from then on--by default, every seven days.</span><span class="sxs-lookup"><span data-stu-id="98b92-264">Yes, after discovery, it is assessed from then on--by default, every seven days.</span></span>

<span data-ttu-id="98b92-265">*What is the name of the process that does the data collection?*</span><span class="sxs-lookup"><span data-stu-id="98b92-265">*What is the name of the process that does the data collection?*</span></span> <span data-ttu-id="98b92-266">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="98b92-266">AdvisorAssessment.exe</span></span>

<span data-ttu-id="98b92-267">*Where does the AdvisorAssessment.exe process run?*</span><span class="sxs-lookup"><span data-stu-id="98b92-267">*Where does the AdvisorAssessment.exe process run?*</span></span> <span data-ttu-id="98b92-268">AdvisorAssessment.exe runs under the HealthService of the management server where the assessment rule is enabled.</span><span class="sxs-lookup"><span data-stu-id="98b92-268">AdvisorAssessment.exe runs under the HealthService of the management server where the assessment rule is enabled.</span></span> <span data-ttu-id="98b92-269">Using that process, discovery of your entire environment is achieved through remote data collection.</span><span class="sxs-lookup"><span data-stu-id="98b92-269">Using that process, discovery of your entire environment is achieved through remote data collection.</span></span>

<span data-ttu-id="98b92-270">*How long does it take for data collection?*</span><span class="sxs-lookup"><span data-stu-id="98b92-270">*How long does it take for data collection?*</span></span> <span data-ttu-id="98b92-271">Data collection on the server takes about one hour.</span><span class="sxs-lookup"><span data-stu-id="98b92-271">Data collection on the server takes about one hour.</span></span> <span data-ttu-id="98b92-272">It may take longer in environments that have many Operations Manager instances or databases.</span><span class="sxs-lookup"><span data-stu-id="98b92-272">It may take longer in environments that have many Operations Manager instances or databases.</span></span>

<span data-ttu-id="98b92-273">*What if I set the interval of the assessment to less than 1440 minutes?*</span><span class="sxs-lookup"><span data-stu-id="98b92-273">*What if I set the interval of the assessment to less than 1440 minutes?*</span></span> <span data-ttu-id="98b92-274">The assessment is pre-configured to run at a maximum of once per day.</span><span class="sxs-lookup"><span data-stu-id="98b92-274">The assessment is pre-configured to run at a maximum of once per day.</span></span> <span data-ttu-id="98b92-275">If you override the interval value to a value less than 1440 minutes, then the assessment uses 1440 minutes as the interval value.</span><span class="sxs-lookup"><span data-stu-id="98b92-275">If you override the interval value to a value less than 1440 minutes, then the assessment uses 1440 minutes as the interval value.</span></span>

<span data-ttu-id="98b92-276">*How to know if there are pre-requisite failures?*</span><span class="sxs-lookup"><span data-stu-id="98b92-276">*How to know if there are pre-requisite failures?*</span></span> <span data-ttu-id="98b92-277">If the assessment ran and you don't see results, then it is likely that some of the pre-requisites for the assessment failed.</span><span class="sxs-lookup"><span data-stu-id="98b92-277">If the assessment ran and you don't see results, then it is likely that some of the pre-requisites for the assessment failed.</span></span> <span data-ttu-id="98b92-278">You can execute queries: `Type=Operation Solution=SCOMAssessment` and `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` in Log Search to see the failed pre-requisites.</span><span class="sxs-lookup"><span data-stu-id="98b92-278">You can execute queries: `Type=Operation Solution=SCOMAssessment` and `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` in Log Search to see the failed pre-requisites.</span></span>

<span data-ttu-id="98b92-279">*There is a `Failed to connect to the SQL Instance (….).` message in pre-requisite failures. What is the issue?*</span><span class="sxs-lookup"><span data-stu-id="98b92-279">*There is a `Failed to connect to the SQL Instance (….).` message in pre-requisite failures. What is the issue?*</span></span> <span data-ttu-id="98b92-280">AdvisorAssessment.exe, the process that collects data, runs under the HealthService of the management server.</span><span class="sxs-lookup"><span data-stu-id="98b92-280">AdvisorAssessment.exe, the process that collects data, runs under the HealthService of the management server.</span></span> <span data-ttu-id="98b92-281">As part of the assessment, the process attempts to connect to the SQL Server where the Operations Manager database is present.</span><span class="sxs-lookup"><span data-stu-id="98b92-281">As part of the assessment, the process attempts to connect to the SQL Server where the Operations Manager database is present.</span></span> <span data-ttu-id="98b92-282">This error can occur when firewall rules block the connection to the SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="98b92-282">This error can occur when firewall rules block the connection to the SQL Server instance.</span></span>

<span data-ttu-id="98b92-283">*What type of data is collected?*</span><span class="sxs-lookup"><span data-stu-id="98b92-283">*What type of data is collected?*</span></span> <span data-ttu-id="98b92-284">The following types of data are collected: - WMI data - Registry data - EventLog data - Operations Manager data through Windows PowerShell, SQL Queries and File information collector.</span><span class="sxs-lookup"><span data-stu-id="98b92-284">The following types of data are collected: - WMI data - Registry data - EventLog data - Operations Manager data through Windows PowerShell, SQL Queries and File information collector.</span></span>

<span data-ttu-id="98b92-285">*Why do I have to configure a Run As Account?*</span><span class="sxs-lookup"><span data-stu-id="98b92-285">*Why do I have to configure a Run As Account?*</span></span> <span data-ttu-id="98b92-286">For an Operations Manager server, various SQL queries are run.</span><span class="sxs-lookup"><span data-stu-id="98b92-286">For an Operations Manager server, various SQL queries are run.</span></span> <span data-ttu-id="98b92-287">In order for them to run, you must use a Run As Account with necessary permissions.</span><span class="sxs-lookup"><span data-stu-id="98b92-287">In order for them to run, you must use a Run As Account with necessary permissions.</span></span> <span data-ttu-id="98b92-288">In addition, local administrator credentials are required to query WMI.</span><span class="sxs-lookup"><span data-stu-id="98b92-288">In addition, local administrator credentials are required to query WMI.</span></span>

<span data-ttu-id="98b92-289">*Why display only the top 10 recommendations?*</span><span class="sxs-lookup"><span data-stu-id="98b92-289">*Why display only the top 10 recommendations?*</span></span> <span data-ttu-id="98b92-290">Instead of giving you an exhaustive, overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span><span class="sxs-lookup"><span data-stu-id="98b92-290">Instead of giving you an exhaustive, overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="98b92-291">After you address them, additional recommendations will become available.</span><span class="sxs-lookup"><span data-stu-id="98b92-291">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="98b92-292">If you prefer to see the detailed list, you can view all recommendations using Log Search.</span><span class="sxs-lookup"><span data-stu-id="98b92-292">If you prefer to see the detailed list, you can view all recommendations using Log Search.</span></span>

<span data-ttu-id="98b92-293">*Is there a way to ignore a recommendation?*</span><span class="sxs-lookup"><span data-stu-id="98b92-293">*Is there a way to ignore a recommendation?*</span></span> <span data-ttu-id="98b92-294">Yes, see the [Ignore recommendations](#Ignore-recommendations).</span><span class="sxs-lookup"><span data-stu-id="98b92-294">Yes, see the [Ignore recommendations](#Ignore-recommendations).</span></span>


## <a name="next-steps"></a><span data-ttu-id="98b92-295">Next steps</span><span class="sxs-lookup"><span data-stu-id="98b92-295">Next steps</span></span>

- <span data-ttu-id="98b92-296">[Search logs](log-analytics-log-searches.md) to view detailed System Center Operations Manager Assessment data and recommendations.</span><span class="sxs-lookup"><span data-stu-id="98b92-296">[Search logs](log-analytics-log-searches.md) to view detailed System Center Operations Manager Assessment data and recommendations.</span></span>












