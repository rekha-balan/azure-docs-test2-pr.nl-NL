---
title: Optimize your SQL Server environment with Azure Log Analytics | Microsoft Docs
description: With Azure Log Analytics, you can use the SQL Assessment solution to assess the risk and health of your SQL server environments on a regular interval.
services: log-analytics
documentationcenter: ''
author: bandersmsft
manager: carmonm
editor: ''
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 544744fbdc68ad43b64e5caefff21bb634d6a99f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553193"
---
# <a name="optimize-your-sql-server-environment-with-the-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="301e8-103">Optimize your SQL Server environment with the SQL Assessment solution in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="301e8-103">Optimize your SQL Server environment with the SQL Assessment solution in Log Analytics</span></span>

<span data-ttu-id="301e8-104">You can use the SQL Assessment solution to assess the risk and health of your server environments on a regular interval.</span><span class="sxs-lookup"><span data-stu-id="301e8-104">You can use the SQL Assessment solution to assess the risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="301e8-105">This article will help you install the solution so that you can take corrective actions for potential problems.</span><span class="sxs-lookup"><span data-stu-id="301e8-105">This article will help you install the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="301e8-106">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span><span class="sxs-lookup"><span data-stu-id="301e8-106">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="301e8-107">The recommendations are categorized across six focus areas which help you quickly understand the risk and take corrective action.</span><span class="sxs-lookup"><span data-stu-id="301e8-107">The recommendations are categorized across six focus areas which help you quickly understand the risk and take corrective action.</span></span>

<span data-ttu-id="301e8-108">The recommendations made are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span><span class="sxs-lookup"><span data-stu-id="301e8-108">The recommendations made are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="301e8-109">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span><span class="sxs-lookup"><span data-stu-id="301e8-109">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="301e8-110">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span><span class="sxs-lookup"><span data-stu-id="301e8-110">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="301e8-111">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **SQL Assessment** dashboard for the infrastructure in your environment.</span><span class="sxs-lookup"><span data-stu-id="301e8-111">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **SQL Assessment** dashboard for the infrastructure in your environment.</span></span> <span data-ttu-id="301e8-112">The following sections describe how to use the information on the **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span><span class="sxs-lookup"><span data-stu-id="301e8-112">The following sections describe how to use the information on the **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![image of SQL Assessment tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-sql-assessment/sql-assess-tile.png)

![image of SQL Assessment dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="301e8-115">Installing and configuring the solution</span><span class="sxs-lookup"><span data-stu-id="301e8-115">Installing and configuring the solution</span></span>
<span data-ttu-id="301e8-116">SQL Assessment works with all currently supported versions of SQL Server for the Standard, Developer, and Enterprise editions.</span><span class="sxs-lookup"><span data-stu-id="301e8-116">SQL Assessment works with all currently supported versions of SQL Server for the Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="301e8-117">Use the following information to install and configure the solution.</span><span class="sxs-lookup"><span data-stu-id="301e8-117">Use the following information to install and configure the solution.</span></span>

* <span data-ttu-id="301e8-118">Agents must be installed on servers that have SQL Server installed.</span><span class="sxs-lookup"><span data-stu-id="301e8-118">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="301e8-119">The SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span><span class="sxs-lookup"><span data-stu-id="301e8-119">The SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="301e8-120">In order to install the solution, the user must be an administrator or contributor to the Azure subscription when using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="301e8-120">In order to install the solution, the user must be an administrator or contributor to the Azure subscription when using the Azure portal.</span></span> <span data-ttu-id="301e8-121">In addition, the user must be a member of the OMS workspace contributor or administrator role in the OMS portal.</span><span class="sxs-lookup"><span data-stu-id="301e8-121">In addition, the user must be a member of the OMS workspace contributor or administrator role in the OMS portal.</span></span>
* <span data-ttu-id="301e8-122">When using the Operations Manager agent with SQL Assessment, you'll need to use an Operations Manager Run-As account.</span><span class="sxs-lookup"><span data-stu-id="301e8-122">When using the Operations Manager agent with SQL Assessment, you'll need to use an Operations Manager Run-As account.</span></span> <span data-ttu-id="301e8-123">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span><span class="sxs-lookup"><span data-stu-id="301e8-123">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="301e8-124">The MMA agent does not support Operations Manager Run-As accounts.</span><span class="sxs-lookup"><span data-stu-id="301e8-124">The MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="301e8-125">Add the SQL Assessment solution to your OMS workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="301e8-125">Add the SQL Assessment solution to your OMS workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="301e8-126">There is no further configuration required.</span><span class="sxs-lookup"><span data-stu-id="301e8-126">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="301e8-127">After you've added the solution, the AdvisorAssessment.exe file is added to servers with agents.</span><span class="sxs-lookup"><span data-stu-id="301e8-127">After you've added the solution, the AdvisorAssessment.exe file is added to servers with agents.</span></span> <span data-ttu-id="301e8-128">Configuration data is read and then sent to the OMS service in the cloud for processing.</span><span class="sxs-lookup"><span data-stu-id="301e8-128">Configuration data is read and then sent to the OMS service in the cloud for processing.</span></span> <span data-ttu-id="301e8-129">Logic is applied to the received data and the cloud service records the data.</span><span class="sxs-lookup"><span data-stu-id="301e8-129">Logic is applied to the received data and the cloud service records the data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="301e8-130">SQL Assessment data collection details</span><span class="sxs-lookup"><span data-stu-id="301e8-130">SQL Assessment data collection details</span></span>
<span data-ttu-id="301e8-131">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using the agents that you have enabled.</span><span class="sxs-lookup"><span data-stu-id="301e8-131">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using the agents that you have enabled.</span></span>

<span data-ttu-id="301e8-132">The following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span><span class="sxs-lookup"><span data-stu-id="301e8-132">The following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="301e8-133">platform</span><span class="sxs-lookup"><span data-stu-id="301e8-133">platform</span></span> | <span data-ttu-id="301e8-134">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="301e8-134">Direct Agent</span></span> | <span data-ttu-id="301e8-135">SCOM agent</span><span class="sxs-lookup"><span data-stu-id="301e8-135">SCOM agent</span></span> | <span data-ttu-id="301e8-136">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="301e8-136">Azure Storage</span></span> | <span data-ttu-id="301e8-137">SCOM required?</span><span class="sxs-lookup"><span data-stu-id="301e8-137">SCOM required?</span></span> | <span data-ttu-id="301e8-138">SCOM agent data sent via management group</span><span class="sxs-lookup"><span data-stu-id="301e8-138">SCOM agent data sent via management group</span></span> | <span data-ttu-id="301e8-139">collection frequency</span><span class="sxs-lookup"><span data-stu-id="301e8-139">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="301e8-140">Windows</span><span class="sxs-lookup"><span data-stu-id="301e8-140">Windows</span></span> |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-sql-assessment/oms-bullet-green.png) |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-sql-assessment/oms-bullet-green.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-sql-assessment/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-sql-assessment/oms-bullet-red.png) |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-sql-assessment/oms-bullet-green.png) |<span data-ttu-id="301e8-146">7 days</span><span class="sxs-lookup"><span data-stu-id="301e8-146">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="301e8-147">Operations Manager run-as accounts for OMS</span><span class="sxs-lookup"><span data-stu-id="301e8-147">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="301e8-148">Log Analytics in OMS uses the Operations Manager agent and management group to collect and send data to the OMS service.</span><span class="sxs-lookup"><span data-stu-id="301e8-148">Log Analytics in OMS uses the Operations Manager agent and management group to collect and send data to the OMS service.</span></span> <span data-ttu-id="301e8-149">OMS builds upon management packs for workloads to provide value-add services.</span><span class="sxs-lookup"><span data-stu-id="301e8-149">OMS builds upon management packs for workloads to provide value-add services.</span></span> <span data-ttu-id="301e8-150">Each workload requires workload-specific privileges to run management packs in a different security context, such as a domain account.</span><span class="sxs-lookup"><span data-stu-id="301e8-150">Each workload requires workload-specific privileges to run management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="301e8-151">You need to provide credential information by configuring an Operations Manager Run As account.</span><span class="sxs-lookup"><span data-stu-id="301e8-151">You need to provide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="301e8-152">Use the following information to set the Operations Manager run-as account for SQL Assessment.</span><span class="sxs-lookup"><span data-stu-id="301e8-152">Use the following information to set the Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-the-run-as-account-for-sql-assessment"></a><span data-ttu-id="301e8-153">Set the Run As account for SQL assessment</span><span class="sxs-lookup"><span data-stu-id="301e8-153">Set the Run As account for SQL assessment</span></span>
 <span data-ttu-id="301e8-154">If you are already using the SQL Server management pack, you should use that Run As account.</span><span class="sxs-lookup"><span data-stu-id="301e8-154">If you are already using the SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="to-configure-the-sql-run-as-account-in-the-operations-console"></a><span data-ttu-id="301e8-155">To configure the SQL Run As account in the Operations console</span><span class="sxs-lookup"><span data-stu-id="301e8-155">To configure the SQL Run As account in the Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="301e8-156">If you are using the OMS direct agent, rather than the SCOM agent, the management pack always runs in the security context of the Local System account.</span><span class="sxs-lookup"><span data-stu-id="301e8-156">If you are using the OMS direct agent, rather than the SCOM agent, the management pack always runs in the security context of the Local System account.</span></span> <span data-ttu-id="301e8-157">Skip steps 1-5 below, and run either the T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as the user name.</span><span class="sxs-lookup"><span data-stu-id="301e8-157">Skip steps 1-5 below, and run either the T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as the user name.</span></span>
>
>

1. <span data-ttu-id="301e8-158">In Operations Manager, open the Operations console, and then click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="301e8-158">In Operations Manager, open the Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="301e8-159">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span><span class="sxs-lookup"><span data-stu-id="301e8-159">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="301e8-160">On the **Run As Accounts** page, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="301e8-160">On the **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="301e8-161">Select a Windows Run As account that contains the credentials needed for SQL Server, or click **New** to create one.</span><span class="sxs-lookup"><span data-stu-id="301e8-161">Select a Windows Run As account that contains the credentials needed for SQL Server, or click **New** to create one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="301e8-162">The Run As account type must be Windows.</span><span class="sxs-lookup"><span data-stu-id="301e8-162">The Run As account type must be Windows.</span></span> <span data-ttu-id="301e8-163">The Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span><span class="sxs-lookup"><span data-stu-id="301e8-163">The Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="301e8-164">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="301e8-164">Click **Save**.</span></span>
6. <span data-ttu-id="301e8-165">Modify and then execute the following T-SQL sample on each SQL Server Instance to grant minimum permissions required to Run As Account to perform SQL Assessment.</span><span class="sxs-lookup"><span data-stu-id="301e8-165">Modify and then execute the following T-SQL sample on each SQL Server Instance to grant minimum permissions required to Run As Account to perform SQL Assessment.</span></span> <span data-ttu-id="301e8-166">However, you don’t need to do this if a Run As Account is already part of the sysadmin server role on SQL Server Instances.</span><span class="sxs-lookup"><span data-stu-id="301e8-166">However, you don’t need to do this if a Run As Account is already part of the sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with the actual user name being used as Run As Account.
    USE master

    -- Create login for the user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions to user.
    GRANT VIEW SERVER STATE TO [<UserName>]
    GRANT VIEW ANY DEFINITION TO [<UserName>]
    GRANT VIEW ANY DATABASE TO [<UserName>]

    -- Add database user for all the databases on SQL Server Instance, this is required for connecting to individual databases.
    -- NOTE: This command must be run anytime new databases are added to SQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="to-configure-the-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="301e8-167">To configure the SQL Run As account using Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="301e8-167">To configure the SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="301e8-168">Open a PowerShell window and run the following script after you’ve updated it with your information:</span><span class="sxs-lookup"><span data-stu-id="301e8-168">Open a PowerShell window and run the following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="301e8-169">Understanding how recommendations are prioritized</span><span class="sxs-lookup"><span data-stu-id="301e8-169">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="301e8-170">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span><span class="sxs-lookup"><span data-stu-id="301e8-170">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="301e8-171">Only the ten most important recommendations are shown.</span><span class="sxs-lookup"><span data-stu-id="301e8-171">Only the ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="301e8-172">How weights are calculated</span><span class="sxs-lookup"><span data-stu-id="301e8-172">How weights are calculated</span></span>
<span data-ttu-id="301e8-173">Weightings are aggregate values based on three key factors:</span><span class="sxs-lookup"><span data-stu-id="301e8-173">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="301e8-174">The *probability* that an issue identified will cause problems.</span><span class="sxs-lookup"><span data-stu-id="301e8-174">The *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="301e8-175">A higher probability equates to a larger overall score for the recommendation.</span><span class="sxs-lookup"><span data-stu-id="301e8-175">A higher probability equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="301e8-176">The *impact* of the issue on your organization if it does cause a problem.</span><span class="sxs-lookup"><span data-stu-id="301e8-176">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="301e8-177">A higher impact equates to a larger overall score for the recommendation.</span><span class="sxs-lookup"><span data-stu-id="301e8-177">A higher impact equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="301e8-178">The *effort* required to implement the recommendation.</span><span class="sxs-lookup"><span data-stu-id="301e8-178">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="301e8-179">A higher effort equates to a smaller overall score for the recommendation.</span><span class="sxs-lookup"><span data-stu-id="301e8-179">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="301e8-180">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span><span class="sxs-lookup"><span data-stu-id="301e8-180">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="301e8-181">For example, if a recommendation in the Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span><span class="sxs-lookup"><span data-stu-id="301e8-181">For example, if a recommendation in the Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="301e8-182">Focus areas</span><span class="sxs-lookup"><span data-stu-id="301e8-182">Focus areas</span></span>
<span data-ttu-id="301e8-183">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span><span class="sxs-lookup"><span data-stu-id="301e8-183">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="301e8-184">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span><span class="sxs-lookup"><span data-stu-id="301e8-184">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="301e8-185">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span><span class="sxs-lookup"><span data-stu-id="301e8-185">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="301e8-186">**Upgrade, Migration and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy SQL Server to your existing infrastructure.</span><span class="sxs-lookup"><span data-stu-id="301e8-186">**Upgrade, Migration and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy SQL Server to your existing infrastructure.</span></span>

<span data-ttu-id="301e8-187">**Operations and Monitoring** - This focus area shows recommendations to help streamline your IT operations, implement preventative maintenance, and maximize performance.</span><span class="sxs-lookup"><span data-stu-id="301e8-187">**Operations and Monitoring** - This focus area shows recommendations to help streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="301e8-188">**Change and Configuration Management** - This focus area shows recommendations to help protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and to track and audit system configurations.</span><span class="sxs-lookup"><span data-stu-id="301e8-188">**Change and Configuration Management** - This focus area shows recommendations to help protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and to track and audit system configurations.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="301e8-189">Should you aim to score 100% in every focus area?</span><span class="sxs-lookup"><span data-stu-id="301e8-189">Should you aim to score 100% in every focus area?</span></span>
<span data-ttu-id="301e8-190">Not necessarily.</span><span class="sxs-lookup"><span data-stu-id="301e8-190">Not necessarily.</span></span> <span data-ttu-id="301e8-191">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span><span class="sxs-lookup"><span data-stu-id="301e8-191">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="301e8-192">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span><span class="sxs-lookup"><span data-stu-id="301e8-192">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="301e8-193">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span><span class="sxs-lookup"><span data-stu-id="301e8-193">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="301e8-194">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span><span class="sxs-lookup"><span data-stu-id="301e8-194">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="301e8-195">Issues that are important to a mature business may be less important to a start-up.</span><span class="sxs-lookup"><span data-stu-id="301e8-195">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="301e8-196">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span><span class="sxs-lookup"><span data-stu-id="301e8-196">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="301e8-197">Every recommendation includes guidance about why it is important.</span><span class="sxs-lookup"><span data-stu-id="301e8-197">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="301e8-198">You should use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span><span class="sxs-lookup"><span data-stu-id="301e8-198">You should use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="301e8-199">Use assessment focus area recommendations</span><span class="sxs-lookup"><span data-stu-id="301e8-199">Use assessment focus area recommendations</span></span>
<span data-ttu-id="301e8-200">Before you can use an assessment solution in OMS, you must have the solution installed.</span><span class="sxs-lookup"><span data-stu-id="301e8-200">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="301e8-201">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="301e8-201">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="301e8-202">After it is installed, you can view the summary of recommendations by using the SQL Assessment tile on the Overview page in OMS.</span><span class="sxs-lookup"><span data-stu-id="301e8-202">After it is installed, you can view the summary of recommendations by using the SQL Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="301e8-203">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span><span class="sxs-lookup"><span data-stu-id="301e8-203">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="301e8-204">To view recommendations for a focus area and take corrective action</span><span class="sxs-lookup"><span data-stu-id="301e8-204">To view recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="301e8-205">On the **Overview** page, click the **SQL Assessment** tile.</span><span class="sxs-lookup"><span data-stu-id="301e8-205">On the **Overview** page, click the **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="301e8-206">On the **SQL Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span><span class="sxs-lookup"><span data-stu-id="301e8-206">On the **SQL Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="301e8-207">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span><span class="sxs-lookup"><span data-stu-id="301e8-207">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="301e8-208">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span><span class="sxs-lookup"><span data-stu-id="301e8-208">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="301e8-209">![image of SQL Assessment recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="301e8-209">![image of SQL Assessment recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="301e8-210">You can take corrective actions suggested in **Suggested Actions**.</span><span class="sxs-lookup"><span data-stu-id="301e8-210">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="301e8-211">When the item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span><span class="sxs-lookup"><span data-stu-id="301e8-211">When the item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="301e8-212">Corrected items appear as **Passed Objects**.</span><span class="sxs-lookup"><span data-stu-id="301e8-212">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="301e8-213">Ignore recommendations</span><span class="sxs-lookup"><span data-stu-id="301e8-213">Ignore recommendations</span></span>
<span data-ttu-id="301e8-214">If you have recommendations that you want to ignore, you can create a text file that OMS will use to prevent recommendations from appearing in your assessment results.</span><span class="sxs-lookup"><span data-stu-id="301e8-214">If you have recommendations that you want to ignore, you can create a text file that OMS will use to prevent recommendations from appearing in your assessment results.</span></span>

### <a name="to-identify-recommendations-that-you-will-ignore"></a><span data-ttu-id="301e8-215">To identify recommendations that you will ignore</span><span class="sxs-lookup"><span data-stu-id="301e8-215">To identify recommendations that you will ignore</span></span>
1. <span data-ttu-id="301e8-216">Sign in to your workspace and open Log Search.</span><span class="sxs-lookup"><span data-stu-id="301e8-216">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="301e8-217">Use the following query to list recommendations that have failed for computers in your environment.</span><span class="sxs-lookup"><span data-stu-id="301e8-217">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="301e8-218">Here's a screen shot showing the Log Search query: ![failed recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="301e8-218">Here's a screen shot showing the Log Search query: ![failed recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="301e8-219">Choose recommendations that you want to ignore.</span><span class="sxs-lookup"><span data-stu-id="301e8-219">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="301e8-220">You’ll use the values for RecommendationId in the next procedure.</span><span class="sxs-lookup"><span data-stu-id="301e8-220">You’ll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="301e8-221">To create and use an IgnoreRecommendations.txt text file</span><span class="sxs-lookup"><span data-stu-id="301e8-221">To create and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="301e8-222">Create a file named IgnoreRecommendations.txt.</span><span class="sxs-lookup"><span data-stu-id="301e8-222">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="301e8-223">Paste or type each RecommendationId for each recommendation that you want OMS to ignore on a separate line and then save and close the file.</span><span class="sxs-lookup"><span data-stu-id="301e8-223">Paste or type each RecommendationId for each recommendation that you want OMS to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="301e8-224">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span><span class="sxs-lookup"><span data-stu-id="301e8-224">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
   * <span data-ttu-id="301e8-225">On computers with the Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span><span class="sxs-lookup"><span data-stu-id="301e8-225">On computers with the Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="301e8-226">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="301e8-226">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="301e8-227">To verify that recommendations are ignored</span><span class="sxs-lookup"><span data-stu-id="301e8-227">To verify that recommendations are ignored</span></span>
1. <span data-ttu-id="301e8-228">After the next scheduled assessment runs, by default every 7 days, the specified recommendations are marked Ignored and will not appear on the assessment dashboard.</span><span class="sxs-lookup"><span data-stu-id="301e8-228">After the next scheduled assessment runs, by default every 7 days, the specified recommendations are marked Ignored and will not appear on the assessment dashboard.</span></span>
2. <span data-ttu-id="301e8-229">You can use the following Log Search queries to list all the ignored recommendations.</span><span class="sxs-lookup"><span data-stu-id="301e8-229">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="301e8-230">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span><span class="sxs-lookup"><span data-stu-id="301e8-230">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="301e8-231">SQL Assessment solution FAQ</span><span class="sxs-lookup"><span data-stu-id="301e8-231">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="301e8-232">*How often does an assessment run?*</span><span class="sxs-lookup"><span data-stu-id="301e8-232">*How often does an assessment run?*</span></span>

* <span data-ttu-id="301e8-233">The assessment runs every 7 days.</span><span class="sxs-lookup"><span data-stu-id="301e8-233">The assessment runs every 7 days.</span></span>

<span data-ttu-id="301e8-234">*Is there a way to configure how often the assessment runs?*</span><span class="sxs-lookup"><span data-stu-id="301e8-234">*Is there a way to configure how often the assessment runs?*</span></span>

* <span data-ttu-id="301e8-235">Not at this time.</span><span class="sxs-lookup"><span data-stu-id="301e8-235">Not at this time.</span></span>

<span data-ttu-id="301e8-236">*If another server is discovered after I’ve added the SQL assessment solution, will it be assessed?*</span><span class="sxs-lookup"><span data-stu-id="301e8-236">*If another server is discovered after I’ve added the SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="301e8-237">Yes, once it is discovered it is assessed from then on, every 7 days.</span><span class="sxs-lookup"><span data-stu-id="301e8-237">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="301e8-238">*If a server is decommissioned, when will it be removed from the assessment?*</span><span class="sxs-lookup"><span data-stu-id="301e8-238">*If a server is decommissioned, when will it be removed from the assessment?*</span></span>

* <span data-ttu-id="301e8-239">If a server does not submit data for 3 weeks, it is removed.</span><span class="sxs-lookup"><span data-stu-id="301e8-239">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="301e8-240">*What is the name of the process that does the data collection?*</span><span class="sxs-lookup"><span data-stu-id="301e8-240">*What is the name of the process that does the data collection?*</span></span>

* <span data-ttu-id="301e8-241">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="301e8-241">AdvisorAssessment.exe</span></span>

<span data-ttu-id="301e8-242">*How long does it take for data to be collected?*</span><span class="sxs-lookup"><span data-stu-id="301e8-242">*How long does it take for data to be collected?*</span></span>

* <span data-ttu-id="301e8-243">The actual data collection on the server takes about 1 hour.</span><span class="sxs-lookup"><span data-stu-id="301e8-243">The actual data collection on the server takes about 1 hour.</span></span> <span data-ttu-id="301e8-244">It may take longer on servers that have a large number of SQL instances or databases.</span><span class="sxs-lookup"><span data-stu-id="301e8-244">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="301e8-245">*What type of data is collected?*</span><span class="sxs-lookup"><span data-stu-id="301e8-245">*What type of data is collected?*</span></span>

* <span data-ttu-id="301e8-246">The following types of data are collected:</span><span class="sxs-lookup"><span data-stu-id="301e8-246">The following types of data are collected:</span></span>
  * <span data-ttu-id="301e8-247">WMI</span><span class="sxs-lookup"><span data-stu-id="301e8-247">WMI</span></span>
  * <span data-ttu-id="301e8-248">Registry</span><span class="sxs-lookup"><span data-stu-id="301e8-248">Registry</span></span>
  * <span data-ttu-id="301e8-249">Performance counters</span><span class="sxs-lookup"><span data-stu-id="301e8-249">Performance counters</span></span>
  * <span data-ttu-id="301e8-250">SQL dynamic management views (DMV).</span><span class="sxs-lookup"><span data-stu-id="301e8-250">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="301e8-251">*Is there a way to configure when data is collected?*</span><span class="sxs-lookup"><span data-stu-id="301e8-251">*Is there a way to configure when data is collected?*</span></span>

* <span data-ttu-id="301e8-252">Not at this time.</span><span class="sxs-lookup"><span data-stu-id="301e8-252">Not at this time.</span></span>

<span data-ttu-id="301e8-253">*Why do I have to configure a Run As Account?*</span><span class="sxs-lookup"><span data-stu-id="301e8-253">*Why do I have to configure a Run As Account?*</span></span>

* <span data-ttu-id="301e8-254">For SQL Server, a small number of SQL queries are run.</span><span class="sxs-lookup"><span data-stu-id="301e8-254">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="301e8-255">In order for them to run, a Run As Account with VIEW SERVER STATE permissions to SQL must be used.</span><span class="sxs-lookup"><span data-stu-id="301e8-255">In order for them to run, a Run As Account with VIEW SERVER STATE permissions to SQL must be used.</span></span>  <span data-ttu-id="301e8-256">In addition, in order to query WMI, local administrator credentials are required.</span><span class="sxs-lookup"><span data-stu-id="301e8-256">In addition, in order to query WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="301e8-257">*Why display only the top 10 recommendations?*</span><span class="sxs-lookup"><span data-stu-id="301e8-257">*Why display only the top 10 recommendations?*</span></span>

* <span data-ttu-id="301e8-258">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span><span class="sxs-lookup"><span data-stu-id="301e8-258">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="301e8-259">After you address them, additional recommendations will become available.</span><span class="sxs-lookup"><span data-stu-id="301e8-259">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="301e8-260">If you prefer to see the detailed list, you can view all recommendations using the OMS log search.</span><span class="sxs-lookup"><span data-stu-id="301e8-260">If you prefer to see the detailed list, you can view all recommendations using the OMS log search.</span></span>

<span data-ttu-id="301e8-261">*Is there a way to ignore a recommendation?*</span><span class="sxs-lookup"><span data-stu-id="301e8-261">*Is there a way to ignore a recommendation?*</span></span>

* <span data-ttu-id="301e8-262">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span><span class="sxs-lookup"><span data-stu-id="301e8-262">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="301e8-263">Next steps</span><span class="sxs-lookup"><span data-stu-id="301e8-263">Next steps</span></span>
* <span data-ttu-id="301e8-264">[Search logs](log-analytics-log-searches.md) to view detailed SQL Assessment data and recommendations.</span><span class="sxs-lookup"><span data-stu-id="301e8-264">[Search logs](log-analytics-log-searches.md) to view detailed SQL Assessment data and recommendations.</span></span>









