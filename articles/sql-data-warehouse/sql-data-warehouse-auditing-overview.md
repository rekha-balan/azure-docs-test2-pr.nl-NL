---
title: Auditing in Azure SQL Data Warehouse  | Microsoft Docs
description: Get started with auditing in Azure SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: ''
author: ronortloff
manager: jhubbard
editor: ''
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: a6ebe5968891de08e6be724cf725671a9b301e13
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552153"
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="ce3e7-103">Auditing in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ce3e7-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [Auditing](sql-data-warehouse-auditing-overview.md)
> * [Threat detection](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="ce3e7-106">SQL Data Warehouse auditing allows you to record events in your database to an audit log in your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-106">SQL Data Warehouse auditing allows you to record events in your database to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="ce3e7-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="ce3e7-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="ce3e7-109">Auditing tools enable and facilitate adherence to compliance standards but don't guarantee compliance.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-109">Auditing tools enable and facilitate adherence to compliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="ce3e7-110">For more information about Azure programs that support standards compliance, see the <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-110">For more information about Azure programs that support standards compliance, see the <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="ce3e7-111">[Database Auditing basics]</span><span class="sxs-lookup"><span data-stu-id="ce3e7-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="ce3e7-112">[Set up auditing for your database]</span><span class="sxs-lookup"><span data-stu-id="ce3e7-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="ce3e7-113">[Analyze audit logs and reports]</span><span class="sxs-lookup"><span data-stu-id="ce3e7-113">[Analyze audit logs and reports]</span></span>

## <a id="subheading-1"></a><span data-ttu-id="ce3e7-114">Azure SQL Data Warehouse Database Auditing basics</span><span class="sxs-lookup"><span data-stu-id="ce3e7-114">Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="ce3e7-115">SQL Data Warehouse database auditing allows you to:</span><span class="sxs-lookup"><span data-stu-id="ce3e7-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="ce3e7-116">**Retain** an audit trail of selected events.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="ce3e7-117">You can define categories of database actions  to be audited.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-117">You can define categories of database actions  to be audited.</span></span>
* <span data-ttu-id="ce3e7-118">**Report** on database activity.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-118">**Report** on database activity.</span></span> <span data-ttu-id="ce3e7-119">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-119">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="ce3e7-120">**Analyze** reports.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-120">**Analyze** reports.</span></span> <span data-ttu-id="ce3e7-121">You can find suspicious events, unusual activity, and trends.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="ce3e7-122">You can configure auditing for the following event categories:</span><span class="sxs-lookup"><span data-stu-id="ce3e7-122">You can configure auditing for the following event categories:</span></span>

<span data-ttu-id="ce3e7-123">**Plain SQL** and **Parameterized SQL** for which the collected audit logs are classified as</span><span class="sxs-lookup"><span data-stu-id="ce3e7-123">**Plain SQL** and **Parameterized SQL** for which the collected audit logs are classified as</span></span>  

* <span data-ttu-id="ce3e7-124">**Access to data**</span><span class="sxs-lookup"><span data-stu-id="ce3e7-124">**Access to data**</span></span>
* <span data-ttu-id="ce3e7-125">**Schema changes (DDL)**</span><span class="sxs-lookup"><span data-stu-id="ce3e7-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="ce3e7-126">**Data changes (DML)**</span><span class="sxs-lookup"><span data-stu-id="ce3e7-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="ce3e7-127">**Accounts, roles, and permissions (DCL)**</span><span class="sxs-lookup"><span data-stu-id="ce3e7-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="ce3e7-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="ce3e7-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="ce3e7-130">For further details about the activities and events audited, see the <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-130">For further details about the activities and events audited, see the <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="ce3e7-131">Audit logs are stored in your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="ce3e7-132">You can define an audit log retention period.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="ce3e7-133">An auditing policy can be defined for a specific database or as a default server policy.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="ce3e7-134">A default server auditing policy will apply to all databases on a server which do not have a specific overriding database auditing policy defined.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-134">A default server auditing policy will apply to all databases on a server which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="ce3e7-135">Before setting up audit auditing check if you are using a ["Downlevel Client"](sql-data-warehouse-auditing-downlevel-clients.md).</span><span class="sxs-lookup"><span data-stu-id="ce3e7-135">Before setting up audit auditing check if you are using a ["Downlevel Client"](sql-data-warehouse-auditing-downlevel-clients.md).</span></span>

## <a id="subheading-2"></a><span data-ttu-id="ce3e7-136">Set up auditing for your database</span><span class="sxs-lookup"><span data-stu-id="ce3e7-136">Set up auditing for your database</span></span>
1. <span data-ttu-id="ce3e7-137">Launch the <a href="https://portal.azure.com" target="_blank">Azure Portal</a>.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-137">Launch the <a href="https://portal.azure.com" target="_blank">Azure Portal</a>.</span></span>
2. <span data-ttu-id="ce3e7-138">navigate to the configuration blade of the SQL Data Warehouse database / SQL Server you want to audit.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-138">navigate to the configuration blade of the SQL Data Warehouse database / SQL Server you want to audit.</span></span> <span data-ttu-id="ce3e7-139">Click the **Settings** button on top and then, in the Setting blade, and select **Auditing**.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-139">Click the **Settings** button on top and then, in the Setting blade, and select **Auditing**.</span></span>
   
    ![][1]
3. <span data-ttu-id="ce3e7-140">In the auditing configuration blade, first unselect the **Inherit Auditing Settings from Server** checkbox.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-140">In the auditing configuration blade, first unselect the **Inherit Auditing Settings from Server** checkbox.</span></span> <span data-ttu-id="ce3e7-141">This allows you to specify the settings for a particular database.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-141">This allows you to specify the settings for a particular database.</span></span>
   
    ![][2]
4. <span data-ttu-id="ce3e7-142">Next, enable auditing by clicking the **ON** button.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-142">Next, enable auditing by clicking the **ON** button.</span></span>
   
    ![][3]
5. <span data-ttu-id="ce3e7-143">In the auditing configuration blade, select **STORAGE DETAILS** to open the Audit Logs Storage Blade.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-143">In the auditing configuration blade, select **STORAGE DETAILS** to open the Audit Logs Storage Blade.</span></span> <span data-ttu-id="ce3e7-144">Select the Azure storage account where logs will be saved and, the retention period.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-144">Select the Azure storage account where logs will be saved and, the retention period.</span></span> <span data-ttu-id="ce3e7-145">**Tip:** Use the same storage account for all audited databases to get the most out of the preconfigured reports templates.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-145">**Tip:** Use the same storage account for all audited databases to get the most out of the preconfigured reports templates.</span></span>
   
    ![][4]
6. <span data-ttu-id="ce3e7-146">Click the **OK** button to save the storage details configuration.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-146">Click the **OK** button to save the storage details configuration.</span></span>
7. <span data-ttu-id="ce3e7-147">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** to log all events, or choose individual event categories.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-147">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** to log all events, or choose individual event categories.</span></span>
8. <span data-ttu-id="ce3e7-148">If you are configuring Auditing for a database, you may need to alter the connection string of your client to ensure data auditing is correctly captured.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-148">If you are configuring Auditing for a database, you may need to alter the connection string of your client to ensure data auditing is correctly captured.</span></span> <span data-ttu-id="ce3e7-149">Check the [Modify Server FDQN in the connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-149">Check the [Modify Server FDQN in the connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
9. <span data-ttu-id="ce3e7-150">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-150">Click **OK**.</span></span>

## <span data-ttu-id="ce3e7-151"><a id="subheading-3">Analyze audit logs and reports</a></span><span class="sxs-lookup"><span data-stu-id="ce3e7-151"><a id="subheading-3">Analyze audit logs and reports</a></span></span>
<span data-ttu-id="ce3e7-152">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in the Azure storage account you chose during setup.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-152">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="ce3e7-153">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-153">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="ce3e7-154">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> to help you quickly analyze log data.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-154">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> to help you quickly analyze log data.</span></span> <span data-ttu-id="ce3e7-155">To use the template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-155">To use the template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="ce3e7-156">The template has fictional sample data in it, and you can set up Power Query to import your audit log directly from your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-156">The template has fictional sample data in it, and you can set up Power Query to import your audit log directly from your Azure storage account.</span></span>

<span data-ttu-id="ce3e7-157">For more detailed instructions on working with the report template, read the <a href="http://go.microsoft.com/fwlink/?LinkId=506731">How To (doc download)</a>.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-157">For more detailed instructions on working with the report template, read the <a href="http://go.microsoft.com/fwlink/?LinkId=506731">How To (doc download)</a>.</span></span>

![][5]

## <span data-ttu-id="ce3e7-158"><a id="subheading-4">Practices for usage in production</a></span><span class="sxs-lookup"><span data-stu-id="ce3e7-158"><a id="subheading-4">Practices for usage in production</a></span></span>
<span data-ttu-id="ce3e7-159">The description in this section refers to screen captures above.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-159">The description in this section refers to screen captures above.</span></span> <span data-ttu-id="ce3e7-160">Either <a href="https://portal.azure.com" target="_blank">Azure Portal</a> or <a href= "https://manage.windowsazure.com/" target="_bank">Classic Azure Classic Portal</a> may be used.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-160">Either <a href="https://portal.azure.com" target="_blank">Azure Portal</a> or <a href= "https://manage.windowsazure.com/" target="_bank">Classic Azure Classic Portal</a> may be used.</span></span>

## <a id="subheading-5"></a><span data-ttu-id="ce3e7-161">Storage Key Regeneration</span><span class="sxs-lookup"><span data-stu-id="ce3e7-161">Storage Key Regeneration</span></span>
<span data-ttu-id="ce3e7-162">In production you are likely to refresh your storage keys periodically.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-162">In production you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="ce3e7-163">When refresh your keys you need to re-save the policy.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-163">When refresh your keys you need to re-save the policy.</span></span> <span data-ttu-id="ce3e7-164">The process is as follows:.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-164">The process is as follows:.</span></span>

1. <span data-ttu-id="ce3e7-165">In the auditing configuration blade (described above in the set up auditing section) switch the **Storage Access Key** from *Primary* to *Secondary* and **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-165">In the auditing configuration blade (described above in the set up auditing section) switch the **Storage Access Key** from *Primary* to *Secondary* and **SAVE**.</span></span>
   ![][4]
2. <span data-ttu-id="ce3e7-166">Go to the storage configuration blade and **regenerate** the *Primary Access Key*.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-166">Go to the storage configuration blade and **regenerate** the *Primary Access Key*.</span></span>
3. <span data-ttu-id="ce3e7-167">Go back to the auditing configuration blade, switch the **Storage Access Key** from *Secondary* to *Primary* and press **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-167">Go back to the auditing configuration blade, switch the **Storage Access Key** from *Secondary* to *Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="ce3e7-168">Go back to the storage UI and **regenerate** the *Secondary Access Key* (as preparation for the next keys refresh cycle.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-168">Go back to the storage UI and **regenerate** the *Secondary Access Key* (as preparation for the next keys refresh cycle.</span></span>

## <a id="subheading-6"></a><span data-ttu-id="ce3e7-169">Automation</span><span class="sxs-lookup"><span data-stu-id="ce3e7-169">Automation</span></span>
<span data-ttu-id="ce3e7-170">There are several PowerShell cmdlets you can use to configure auditing in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-170">There are several PowerShell cmdlets you can use to configure auditing in Azure SQL Database.</span></span> <span data-ttu-id="ce3e7-171">To access the auditing cmdlets you must be running PowerShell in Azure Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-171">To access the auditing cmdlets you must be running PowerShell in Azure Resource Manager mode.</span></span>

> [!NOTE]
> The  [Azure Resource Manager](https://msdn.microsoft.com/library/dn654592.aspx) module is currently in preview. It might not provide the same management capabilities as the Azure module.
> 
> 

<span data-ttu-id="ce3e7-174">When you are in Azure Resource Manager mode, run `Get-Command *AzureSql*` to list the available cmdlets.</span><span class="sxs-lookup"><span data-stu-id="ce3e7-174">When you are in Azure Resource Manager mode, run `Get-Command *AzureSql*` to list the available cmdlets.</span></span>

<!--Anchors-->
[Database Auditing basics]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3


<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->





