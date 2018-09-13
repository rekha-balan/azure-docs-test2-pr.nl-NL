---
title: Get started with Azure SQL database auditing | Microsoft Docs
description: Use Azure SQL database auditing to track database events into an audit log.
services: sql-database
author: giladmit
manager: craigg
ms.service: sql-database
ms.custom: security
ms.topic: conceptual
ms.date: 06/24/2018
ms.author: giladm
ms.openlocfilehash: f187a5fe1541f5508e55443abe80fc295ee63c87
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800636"
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="41b8f-103">Get started with SQL database auditing</span><span class="sxs-lookup"><span data-stu-id="41b8f-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="41b8f-104">Azure SQL database auditing tracks database events and writes them to an audit log in your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="41b8f-104">Azure SQL database auditing tracks database events and writes them to an audit log in your Azure storage account.</span></span> <span data-ttu-id="41b8f-105">Auditing also:</span><span class="sxs-lookup"><span data-stu-id="41b8f-105">Auditing also:</span></span>

* <span data-ttu-id="41b8f-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span><span class="sxs-lookup"><span data-stu-id="41b8f-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="41b8f-107">Enables and facilitates adherence to compliance standards, although it doesn't guarantee compliance.</span><span class="sxs-lookup"><span data-stu-id="41b8f-107">Enables and facilitates adherence to compliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="41b8f-108">For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="41b8f-108">For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <a id="subheading-1"></a><span data-ttu-id="41b8f-109">Azure SQL database auditing overview</span><span class="sxs-lookup"><span data-stu-id="41b8f-109">Azure SQL database auditing overview</span></span>
<span data-ttu-id="41b8f-110">You can use SQL database auditing to:</span><span class="sxs-lookup"><span data-stu-id="41b8f-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="41b8f-111">**Retain** an audit trail of selected events.</span><span class="sxs-lookup"><span data-stu-id="41b8f-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="41b8f-112">You can define categories of database actions to be audited.</span><span class="sxs-lookup"><span data-stu-id="41b8f-112">You can define categories of database actions to be audited.</span></span>
* <span data-ttu-id="41b8f-113">**Report** on database activity.</span><span class="sxs-lookup"><span data-stu-id="41b8f-113">**Report** on database activity.</span></span> <span data-ttu-id="41b8f-114">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span><span class="sxs-lookup"><span data-stu-id="41b8f-114">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="41b8f-115">**Analyze** reports.</span><span class="sxs-lookup"><span data-stu-id="41b8f-115">**Analyze** reports.</span></span> <span data-ttu-id="41b8f-116">You can find suspicious events, unusual activity, and trends.</span><span class="sxs-lookup"><span data-stu-id="41b8f-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="41b8f-117">You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.</span><span class="sxs-lookup"><span data-stu-id="41b8f-117">You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41b8f-118">Audit logs are written to **Append Blobs** in an Azure Blob storage on your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="41b8f-118">Audit logs are written to **Append Blobs** in an Azure Blob storage on your Azure subscription.</span></span>
>
> * <span data-ttu-id="41b8f-119">**Premium Storage** is currently **not supported** by Append Blobs.</span><span class="sxs-lookup"><span data-stu-id="41b8f-119">**Premium Storage** is currently **not supported** by Append Blobs.</span></span>
> * <span data-ttu-id="41b8f-120">**Storage in VNet** is currently **not supported**.</span><span class="sxs-lookup"><span data-stu-id="41b8f-120">**Storage in VNet** is currently **not supported**.</span></span>

## <a id="subheading-8"></a><span data-ttu-id="41b8f-121">Define server-level vs. database-level auditing policy</span><span class="sxs-lookup"><span data-stu-id="41b8f-121">Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="41b8f-122">An auditing policy can be defined for a specific database or as a default server policy:</span><span class="sxs-lookup"><span data-stu-id="41b8f-122">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="41b8f-123">A server policy applies to all existing and newly created databases on the server.</span><span class="sxs-lookup"><span data-stu-id="41b8f-123">A server policy applies to all existing and newly created databases on the server.</span></span>

* <span data-ttu-id="41b8f-124">If *server blob auditing is enabled*, it *always applies to the database*.</span><span class="sxs-lookup"><span data-stu-id="41b8f-124">If *server blob auditing is enabled*, it *always applies to the database*.</span></span> <span data-ttu-id="41b8f-125">The database will be audited, regardless of the database auditing settings.</span><span class="sxs-lookup"><span data-stu-id="41b8f-125">The database will be audited, regardless of the database auditing settings.</span></span>

* <span data-ttu-id="41b8f-126">Enabling blob auditing on the database, in addition to enabling it on the server, does *not* override or change any of the settings of the server blob auditing.</span><span class="sxs-lookup"><span data-stu-id="41b8f-126">Enabling blob auditing on the database, in addition to enabling it on the server, does *not* override or change any of the settings of the server blob auditing.</span></span> <span data-ttu-id="41b8f-127">Both audits will exist side by side.</span><span class="sxs-lookup"><span data-stu-id="41b8f-127">Both audits will exist side by side.</span></span> <span data-ttu-id="41b8f-128">In other words, the database is audited twice in parallel; once by the server policy and once by the database policy.</span><span class="sxs-lookup"><span data-stu-id="41b8f-128">In other words, the database is audited twice in parallel; once by the server policy and once by the database policy.</span></span>

   > [!NOTE]
   > <span data-ttu-id="41b8f-129">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span><span class="sxs-lookup"><span data-stu-id="41b8f-129">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="41b8f-130">You want to use a different *storage account* or *retention period* for a specific database.</span><span class="sxs-lookup"><span data-stu-id="41b8f-130">You want to use a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="41b8f-131">You want to audit event types or categories for a specific database that differ from the rest of the databases on the server.</span><span class="sxs-lookup"><span data-stu-id="41b8f-131">You want to audit event types or categories for a specific database that differ from the rest of the databases on the server.</span></span> <span data-ttu-id="41b8f-132">For example, you might have table inserts that need to be audited only for a specific database.</span><span class="sxs-lookup"><span data-stu-id="41b8f-132">For example, you might have table inserts that need to be audited only for a specific database.</span></span>
   >
   > <span data-ttu-id="41b8f-133">Otherwise, we recommended that you enable only server-level blob auditing and leave the database-level auditing disabled for all databases.</span><span class="sxs-lookup"><span data-stu-id="41b8f-133">Otherwise, we recommended that you enable only server-level blob auditing and leave the database-level auditing disabled for all databases.</span></span>


## <a id="subheading-2"></a><span data-ttu-id="41b8f-134">Set up auditing for your database</span><span class="sxs-lookup"><span data-stu-id="41b8f-134">Set up auditing for your database</span></span>
<span data-ttu-id="41b8f-135">The following section describes the configuration of auditing using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="41b8f-135">The following section describes the configuration of auditing using the Azure portal.</span></span>

1. <span data-ttu-id="41b8f-136">Go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="41b8f-136">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="41b8f-137">Navigate to **Auditing** under the Security heading in your SQL database/server pane.</span><span class="sxs-lookup"><span data-stu-id="41b8f-137">Navigate to **Auditing** under the Security heading in your SQL database/server pane.</span></span>

    <a id="auditing-screenshot"></a> <span data-ttu-id="41b8f-138">![Navigation pane][1]</span><span class="sxs-lookup"><span data-stu-id="41b8f-138">![Navigation pane][1]</span></span>
3. <span data-ttu-id="41b8f-139">If you prefer to set up a server auditing policy, you can select the **View server settings** link in the database auditing blade.</span><span class="sxs-lookup"><span data-stu-id="41b8f-139">If you prefer to set up a server auditing policy, you can select the **View server settings** link in the database auditing blade.</span></span> <span data-ttu-id="41b8f-140">You can then view or modify the server auditing settings.</span><span class="sxs-lookup"><span data-stu-id="41b8f-140">You can then view or modify the server auditing settings.</span></span> <span data-ttu-id="41b8f-141">Server auditing policies  apply to all existing and newly created databases on this server.</span><span class="sxs-lookup"><span data-stu-id="41b8f-141">Server auditing policies  apply to all existing and newly created databases on this server.</span></span>

    ![Navigation pane][2]
4. <span data-ttu-id="41b8f-143">If you prefer to enable auditing on the database level, switch **Auditing** to **ON**.</span><span class="sxs-lookup"><span data-stu-id="41b8f-143">If you prefer to enable auditing on the database level, switch **Auditing** to **ON**.</span></span>

    <span data-ttu-id="41b8f-144">If server auditing is enabled, the database-configured audit will exist side-by-side with the server audit.</span><span class="sxs-lookup"><span data-stu-id="41b8f-144">If server auditing is enabled, the database-configured audit will exist side-by-side with the server audit.</span></span>

    ![Navigation pane][3]
5. <span data-ttu-id="41b8f-146">To open the **Audit Logs Storage** blade, select **Storage Details**.</span><span class="sxs-lookup"><span data-stu-id="41b8f-146">To open the **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="41b8f-147">Select the Azure storage account where logs will be saved, and then select the retention period.</span><span class="sxs-lookup"><span data-stu-id="41b8f-147">Select the Azure storage account where logs will be saved, and then select the retention period.</span></span> <span data-ttu-id="41b8f-148">The old logs will be deleted.</span><span class="sxs-lookup"><span data-stu-id="41b8f-148">The old logs will be deleted.</span></span> <span data-ttu-id="41b8f-149">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="41b8f-149">Then click **OK**.</span></span>

    <a id="storage-screenshot"></a> <span data-ttu-id="41b8f-150">![Navigation pane][4]</span><span class="sxs-lookup"><span data-stu-id="41b8f-150">![Navigation pane][4]</span></span>
6. <span data-ttu-id="41b8f-151">If you want to customize the audited events, you can do this via [PowerShell cmdlets](#subheading-7) or the [REST API](#subheading-9).</span><span class="sxs-lookup"><span data-stu-id="41b8f-151">If you want to customize the audited events, you can do this via [PowerShell cmdlets](#subheading-7) or the [REST API](#subheading-9).</span></span>
7. <span data-ttu-id="41b8f-152">After you've configured your auditing settings, you can turn on the new threat detection feature and configure emails to receive security alerts.</span><span class="sxs-lookup"><span data-stu-id="41b8f-152">After you've configured your auditing settings, you can turn on the new threat detection feature and configure emails to receive security alerts.</span></span> <span data-ttu-id="41b8f-153">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span><span class="sxs-lookup"><span data-stu-id="41b8f-153">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="41b8f-154">For more information, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="41b8f-154">For more information, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="41b8f-155">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="41b8f-155">Click **Save**.</span></span>





## <a id="subheading-3"></a><span data-ttu-id="41b8f-156">Analyze audit logs and reports</span><span class="sxs-lookup"><span data-stu-id="41b8f-156">Analyze audit logs and reports</span></span>
<span data-ttu-id="41b8f-157">Audit logs are aggregated in the Azure storage account you chose during setup.</span><span class="sxs-lookup"><span data-stu-id="41b8f-157">Audit logs are aggregated in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="41b8f-158">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="41b8f-158">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="41b8f-159">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="41b8f-159">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="41b8f-160">For further details about the hierarchy of the storage folder, naming conventions, and log format, see the [Blob Audit Log Format Reference](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="41b8f-160">For further details about the hierarchy of the storage folder, naming conventions, and log format, see the [Blob Audit Log Format Reference](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="41b8f-161">There are several methods you can use to view blob auditing logs:</span><span class="sxs-lookup"><span data-stu-id="41b8f-161">There are several methods you can use to view blob auditing logs:</span></span>

* <span data-ttu-id="41b8f-162">Use the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="41b8f-162">Use the [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="41b8f-163">Open the relevant database.</span><span class="sxs-lookup"><span data-stu-id="41b8f-163">Open the relevant database.</span></span> <span data-ttu-id="41b8f-164">At the top of the database's **Auditing & Threat detection** blade, click **View audit logs**.</span><span class="sxs-lookup"><span data-stu-id="41b8f-164">At the top of the database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Navigation pane][7]

    <span data-ttu-id="41b8f-166">An **Audit records** blade opens, from which you'll be able to view the logs.</span><span class="sxs-lookup"><span data-stu-id="41b8f-166">An **Audit records** blade opens, from which you'll be able to view the logs.</span></span>

    - <span data-ttu-id="41b8f-167">You can view specific dates by clicking **Filter** at the top of the **Audit records** blade.</span><span class="sxs-lookup"><span data-stu-id="41b8f-167">You can view specific dates by clicking **Filter** at the top of the **Audit records** blade.</span></span>
    - <span data-ttu-id="41b8f-168">You can switch between audit records that were created by the *server audit policy* and the *database audit policy* by toggling **Audit Source**.</span><span class="sxs-lookup"><span data-stu-id="41b8f-168">You can switch between audit records that were created by the *server audit policy* and the *database audit policy* by toggling **Audit Source**.</span></span>
    - <span data-ttu-id="41b8f-169">You can view only SQL injection related audit records by checking  **Show only audit records for SQL injections** checkbox.</span><span class="sxs-lookup"><span data-stu-id="41b8f-169">You can view only SQL injection related audit records by checking  **Show only audit records for SQL injections** checkbox.</span></span>

       ![Navigation pane][8]

* <span data-ttu-id="41b8f-171">Use the system function **sys.fn_get_audit_file** (T-SQL) to return the audit log data in tabular format.</span><span class="sxs-lookup"><span data-stu-id="41b8f-171">Use the system function **sys.fn_get_audit_file** (T-SQL) to return the audit log data in tabular format.</span></span> <span data-ttu-id="41b8f-172">For more information on using this function, see the [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="41b8f-172">For more information on using this function, see the [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="41b8f-173">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span><span class="sxs-lookup"><span data-stu-id="41b8f-173">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>
    1. <span data-ttu-id="41b8f-174">From the SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span><span class="sxs-lookup"><span data-stu-id="41b8f-174">From the SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Navigation pane][9]
    2. <span data-ttu-id="41b8f-176">The **Add Audit Files** dialog box opens.</span><span class="sxs-lookup"><span data-stu-id="41b8f-176">The **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="41b8f-177">Select one of the **Add** options to choose whether to merge audit files from a local disk or import them from Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="41b8f-177">Select one of the **Add** options to choose whether to merge audit files from a local disk or import them from Azure Storage.</span></span> <span data-ttu-id="41b8f-178">You are required to provide your Azure Storage details and account key.</span><span class="sxs-lookup"><span data-stu-id="41b8f-178">You are required to provide your Azure Storage details and account key.</span></span>

    3. <span data-ttu-id="41b8f-179">After all files to merge have been added, click **OK** to complete the merge operation.</span><span class="sxs-lookup"><span data-stu-id="41b8f-179">After all files to merge have been added, click **OK** to complete the merge operation.</span></span>

    4. <span data-ttu-id="41b8f-180">The merged file opens in SSMS, where you can view and analyze it, as well as export it to an XEL or CSV file or to a table.</span><span class="sxs-lookup"><span data-stu-id="41b8f-180">The merged file opens in SSMS, where you can view and analyze it, as well as export it to an XEL or CSV file or to a table.</span></span>

* <span data-ttu-id="41b8f-181">Use the [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span><span class="sxs-lookup"><span data-stu-id="41b8f-181">Use the [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="41b8f-182">It runs in Azure and utilizes Log Analytics public APIs to push SQL audit logs into Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="41b8f-182">It runs in Azure and utilizes Log Analytics public APIs to push SQL audit logs into Log Analytics.</span></span> <span data-ttu-id="41b8f-183">The sync application pushes SQL audit logs into Log Analytics for consumption via the Log Analytics dashboard.</span><span class="sxs-lookup"><span data-stu-id="41b8f-183">The sync application pushes SQL audit logs into Log Analytics for consumption via the Log Analytics dashboard.</span></span>

* <span data-ttu-id="41b8f-184">Use Power BI.</span><span class="sxs-lookup"><span data-stu-id="41b8f-184">Use Power BI.</span></span> <span data-ttu-id="41b8f-185">You can view and analyze audit log data in Power BI.</span><span class="sxs-lookup"><span data-stu-id="41b8f-185">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="41b8f-186">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="41b8f-186">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="41b8f-187">Download log files from your Azure Storage blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="41b8f-187">Download log files from your Azure Storage blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="41b8f-188">After you have downloaded a log file locally, you can double-click the file to open, view, and analyze the logs in SSMS.</span><span class="sxs-lookup"><span data-stu-id="41b8f-188">After you have downloaded a log file locally, you can double-click the file to open, view, and analyze the logs in SSMS.</span></span>
    * <span data-ttu-id="41b8f-189">You can also download multiple files simultaneously via Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="41b8f-189">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="41b8f-190">Right-click a specific subfolder and select **Save as** to save in a local folder.</span><span class="sxs-lookup"><span data-stu-id="41b8f-190">Right-click a specific subfolder and select **Save as** to save in a local folder.</span></span>

* <span data-ttu-id="41b8f-191">Additional methods:</span><span class="sxs-lookup"><span data-stu-id="41b8f-191">Additional methods:</span></span>
   * <span data-ttu-id="41b8f-192">After downloading several files or a subfolder that contains log files, you can merge them locally as described in the SSMS Merge Audit Files instructions described earlier.</span><span class="sxs-lookup"><span data-stu-id="41b8f-192">After downloading several files or a subfolder that contains log files, you can merge them locally as described in the SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="41b8f-193">View blob auditing logs programmatically:</span><span class="sxs-lookup"><span data-stu-id="41b8f-193">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="41b8f-194">Use the [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span><span class="sxs-lookup"><span data-stu-id="41b8f-194">Use the [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="41b8f-195">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41b8f-195">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <a id="subheading-5"></a><span data-ttu-id="41b8f-196">Production practices</span><span class="sxs-lookup"><span data-stu-id="41b8f-196">Production practices</span></span>
<!--The description in this section refers to preceding screen captures.-->

### <span data-ttu-id="41b8f-197"><a id="subheading-6">Auditing geo-replicated databases</a></span><span class="sxs-lookup"><span data-stu-id="41b8f-197"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="41b8f-198">With geo-replicated databases, when you enable auditing on the primary database the secondary database will have an identical auditing policy.</span><span class="sxs-lookup"><span data-stu-id="41b8f-198">With geo-replicated databases, when you enable auditing on the primary database the secondary database will have an identical auditing policy.</span></span> <span data-ttu-id="41b8f-199">It is also possible to set up auditing on the secondary database by enabling auditing on the **secondary server**, independently from the primary database.</span><span class="sxs-lookup"><span data-stu-id="41b8f-199">It is also possible to set up auditing on the secondary database by enabling auditing on the **secondary server**, independently from the primary database.</span></span>

* <span data-ttu-id="41b8f-200">Server-level (**recommended**): Turn on auditing on both the **primary server** as well as the **secondary server** - the primary and secondary databases will each be audited independently based on their respective server-level policy.</span><span class="sxs-lookup"><span data-stu-id="41b8f-200">Server-level (**recommended**): Turn on auditing on both the **primary server** as well as the **secondary server** - the primary and secondary databases will each be audited independently based on their respective server-level policy.</span></span>

* <span data-ttu-id="41b8f-201">Database-level: Database-level auditing for secondary databases can only be configured from Primary database auditing settings.</span><span class="sxs-lookup"><span data-stu-id="41b8f-201">Database-level: Database-level auditing for secondary databases can only be configured from Primary database auditing settings.</span></span>
   * <span data-ttu-id="41b8f-202">Auditing must be enabled on the *primary database itself*, not the server.</span><span class="sxs-lookup"><span data-stu-id="41b8f-202">Auditing must be enabled on the *primary database itself*, not the server.</span></span>
   * <span data-ttu-id="41b8f-203">After auditing is enabled on the primary database, it will also become enabled on the secondary database.</span><span class="sxs-lookup"><span data-stu-id="41b8f-203">After auditing is enabled on the primary database, it will also become enabled on the secondary database.</span></span>

    >[!IMPORTANT]
    ><span data-ttu-id="41b8f-204">With database-level auditing, the storage settings for the secondary database will be identical to those of the primary database, causing cross-regional traffic.</span><span class="sxs-lookup"><span data-stu-id="41b8f-204">With database-level auditing, the storage settings for the secondary database will be identical to those of the primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="41b8f-205">We recommend that you enable only server-level auditing, and leave the database-level auditing disabled for all databases.</span><span class="sxs-lookup"><span data-stu-id="41b8f-205">We recommend that you enable only server-level auditing, and leave the database-level auditing disabled for all databases.</span></span>
<br>

### <span data-ttu-id="41b8f-206"><a id="subheading-6">Storage key regeneration</a></span><span class="sxs-lookup"><span data-stu-id="41b8f-206"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="41b8f-207">In production, you are likely to refresh your storage keys periodically.</span><span class="sxs-lookup"><span data-stu-id="41b8f-207">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="41b8f-208">When refreshing your keys, you need to resave the auditing policy.</span><span class="sxs-lookup"><span data-stu-id="41b8f-208">When refreshing your keys, you need to resave the auditing policy.</span></span> <span data-ttu-id="41b8f-209">The process is as follows:</span><span class="sxs-lookup"><span data-stu-id="41b8f-209">The process is as follows:</span></span>

1. <span data-ttu-id="41b8f-210">Open the **Storage Details** blade.</span><span class="sxs-lookup"><span data-stu-id="41b8f-210">Open the **Storage Details** blade.</span></span> <span data-ttu-id="41b8f-211">In the **Storage Access Key** box, select **Secondary**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="41b8f-211">In the **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="41b8f-212">Then click **Save** at the top of the auditing configuration blade.</span><span class="sxs-lookup"><span data-stu-id="41b8f-212">Then click **Save** at the top of the auditing configuration blade.</span></span>

    ![Navigation pane][5]
2. <span data-ttu-id="41b8f-214">Go to the storage configuration blade and regenerate the primary access key.</span><span class="sxs-lookup"><span data-stu-id="41b8f-214">Go to the storage configuration blade and regenerate the primary access key.</span></span>

    ![Navigation pane][6]
3. <span data-ttu-id="41b8f-216">Go back to the auditing configuration blade, switch the storage access key from secondary to primary, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="41b8f-216">Go back to the auditing configuration blade, switch the storage access key from secondary to primary, and then click **OK**.</span></span> <span data-ttu-id="41b8f-217">Then click **Save** at the top of the auditing configuration blade.</span><span class="sxs-lookup"><span data-stu-id="41b8f-217">Then click **Save** at the top of the auditing configuration blade.</span></span>
4. <span data-ttu-id="41b8f-218">Go back to the storage configuration blade and regenerate the secondary access key (in preparation for the next key's refresh cycle).</span><span class="sxs-lookup"><span data-stu-id="41b8f-218">Go back to the storage configuration blade and regenerate the secondary access key (in preparation for the next key's refresh cycle).</span></span>

## <a name="additional-information"></a><span data-ttu-id="41b8f-219">Additional Information</span><span class="sxs-lookup"><span data-stu-id="41b8f-219">Additional Information</span></span>

* <span data-ttu-id="41b8f-220">For details about the log format, hierarchy of the storage folder and naming conventions, see the [Blob Audit Log Format Reference](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="41b8f-220">For details about the log format, hierarchy of the storage folder and naming conventions, see the [Blob Audit Log Format Reference](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="41b8f-221">Azure SQL Database Audit stores 4000 characters of data for character fields in an audit record.</span><span class="sxs-lookup"><span data-stu-id="41b8f-221">Azure SQL Database Audit stores 4000 characters of data for character fields in an audit record.</span></span> <span data-ttu-id="41b8f-222">When the **statement** or the **data_sensitivity_information** values returned from an auditable action contain more than 4000 characters, any data beyond the first 4000 characters will be **truncated and not audited**.</span><span class="sxs-lookup"><span data-stu-id="41b8f-222">When the **statement** or the **data_sensitivity_information** values returned from an auditable action contain more than 4000 characters, any data beyond the first 4000 characters will be **truncated and not audited**.</span></span>

* <span data-ttu-id="41b8f-223">Audit logs are written to **Append Blobs** in an Azure Blob storage on your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="41b8f-223">Audit logs are written to **Append Blobs** in an Azure Blob storage on your Azure subscription:</span></span>
    * <span data-ttu-id="41b8f-224">**Premium Storage** is currently **not supported** by Append Blobs.</span><span class="sxs-lookup"><span data-stu-id="41b8f-224">**Premium Storage** is currently **not supported** by Append Blobs.</span></span>
    * <span data-ttu-id="41b8f-225">**Storage in VNet** is currently **not supported**.</span><span class="sxs-lookup"><span data-stu-id="41b8f-225">**Storage in VNet** is currently **not supported**.</span></span>

* <span data-ttu-id="41b8f-226">The default auditing policy includes all actions and the following set of action groups, which will audit all the queries and stored procedures executed against the database, as well as successful and failed logins:</span><span class="sxs-lookup"><span data-stu-id="41b8f-226">The default auditing policy includes all actions and the following set of action groups, which will audit all the queries and stored procedures executed against the database, as well as successful and failed logins:</span></span>

    <span data-ttu-id="41b8f-227">BATCH_COMPLETED_GROUP</span><span class="sxs-lookup"><span data-stu-id="41b8f-227">BATCH_COMPLETED_GROUP</span></span><br>
    <span data-ttu-id="41b8f-228">SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP</span><span class="sxs-lookup"><span data-stu-id="41b8f-228">SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP</span></span><br>
    <span data-ttu-id="41b8f-229">FAILED_DATABASE_AUTHENTICATION_GROUP</span><span class="sxs-lookup"><span data-stu-id="41b8f-229">FAILED_DATABASE_AUTHENTICATION_GROUP</span></span>

    <span data-ttu-id="41b8f-230">You can configure auditing for different types of actions and action groups using PowerShell, as described in the [Manage SQL database auditing using Azure PowerShell](#subheading-7) section.</span><span class="sxs-lookup"><span data-stu-id="41b8f-230">You can configure auditing for different types of actions and action groups using PowerShell, as described in the [Manage SQL database auditing using Azure PowerShell](#subheading-7) section.</span></span>

## <a id="subheading-7"></a><span data-ttu-id="41b8f-231">Manage SQL database auditing using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="41b8f-231">Manage SQL database auditing using Azure PowerShell</span></span>

<span data-ttu-id="41b8f-232">**PowerShell cmdlets**:</span><span class="sxs-lookup"><span data-stu-id="41b8f-232">**PowerShell cmdlets**:</span></span>

* <span data-ttu-id="41b8f-233">[Create or Update Database Blob Auditing Policy (Set-AzureRMSqlDatabaseAuditing)][105]</span><span class="sxs-lookup"><span data-stu-id="41b8f-233">[Create or Update Database Blob Auditing Policy (Set-AzureRMSqlDatabaseAuditing)][105]</span></span>
* <span data-ttu-id="41b8f-234">[Create or Update Server Blob Auditing Policy (Set-AzureRMSqlServerAuditing)][106]</span><span class="sxs-lookup"><span data-stu-id="41b8f-234">[Create or Update Server Blob Auditing Policy (Set-AzureRMSqlServerAuditing)][106]</span></span>
* <span data-ttu-id="41b8f-235">[Get Database Auditing Policy (Get-AzureRMSqlDatabaseAuditing)][101]</span><span class="sxs-lookup"><span data-stu-id="41b8f-235">[Get Database Auditing Policy (Get-AzureRMSqlDatabaseAuditing)][101]</span></span>
* <span data-ttu-id="41b8f-236">[Get Server Blob Auditing Policy (Get-AzureRMSqlServerAuditing)][102]</span><span class="sxs-lookup"><span data-stu-id="41b8f-236">[Get Server Blob Auditing Policy (Get-AzureRMSqlServerAuditing)][102]</span></span>

<span data-ttu-id="41b8f-237">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="41b8f-237">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a id="subheading-9"></a><span data-ttu-id="41b8f-238">Manage SQL database auditing using REST API</span><span class="sxs-lookup"><span data-stu-id="41b8f-238">Manage SQL database auditing using REST API</span></span>

<span data-ttu-id="41b8f-239">**REST API - Blob auditing**:</span><span class="sxs-lookup"><span data-stu-id="41b8f-239">**REST API - Blob auditing**:</span></span>

* [<span data-ttu-id="41b8f-240">Create or Update Database Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="41b8f-240">Create or Update Database Blob Auditing Policy</span></span>](https://docs.microsoft.com/en-us/rest/api/sql/database%20auditing%20settings/createorupdate)
* [<span data-ttu-id="41b8f-241">Create or Update Server Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="41b8f-241">Create or Update Server Blob Auditing Policy</span></span>](https://docs.microsoft.com/en-us/rest/api/sql/server%20auditing%20settings/createorupdate)
* [<span data-ttu-id="41b8f-242">Get Database Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="41b8f-242">Get Database Blob Auditing Policy</span></span>](https://docs.microsoft.com/en-us/rest/api/sql/database%20auditing%20settings/get)
* [<span data-ttu-id="41b8f-243">Get Server Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="41b8f-243">Get Server Blob Auditing Policy</span></span>](https://docs.microsoft.com/en-us/rest/api/sql/server%20auditing%20settings/get)

<span data-ttu-id="41b8f-244">Extended policy with WHERE clause support for additional filtering:</span><span class="sxs-lookup"><span data-stu-id="41b8f-244">Extended policy with WHERE clause support for additional filtering:</span></span>
* [<span data-ttu-id="41b8f-245">Create or Update Database *Extended* Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="41b8f-245">Create or Update Database *Extended* Blob Auditing Policy</span></span>](https://docs.microsoft.com/en-us/rest/api/sql/database%20extended%20auditing%20settings/createorupdate)
* [<span data-ttu-id="41b8f-246">Create or Update Server *Extended* Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="41b8f-246">Create or Update Server *Extended* Blob Auditing Policy</span></span>](https://docs.microsoft.com/en-us/rest/api/sql/server%20extended%20auditing%20settings/createorupdate)
* [<span data-ttu-id="41b8f-247">Get Database *Extended* Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="41b8f-247">Get Database *Extended* Blob Auditing Policy</span></span>](https://docs.microsoft.com/en-us/rest/api/sql/database%20extended%20auditing%20settings/get)
* [<span data-ttu-id="41b8f-248">Get Server *Extended* Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="41b8f-248">Get Server *Extended* Blob Auditing Policy</span></span>](https://docs.microsoft.com/en-us/rest/api/sql/server%20extended%20auditing%20settings/get)

<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Manage SQL database auditing using Azure PowerShell]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)
[Manage SQL database auditing using REST API]: #subheading-9

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditing
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditing
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditing
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditing
