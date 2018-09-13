---
title: Get started with Azure SQL database auditing | Microsoft Docs
description: Get started with SQL database auditing
services: sql-database
documentationcenter: ''
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security-protect
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: giladm
ms.openlocfilehash: 27ad91eed1c8a80afca98dada556a8b83bcfc7d2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549526"
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="9d48f-103">Get started with SQL database auditing</span><span class="sxs-lookup"><span data-stu-id="9d48f-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="9d48f-104">Azure SQL Database Auditing tracks database events and writes them to an audit log in your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="9d48f-104">Azure SQL Database Auditing tracks database events and writes them to an audit log in your Azure Storage account.</span></span>

<span data-ttu-id="9d48f-105">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span><span class="sxs-lookup"><span data-stu-id="9d48f-105">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="9d48f-106">Auditing enables and facilitates adherence to compliance standards but doesn't guarantee compliance.</span><span class="sxs-lookup"><span data-stu-id="9d48f-106">Auditing enables and facilitates adherence to compliance standards but doesn't guarantee compliance.</span></span> <span data-ttu-id="9d48f-107">For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="9d48f-107">For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>

* <span data-ttu-id="9d48f-108">[Azure SQL Database Auditing overview]</span><span class="sxs-lookup"><span data-stu-id="9d48f-108">[Azure SQL Database Auditing overview]</span></span>
* <span data-ttu-id="9d48f-109">[Set up auditing for your database]</span><span class="sxs-lookup"><span data-stu-id="9d48f-109">[Set up auditing for your database]</span></span>
* <span data-ttu-id="9d48f-110">[Analyze audit logs and reports]</span><span class="sxs-lookup"><span data-stu-id="9d48f-110">[Analyze audit logs and reports]</span></span>

## <a id="subheading-1"></a><span data-ttu-id="9d48f-111">Azure SQL Database auditing overview</span><span class="sxs-lookup"><span data-stu-id="9d48f-111">Azure SQL Database auditing overview</span></span>
<span data-ttu-id="9d48f-112">SQL Database Auditing allows you to:</span><span class="sxs-lookup"><span data-stu-id="9d48f-112">SQL Database Auditing allows you to:</span></span>

* <span data-ttu-id="9d48f-113">**Retain** an audit trail of selected events.</span><span class="sxs-lookup"><span data-stu-id="9d48f-113">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="9d48f-114">You can define categories of database actions to be audited.</span><span class="sxs-lookup"><span data-stu-id="9d48f-114">You can define categories of database actions to be audited.</span></span>
* <span data-ttu-id="9d48f-115">**Report** on database activity.</span><span class="sxs-lookup"><span data-stu-id="9d48f-115">**Report** on database activity.</span></span> <span data-ttu-id="9d48f-116">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span><span class="sxs-lookup"><span data-stu-id="9d48f-116">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="9d48f-117">**Analyze** reports.</span><span class="sxs-lookup"><span data-stu-id="9d48f-117">**Analyze** reports.</span></span> <span data-ttu-id="9d48f-118">You can find suspicious events, unusual activity, and trends.</span><span class="sxs-lookup"><span data-stu-id="9d48f-118">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="9d48f-119">There are two **Auditing methods**:</span><span class="sxs-lookup"><span data-stu-id="9d48f-119">There are two **Auditing methods**:</span></span>

* <span data-ttu-id="9d48f-120">**Blob Auditing** - logs are written to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="9d48f-120">**Blob Auditing** - logs are written to Azure Blob Storage.</span></span> <span data-ttu-id="9d48f-121">This is a newer auditing method, which provides **higher performance**, supports **higher granularity object-level auditing**, and is **more cost effective**.</span><span class="sxs-lookup"><span data-stu-id="9d48f-121">This is a newer auditing method, which provides **higher performance**, supports **higher granularity object-level auditing**, and is **more cost effective**.</span></span> <span data-ttu-id="9d48f-122">Blob Auditing will be replacing Table Auditing.</span><span class="sxs-lookup"><span data-stu-id="9d48f-122">Blob Auditing will be replacing Table Auditing.</span></span>
* <span data-ttu-id="9d48f-123">**Table Auditing (deprecated)** - logs are written to Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="9d48f-123">**Table Auditing (deprecated)** - logs are written to Azure Table Storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d48f-124">The introduction of the new Blob Auditing brings a major change to the way server auditing policy is being inherited by the database.</span><span class="sxs-lookup"><span data-stu-id="9d48f-124">The introduction of the new Blob Auditing brings a major change to the way server auditing policy is being inherited by the database.</span></span> <span data-ttu-id="9d48f-125">See [Blob/Table differences in server auditing policy inheritance](#subheading-8) section for additional details.</span><span class="sxs-lookup"><span data-stu-id="9d48f-125">See [Blob/Table differences in server auditing policy inheritance](#subheading-8) section for additional details.</span></span>

<span data-ttu-id="9d48f-126">You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.</span><span class="sxs-lookup"><span data-stu-id="9d48f-126">You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.</span></span>

<!--For each Event Category, auditing of **Success** and **Failure** operations are configured separately.-->

<span data-ttu-id="9d48f-127">An auditing policy can be defined for a specific database or as a default server policy.</span><span class="sxs-lookup"><span data-stu-id="9d48f-127">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="9d48f-128">A default server auditing policy applies to all existing and newly created databases on a server.</span><span class="sxs-lookup"><span data-stu-id="9d48f-128">A default server auditing policy applies to all existing and newly created databases on a server.</span></span>

## <a id="subheading-2"></a><span data-ttu-id="9d48f-129">Set up auditing for your database</span><span class="sxs-lookup"><span data-stu-id="9d48f-129">Set up auditing for your database</span></span>
<span data-ttu-id="9d48f-130">The following section describes the configuration of auditing using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9d48f-130">The following section describes the configuration of auditing using the Azure portal.</span></span>

### <span data-ttu-id="9d48f-131"><a id="subheading-2-1">Blob Auditing</a></span><span class="sxs-lookup"><span data-stu-id="9d48f-131"><a id="subheading-2-1">Blob Auditing</a></span></span>
1. <span data-ttu-id="9d48f-132">Launch the [Azure portal](https://portal.azure.com) at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="9d48f-132">Launch the [Azure portal](https://portal.azure.com) at https://portal.azure.com.</span></span>
2. <span data-ttu-id="9d48f-133">Navigate to the settings blade of the SQL Database / SQL Server you want to audit.</span><span class="sxs-lookup"><span data-stu-id="9d48f-133">Navigate to the settings blade of the SQL Database / SQL Server you want to audit.</span></span> <span data-ttu-id="9d48f-134">In the Settings blade, select **Auditing & Threat detection**.</span><span class="sxs-lookup"><span data-stu-id="9d48f-134">In the Settings blade, select **Auditing & Threat detection**.</span></span>

    <a id="auditing-screenshot"></a> <span data-ttu-id="9d48f-135">![Navigation pane][1]</span><span class="sxs-lookup"><span data-stu-id="9d48f-135">![Navigation pane][1]</span></span>
3. <span data-ttu-id="9d48f-136">In the database auditing configuration blade, you can check the **Inherit settings from server** checkbox to designate that this database will be audited according to its server's settings.</span><span class="sxs-lookup"><span data-stu-id="9d48f-136">In the database auditing configuration blade, you can check the **Inherit settings from server** checkbox to designate that this database will be audited according to its server's settings.</span></span> <span data-ttu-id="9d48f-137">If this option is checked, you will see a **View server auditing settings** link that allows you to view or modify the server auditing settings from this context.</span><span class="sxs-lookup"><span data-stu-id="9d48f-137">If this option is checked, you will see a **View server auditing settings** link that allows you to view or modify the server auditing settings from this context.</span></span>

    ![Navigation pane][2]
4. <span data-ttu-id="9d48f-139">If you prefer to enable Blob Auditing on the database-level (in addition or instead of server-level auditing), **uncheck** the **Inherit Auditing settings from server** option, turn **ON** Auditing, and choose the **Blob** Auditing Type.</span><span class="sxs-lookup"><span data-stu-id="9d48f-139">If you prefer to enable Blob Auditing on the database-level (in addition or instead of server-level auditing), **uncheck** the **Inherit Auditing settings from server** option, turn **ON** Auditing, and choose the **Blob** Auditing Type.</span></span>

   > <span data-ttu-id="9d48f-140">If server Blob auditing is enabled, the database configured audit will exist side by side with the server Blob audit.</span><span class="sxs-lookup"><span data-stu-id="9d48f-140">If server Blob auditing is enabled, the database configured audit will exist side by side with the server Blob audit.</span></span>  

    ![Navigation pane][3]
5. <span data-ttu-id="9d48f-142">Select **Storage Details** to open the Audit Logs Storage Blade.</span><span class="sxs-lookup"><span data-stu-id="9d48f-142">Select **Storage Details** to open the Audit Logs Storage Blade.</span></span> <span data-ttu-id="9d48f-143">Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted, then click **OK** at the bottom.</span><span class="sxs-lookup"><span data-stu-id="9d48f-143">Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted, then click **OK** at the bottom.</span></span> <span data-ttu-id="9d48f-144">**Tip:** Use the same storage account for all audited databases to get the most out of the auditing reports templates.</span><span class="sxs-lookup"><span data-stu-id="9d48f-144">**Tip:** Use the same storage account for all audited databases to get the most out of the auditing reports templates.</span></span>

    <a id="storage-screenshot"></a> <span data-ttu-id="9d48f-145">![Navigation pane][4]</span><span class="sxs-lookup"><span data-stu-id="9d48f-145">![Navigation pane][4]</span></span>
6. <span data-ttu-id="9d48f-146">If you want to customize the audited events, you can do this via PowerShell or REST API - see the [Automation (PowerShell / REST API)](#subheading-7) section for more details.</span><span class="sxs-lookup"><span data-stu-id="9d48f-146">If you want to customize the audited events, you can do this via PowerShell or REST API - see the [Automation (PowerShell / REST API)](#subheading-7) section for more details.</span></span>
7. <span data-ttu-id="9d48f-147">Once you've configured your auditing settings, you can turn on the new **Threat Detection** (preview) feature, and configure the emails to receive security alerts.</span><span class="sxs-lookup"><span data-stu-id="9d48f-147">Once you've configured your auditing settings, you can turn on the new **Threat Detection** (preview) feature, and configure the emails to receive security alerts.</span></span> <span data-ttu-id="9d48f-148">Threat Detection allows you to receive proactive alerts on anomalous database activities that may indicate potential security threats.</span><span class="sxs-lookup"><span data-stu-id="9d48f-148">Threat Detection allows you to receive proactive alerts on anomalous database activities that may indicate potential security threats.</span></span> <span data-ttu-id="9d48f-149">See [Getting Started with Threat Detection](sql-database-threat-detection-get-started.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="9d48f-149">See [Getting Started with Threat Detection](sql-database-threat-detection-get-started.md) for more details.</span></span>
8. <span data-ttu-id="9d48f-150">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9d48f-150">Click **Save**.</span></span>

### <span data-ttu-id="9d48f-151"><a id="subheading-2-2">Table Auditing</a> (deprecated)</span><span class="sxs-lookup"><span data-stu-id="9d48f-151"><a id="subheading-2-2">Table Auditing</a> (deprecated)</span></span>

> <span data-ttu-id="9d48f-152">Before setting up **Table Auditing**, check if you are using a ["Downlevel Client"](sql-database-auditing-and-dynamic-data-masking-downlevel-clients.md).</span><span class="sxs-lookup"><span data-stu-id="9d48f-152">Before setting up **Table Auditing**, check if you are using a ["Downlevel Client"](sql-database-auditing-and-dynamic-data-masking-downlevel-clients.md).</span></span> <span data-ttu-id="9d48f-153">Also, if you have strict firewall settings, please note that the [IP endpoint of your database will change](sql-database-auditing-and-dynamic-data-masking-downlevel-clients.md) when enabling Table Auditing.</span><span class="sxs-lookup"><span data-stu-id="9d48f-153">Also, if you have strict firewall settings, please note that the [IP endpoint of your database will change](sql-database-auditing-and-dynamic-data-masking-downlevel-clients.md) when enabling Table Auditing.</span></span>


1. <span data-ttu-id="9d48f-154">Launch the [Azure portal](https://portal.azure.com) at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="9d48f-154">Launch the [Azure portal](https://portal.azure.com) at https://portal.azure.com.</span></span>
2. <span data-ttu-id="9d48f-155">Navigate to the settings blade of the SQL Database / SQL Server you want to audit.</span><span class="sxs-lookup"><span data-stu-id="9d48f-155">Navigate to the settings blade of the SQL Database / SQL Server you want to audit.</span></span> <span data-ttu-id="9d48f-156">In the Settings blade, select **Auditing & Threat detection** (*[see screenshot in Blob Auditing section](#auditing-screenshot)*).</span><span class="sxs-lookup"><span data-stu-id="9d48f-156">In the Settings blade, select **Auditing & Threat detection** (*[see screenshot in Blob Auditing section](#auditing-screenshot)*).</span></span>
3. <span data-ttu-id="9d48f-157">In the database auditing configuration blade, you can check the **Inherit settings from server** checkbox to designate that this database will be audited according to its server's settings.</span><span class="sxs-lookup"><span data-stu-id="9d48f-157">In the database auditing configuration blade, you can check the **Inherit settings from server** checkbox to designate that this database will be audited according to its server's settings.</span></span> <span data-ttu-id="9d48f-158">If this option is checked, you will see a **View server auditing settings** link that allows you to view or modify the server auditing settings from this context.</span><span class="sxs-lookup"><span data-stu-id="9d48f-158">If this option is checked, you will see a **View server auditing settings** link that allows you to view or modify the server auditing settings from this context.</span></span>

    ![Navigation pane][2]
4. <span data-ttu-id="9d48f-160">If you prefer not to inherit Auditing settings from server, **uncheck** the **Inherit Auditing settings from server** option, turn **ON** Auditing, and choose **Table** Auditing Type.</span><span class="sxs-lookup"><span data-stu-id="9d48f-160">If you prefer not to inherit Auditing settings from server, **uncheck** the **Inherit Auditing settings from server** option, turn **ON** Auditing, and choose **Table** Auditing Type.</span></span>

    ![Navigation pane][3-tbl]
5. <span data-ttu-id="9d48f-162">Select **Storage Details** to open the Audit Logs Storage Blade.</span><span class="sxs-lookup"><span data-stu-id="9d48f-162">Select **Storage Details** to open the Audit Logs Storage Blade.</span></span> <span data-ttu-id="9d48f-163">Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted.</span><span class="sxs-lookup"><span data-stu-id="9d48f-163">Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted.</span></span> <span data-ttu-id="9d48f-164">**Tip:** Use the same storage account for all audited databases to get the most out of the auditing reports templates (*[see screenshot in Blob Auditing section](#storage-screenshot)*).</span><span class="sxs-lookup"><span data-stu-id="9d48f-164">**Tip:** Use the same storage account for all audited databases to get the most out of the auditing reports templates (*[see screenshot in Blob Auditing section](#storage-screenshot)*).</span></span>
6. <span data-ttu-id="9d48f-165">Click on **Audited Events** to customize which events to audit.</span><span class="sxs-lookup"><span data-stu-id="9d48f-165">Click on **Audited Events** to customize which events to audit.</span></span> <span data-ttu-id="9d48f-166">In the **Logging by event** blade, click **Success** and **Failure** to log all events, or choose individual event categories.</span><span class="sxs-lookup"><span data-stu-id="9d48f-166">In the **Logging by event** blade, click **Success** and **Failure** to log all events, or choose individual event categories.</span></span>

   > <span data-ttu-id="9d48f-167">Customizing audited events can also be done via PowerShell or REST API - see the [Automation (PowerShell / REST API)](#subheading-7) section for more details.</span><span class="sxs-lookup"><span data-stu-id="9d48f-167">Customizing audited events can also be done via PowerShell or REST API - see the [Automation (PowerShell / REST API)](#subheading-7) section for more details.</span></span>

    ![Navigation pane][5]
7. <span data-ttu-id="9d48f-169">Once you've configured your auditing settings, you can turn on the new **Threat Detection** (preview) feature, and configure the emails to receive security alerts.</span><span class="sxs-lookup"><span data-stu-id="9d48f-169">Once you've configured your auditing settings, you can turn on the new **Threat Detection** (preview) feature, and configure the emails to receive security alerts.</span></span> <span data-ttu-id="9d48f-170">Threat Detection allows you to receive proactive alerts on anomalous database activities that may indicate potential security threats.</span><span class="sxs-lookup"><span data-stu-id="9d48f-170">Threat Detection allows you to receive proactive alerts on anomalous database activities that may indicate potential security threats.</span></span> <span data-ttu-id="9d48f-171">See [Getting Started with Threat Detection](sql-database-threat-detection-get-started.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="9d48f-171">See [Getting Started with Threat Detection](sql-database-threat-detection-get-started.md) for more details.</span></span>
8. <span data-ttu-id="9d48f-172">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9d48f-172">Click **Save**.</span></span>


## <a id="subheading-8"></a><span data-ttu-id="9d48f-173">Blob/table differences in server auditing policy inheritance</span><span class="sxs-lookup"><span data-stu-id="9d48f-173">Blob/table differences in server auditing policy inheritance</span></span>

###<a name="ablob-auditinga"></a><span data-ttu-id="9d48f-174"><a>Blob auditing</a></span><span class="sxs-lookup"><span data-stu-id="9d48f-174"><a>Blob auditing</a></span></span>

1. <span data-ttu-id="9d48f-175">If **Server Blob auditing is enabled**, it **always applies to the database** (i.e. the database will be audited), regardless of:</span><span class="sxs-lookup"><span data-stu-id="9d48f-175">If **Server Blob auditing is enabled**, it **always applies to the database** (i.e. the database will be audited), regardless of:</span></span>
    - <span data-ttu-id="9d48f-176">The database auditing settings.</span><span class="sxs-lookup"><span data-stu-id="9d48f-176">The database auditing settings.</span></span>
    - <span data-ttu-id="9d48f-177">Whether or not the "Inherit settings from server" checkbox is checked in the database blade.</span><span class="sxs-lookup"><span data-stu-id="9d48f-177">Whether or not the "Inherit settings from server" checkbox is checked in the database blade.</span></span>

2. <span data-ttu-id="9d48f-178">Enabling Blob auditing on the database, in addition to enabling it on the server, will **not** override or change any of the settings of the server Blob auditing - both audits will exist side by side.</span><span class="sxs-lookup"><span data-stu-id="9d48f-178">Enabling Blob auditing on the database, in addition to enabling it on the server, will **not** override or change any of the settings of the server Blob auditing - both audits will exist side by side.</span></span> <span data-ttu-id="9d48f-179">In other words, the database will be audited twice in parallel (once by the Server policy and once by the Database policy).</span><span class="sxs-lookup"><span data-stu-id="9d48f-179">In other words, the database will be audited twice in parallel (once by the Server policy and once by the Database policy).</span></span>

    > [!NOTE]
    > <span data-ttu-id="9d48f-180">You should avoid enabling both server Blob auditing and database Blob auditing together, unless:</span><span class="sxs-lookup"><span data-stu-id="9d48f-180">You should avoid enabling both server Blob auditing and database Blob auditing together, unless:</span></span>
    > * <span data-ttu-id="9d48f-181">You need to use a different *storage account* or *retention period* for a specific database.</span><span class="sxs-lookup"><span data-stu-id="9d48f-181">You need to use a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="9d48f-182">You want to audit different event types or categories for a specific database than are being audited for the rest of the databases on this server (e.g. if table inserts need to be audited only for a specific database).</span><span class="sxs-lookup"><span data-stu-id="9d48f-182">You want to audit different event types or categories for a specific database than are being audited for the rest of the databases on this server (e.g. if table inserts need to be audited only for a specific database).</span></span>
    > <br><br>
    > <span data-ttu-id="9d48f-183">Otherwise, it is **recommended to only enable server-level Blob Auditing** and leave the database-level auditing disabled for all databases.</span><span class="sxs-lookup"><span data-stu-id="9d48f-183">Otherwise, it is **recommended to only enable server-level Blob Auditing** and leave the database-level auditing disabled for all databases.</span></span>

###<a name="atable-auditinga-deprecated"></a><span data-ttu-id="9d48f-184"><a>Table auditing</a> (deprecated)</span><span class="sxs-lookup"><span data-stu-id="9d48f-184"><a>Table auditing</a> (deprecated)</span></span>

<span data-ttu-id="9d48f-185">If **server-level Table auditing is enabled**, it only applies to the database if the "Inherit settings from server" checkbox is checked in the database blade (this is checked by default for all existing and newly created databases).</span><span class="sxs-lookup"><span data-stu-id="9d48f-185">If **server-level Table auditing is enabled**, it only applies to the database if the "Inherit settings from server" checkbox is checked in the database blade (this is checked by default for all existing and newly created databases).</span></span>

- <span data-ttu-id="9d48f-186">If the checkbox is *checked*, any changes made to the auditing settings in database **override** the server settings for this database.</span><span class="sxs-lookup"><span data-stu-id="9d48f-186">If the checkbox is *checked*, any changes made to the auditing settings in database **override** the server settings for this database.</span></span>

- <span data-ttu-id="9d48f-187">If the checkbox is *unchecked* and the database-level auditing is disabled, the database will not be audited.</span><span class="sxs-lookup"><span data-stu-id="9d48f-187">If the checkbox is *unchecked* and the database-level auditing is disabled, the database will not be audited.</span></span>

## <a id="subheading-3"></a><span data-ttu-id="9d48f-188">Analyze audit logs and reports</span><span class="sxs-lookup"><span data-stu-id="9d48f-188">Analyze audit logs and reports</span></span>
<span data-ttu-id="9d48f-189">Audit logs are aggregated in the Azure storage account you chose during setup.</span><span class="sxs-lookup"><span data-stu-id="9d48f-189">Audit logs are aggregated in the Azure storage account you chose during setup.</span></span>

<span data-ttu-id="9d48f-190">You can explore audit logs using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="9d48f-190">You can explore audit logs using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="9d48f-191">See below specifics for analysis of both **Blob** and **Table** audit logs.</span><span class="sxs-lookup"><span data-stu-id="9d48f-191">See below specifics for analysis of both **Blob** and **Table** audit logs.</span></span>

### <span data-ttu-id="9d48f-192"><a id="subheading-3-1">Blob Auditing</a></span><span class="sxs-lookup"><span data-stu-id="9d48f-192"><a id="subheading-3-1">Blob Auditing</a></span></span>
<span data-ttu-id="9d48f-193">Blob Auditing logs are saved as a collection of blob files within a container named "**sqldbauditlogs**".</span><span class="sxs-lookup"><span data-stu-id="9d48f-193">Blob Auditing logs are saved as a collection of blob files within a container named "**sqldbauditlogs**".</span></span>

<span data-ttu-id="9d48f-194">For further details about the Blob audit logs storage folder hierarchy, blob naming convention, and log format, see the [Blob Audit Log Format Reference (doc file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="9d48f-194">For further details about the Blob audit logs storage folder hierarchy, blob naming convention, and log format, see the [Blob Audit Log Format Reference (doc file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="9d48f-195">There are several methods to view Blob Auditing logs:</span><span class="sxs-lookup"><span data-stu-id="9d48f-195">There are several methods to view Blob Auditing logs:</span></span>

1. <span data-ttu-id="9d48f-196">Through the [Azure portal](https://portal.azure.com) - open the relevant database.</span><span class="sxs-lookup"><span data-stu-id="9d48f-196">Through the [Azure portal](https://portal.azure.com) - open the relevant database.</span></span> <span data-ttu-id="9d48f-197">At the top of the database's **Auditing & Threat detection** blade, click on **View audit logs**.</span><span class="sxs-lookup"><span data-stu-id="9d48f-197">At the top of the database's **Auditing & Threat detection** blade, click on **View audit logs**.</span></span>

    ![Navigation Pane][10]

    <span data-ttu-id="9d48f-199">An **Audit records** blade will open, where you'll be able to view the logs.</span><span class="sxs-lookup"><span data-stu-id="9d48f-199">An **Audit records** blade will open, where you'll be able to view the logs.</span></span>

    - <span data-ttu-id="9d48f-200">You can choose to view specific dates by clicking on **Filter** at the top area of the Audit records blade</span><span class="sxs-lookup"><span data-stu-id="9d48f-200">You can choose to view specific dates by clicking on **Filter** at the top area of the Audit records blade</span></span>
    - <span data-ttu-id="9d48f-201">You can toggle between audit records that were created by server policy or database policy audit</span><span class="sxs-lookup"><span data-stu-id="9d48f-201">You can toggle between audit records that were created by server policy or database policy audit</span></span>

    ![Navigation Pane][11]
2. <span data-ttu-id="9d48f-203">Download log files from your Azure Storage Blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="9d48f-203">Download log files from your Azure Storage Blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

    <span data-ttu-id="9d48f-204">Once you have downloaded the log file locally, you can double-click the file to open, view and analyze the logs in SSMS.</span><span class="sxs-lookup"><span data-stu-id="9d48f-204">Once you have downloaded the log file locally, you can double-click the file to open, view and analyze the logs in SSMS.</span></span>

    <span data-ttu-id="9d48f-205">Additional methods:</span><span class="sxs-lookup"><span data-stu-id="9d48f-205">Additional methods:</span></span>

   * <span data-ttu-id="9d48f-206">You can **download multiple files simultaneously** via Azure Storage Explorer - right-click on a specific subfolder (e.g. a subfolder that includes all log files for a specific date) and choose "Save as" to save in a local folder.</span><span class="sxs-lookup"><span data-stu-id="9d48f-206">You can **download multiple files simultaneously** via Azure Storage Explorer - right-click on a specific subfolder (e.g. a subfolder that includes all log files for a specific date) and choose "Save as" to save in a local folder.</span></span>

       <span data-ttu-id="9d48f-207">After downloading several files (or an entire day, as described above), you can merge them locally as follows:</span><span class="sxs-lookup"><span data-stu-id="9d48f-207">After downloading several files (or an entire day, as described above), you can merge them locally as follows:</span></span>

       <span data-ttu-id="9d48f-208">**Open SSMS -> File -> Open -> Merge Extended Events -> Choose all files to merge**</span><span class="sxs-lookup"><span data-stu-id="9d48f-208">**Open SSMS -> File -> Open -> Merge Extended Events -> Choose all files to merge**</span></span>
   * <span data-ttu-id="9d48f-209">Programmatically:</span><span class="sxs-lookup"><span data-stu-id="9d48f-209">Programmatically:</span></span>

     * <span data-ttu-id="9d48f-210">Extended Events Reader **C# library** ([more info here](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/))</span><span class="sxs-lookup"><span data-stu-id="9d48f-210">Extended Events Reader **C# library** ([more info here](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/))</span></span>
     * <span data-ttu-id="9d48f-211">Querying Extended Events Files Using **PowerShell** ([more info here](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/))</span><span class="sxs-lookup"><span data-stu-id="9d48f-211">Querying Extended Events Files Using **PowerShell** ([more info here](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/))</span></span>

3. <span data-ttu-id="9d48f-212">We have created a **sample application** that runs in Azure and utilizes OMS public APIs to push SQL audit logs into OMS for consumption via the OMS dashboard ([more info here](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration)).</span><span class="sxs-lookup"><span data-stu-id="9d48f-212">We have created a **sample application** that runs in Azure and utilizes OMS public APIs to push SQL audit logs into OMS for consumption via the OMS dashboard ([more info here](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration)).</span></span>

### <span data-ttu-id="9d48f-213"><a id="subheading-3-2">Table auditing</a> (deprecated)</span><span class="sxs-lookup"><span data-stu-id="9d48f-213"><a id="subheading-3-2">Table auditing</a> (deprecated)</span></span>
<span data-ttu-id="9d48f-214">Table Auditing logs are saved as a collection of Azure Storage Tables with a **SQLDBAuditLogs** prefix.</span><span class="sxs-lookup"><span data-stu-id="9d48f-214">Table Auditing logs are saved as a collection of Azure Storage Tables with a **SQLDBAuditLogs** prefix.</span></span>

<span data-ttu-id="9d48f-215">For further details about the Table audit log format, see the [Table Audit Log Format Reference (doc file download)](http://go.microsoft.com/fwlink/?LinkId=506733).</span><span class="sxs-lookup"><span data-stu-id="9d48f-215">For further details about the Table audit log format, see the [Table Audit Log Format Reference (doc file download)](http://go.microsoft.com/fwlink/?LinkId=506733).</span></span>

<span data-ttu-id="9d48f-216">There are several methods to view Table Auditing logs:</span><span class="sxs-lookup"><span data-stu-id="9d48f-216">There are several methods to view Table Auditing logs:</span></span>

1. <span data-ttu-id="9d48f-217">Through the [Azure portal](https://portal.azure.com) - open the relevant database.</span><span class="sxs-lookup"><span data-stu-id="9d48f-217">Through the [Azure portal](https://portal.azure.com) - open the relevant database.</span></span> <span data-ttu-id="9d48f-218">At the top of the database's **Auditing & Threat detection** blade, click on **View audit logs**.</span><span class="sxs-lookup"><span data-stu-id="9d48f-218">At the top of the database's **Auditing & Threat detection** blade, click on **View audit logs**.</span></span>

    ![Navigation Pane][10]

    <span data-ttu-id="9d48f-220">An **Audit records** blade will open, where you'll be able to view the logs.</span><span class="sxs-lookup"><span data-stu-id="9d48f-220">An **Audit records** blade will open, where you'll be able to view the logs.</span></span>

    * <span data-ttu-id="9d48f-221">You can choose to view specific dates by clicking on **Filter** at the top area of the Audit records blade</span><span class="sxs-lookup"><span data-stu-id="9d48f-221">You can choose to view specific dates by clicking on **Filter** at the top area of the Audit records blade</span></span>
    * <span data-ttu-id="9d48f-222">You can download and view the audit logs in Excel format by clicking on **Open in Excel** at the top area of the Audit records blade</span><span class="sxs-lookup"><span data-stu-id="9d48f-222">You can download and view the audit logs in Excel format by clicking on **Open in Excel** at the top area of the Audit records blade</span></span>

    ![Navigation Pane][12]

2. <span data-ttu-id="9d48f-224">Alternatively, a preconfigured report template is available as a [downloadable Excel spreadsheet](http://go.microsoft.com/fwlink/?LinkId=403540) to help you quickly analyze log data.</span><span class="sxs-lookup"><span data-stu-id="9d48f-224">Alternatively, a preconfigured report template is available as a [downloadable Excel spreadsheet](http://go.microsoft.com/fwlink/?LinkId=403540) to help you quickly analyze log data.</span></span> <span data-ttu-id="9d48f-225">To use the template on your audit logs, you need Excel 2013 or later and Power Query, which you can download [here](http://www.microsoft.com/download/details.aspx?id=39379).</span><span class="sxs-lookup"><span data-stu-id="9d48f-225">To use the template on your audit logs, you need Excel 2013 or later and Power Query, which you can download [here](http://www.microsoft.com/download/details.aspx?id=39379).</span></span>

    <span data-ttu-id="9d48f-226">You can also import your audit logs into the Excel template directly from your Azure storage account using Power Query.</span><span class="sxs-lookup"><span data-stu-id="9d48f-226">You can also import your audit logs into the Excel template directly from your Azure storage account using Power Query.</span></span> <span data-ttu-id="9d48f-227">You can then explore your audit records and create dashboards and reports on top of the log data.</span><span class="sxs-lookup"><span data-stu-id="9d48f-227">You can then explore your audit records and create dashboards and reports on top of the log data.</span></span>

    ![Navigation Pane][9]

## <a id="subheading-5"></a><span data-ttu-id="9d48f-229">Practices for usage in production</span><span class="sxs-lookup"><span data-stu-id="9d48f-229">Practices for usage in production</span></span>
<!--The description in this section refers to screen captures above.-->

### <span data-ttu-id="9d48f-230"><a id="subheading-6">Auditing geo-replicated databases</a></span><span class="sxs-lookup"><span data-stu-id="9d48f-230"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="9d48f-231">When using Geo-replicated databases, it is possible to set up Auditing on either the Primary database, the Secondary database, or both, depending on the Audit type.</span><span class="sxs-lookup"><span data-stu-id="9d48f-231">When using Geo-replicated databases, it is possible to set up Auditing on either the Primary database, the Secondary database, or both, depending on the Audit type.</span></span>

<span data-ttu-id="9d48f-232">**Table Auditing** - you can configure a separate policy, on either the database or the server level, for each of the two databases (Primary and Secondary) as described in [Set up auditing for your database](#subheading-2-2) section.</span><span class="sxs-lookup"><span data-stu-id="9d48f-232">**Table Auditing** - you can configure a separate policy, on either the database or the server level, for each of the two databases (Primary and Secondary) as described in [Set up auditing for your database](#subheading-2-2) section.</span></span>

<span data-ttu-id="9d48f-233">**Blob auditing** - follow these instructions:</span><span class="sxs-lookup"><span data-stu-id="9d48f-233">**Blob auditing** - follow these instructions:</span></span>

1. <span data-ttu-id="9d48f-234">**Primary database** - turn on **Blob Auditing** either on the server or the database itself, as described in [Set up auditing for your database](#subheading-2-1) section.</span><span class="sxs-lookup"><span data-stu-id="9d48f-234">**Primary database** - turn on **Blob Auditing** either on the server or the database itself, as described in [Set up auditing for your database](#subheading-2-1) section.</span></span>
2. <span data-ttu-id="9d48f-235">**Secondary database** - Blob Auditing can only be turned on/off from the Primary database auditing settings.</span><span class="sxs-lookup"><span data-stu-id="9d48f-235">**Secondary database** - Blob Auditing can only be turned on/off from the Primary database auditing settings.</span></span>

   * <span data-ttu-id="9d48f-236">Turn on **Blob Auditing** on the **Primary database**, as described in [Set up auditing for your database](#subheading-2-1) section.</span><span class="sxs-lookup"><span data-stu-id="9d48f-236">Turn on **Blob Auditing** on the **Primary database**, as described in [Set up auditing for your database](#subheading-2-1) section.</span></span> <span data-ttu-id="9d48f-237">Blob Auditing must be enabled on the *primary database itself*, not the server.</span><span class="sxs-lookup"><span data-stu-id="9d48f-237">Blob Auditing must be enabled on the *primary database itself*, not the server.</span></span>
   * <span data-ttu-id="9d48f-238">Once Blob Auditing is enabled on the Primary database, it will also become enabled on the Secondary database.</span><span class="sxs-lookup"><span data-stu-id="9d48f-238">Once Blob Auditing is enabled on the Primary database, it will also become enabled on the Secondary database.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9d48f-239">By default, the **storage settings** for the Secondary database will be identical to those of the Primary database, causing **cross-regional traffic**.</span><span class="sxs-lookup"><span data-stu-id="9d48f-239">By default, the **storage settings** for the Secondary database will be identical to those of the Primary database, causing **cross-regional traffic**.</span></span> <span data-ttu-id="9d48f-240">You can avoid this by enabling Blob Auditing on the **Secondary server** and configuring a **local storage** in the Secondary server storage settings (this will override the storage location for the Secondary database and result in each database saving the Audit logs to a local storage).</span><span class="sxs-lookup"><span data-stu-id="9d48f-240">You can avoid this by enabling Blob Auditing on the **Secondary server** and configuring a **local storage** in the Secondary server storage settings (this will override the storage location for the Secondary database and result in each database saving the Audit logs to a local storage).</span></span>  

<br>

### <span data-ttu-id="9d48f-241"><a id="subheading-6">Storage key regeneration</a></span><span class="sxs-lookup"><span data-stu-id="9d48f-241"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="9d48f-242">In production, you are likely to refresh your storage keys periodically.</span><span class="sxs-lookup"><span data-stu-id="9d48f-242">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="9d48f-243">When refreshing your keys, you need to re-save the auditing policy.</span><span class="sxs-lookup"><span data-stu-id="9d48f-243">When refreshing your keys, you need to re-save the auditing policy.</span></span> <span data-ttu-id="9d48f-244">The process is as follows:</span><span class="sxs-lookup"><span data-stu-id="9d48f-244">The process is as follows:</span></span>

1. <span data-ttu-id="9d48f-245">In the storage details blade switch the **Storage Access Key** from *Primary* to *Secondary*, and then click **OK** at the bottom.</span><span class="sxs-lookup"><span data-stu-id="9d48f-245">In the storage details blade switch the **Storage Access Key** from *Primary* to *Secondary*, and then click **OK** at the bottom.</span></span> <span data-ttu-id="9d48f-246">Then click **SAVE** at the top of the auditing configuration blade.</span><span class="sxs-lookup"><span data-stu-id="9d48f-246">Then click **SAVE** at the top of the auditing configuration blade.</span></span>

    ![Navigation Pane][6]
2. <span data-ttu-id="9d48f-248">Go to the storage configuration blade and **regenerate** the *Primary Access Key*.</span><span class="sxs-lookup"><span data-stu-id="9d48f-248">Go to the storage configuration blade and **regenerate** the *Primary Access Key*.</span></span>

    ![Navigation Pane][8]
3. <span data-ttu-id="9d48f-250">Go back to the auditing configuration blade, switch the **Storage Access Key** from *Secondary* to *Primary*, and then click **OK** at the bottom.</span><span class="sxs-lookup"><span data-stu-id="9d48f-250">Go back to the auditing configuration blade, switch the **Storage Access Key** from *Secondary* to *Primary*, and then click **OK** at the bottom.</span></span> <span data-ttu-id="9d48f-251">Then click **SAVE** at the top of the auditing configuration blade.</span><span class="sxs-lookup"><span data-stu-id="9d48f-251">Then click **SAVE** at the top of the auditing configuration blade.</span></span>
4. <span data-ttu-id="9d48f-252">Go back to the storage configuration blade and **regenerate** the *Secondary Access Key* (in preparation for the next keys refresh cycle).</span><span class="sxs-lookup"><span data-stu-id="9d48f-252">Go back to the storage configuration blade and **regenerate** the *Secondary Access Key* (in preparation for the next keys refresh cycle).</span></span>

## <a id="subheading-7"></a><span data-ttu-id="9d48f-253">Automation (PowerShell / REST API)</span><span class="sxs-lookup"><span data-stu-id="9d48f-253">Automation (PowerShell / REST API)</span></span>
<span data-ttu-id="9d48f-254">You can also configure Auditing in Azure SQL Database using the following automation tools:</span><span class="sxs-lookup"><span data-stu-id="9d48f-254">You can also configure Auditing in Azure SQL Database using the following automation tools:</span></span>

1. <span data-ttu-id="9d48f-255">**PowerShell cmdlets**</span><span class="sxs-lookup"><span data-stu-id="9d48f-255">**PowerShell cmdlets**</span></span>

   * <span data-ttu-id="9d48f-256">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="9d48f-256">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="9d48f-257">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="9d48f-257">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="9d48f-258">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="9d48f-258">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="9d48f-259">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="9d48f-259">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="9d48f-260">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="9d48f-260">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="9d48f-261">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="9d48f-261">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="9d48f-262">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="9d48f-262">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="9d48f-263">For an script example, see [Configure auditing and threat detectoin using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9d48f-263">For an script example, see [Configure auditing and threat detectoin using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

2. <span data-ttu-id="9d48f-264">**REST API - Blob Auditing**</span><span class="sxs-lookup"><span data-stu-id="9d48f-264">**REST API - Blob Auditing**</span></span>

   * [<span data-ttu-id="9d48f-265">Create or Update Database Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="9d48f-265">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="9d48f-266">Create or Update Server Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="9d48f-266">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="9d48f-267">Get Database Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="9d48f-267">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="9d48f-268">Get Server Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="9d48f-268">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="9d48f-269">Get Server Blob Auditing Operation Result</span><span class="sxs-lookup"><span data-stu-id="9d48f-269">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)
3. <span data-ttu-id="9d48f-270">**REST API - Table Auditing (deprecated)**</span><span class="sxs-lookup"><span data-stu-id="9d48f-270">**REST API - Table Auditing (deprecated)**</span></span>

   * [<span data-ttu-id="9d48f-271">Create or Update Database Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="9d48f-271">Create or Update Database Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt604471.aspx)
   * [<span data-ttu-id="9d48f-272">Create or Update Server Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="9d48f-272">Create or Update Server Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt604383.aspx)
   * [<span data-ttu-id="9d48f-273">Get Database Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="9d48f-273">Get Database Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt604381.aspx)
   * [<span data-ttu-id="9d48f-274">Get Server Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="9d48f-274">Get Server Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt604382.aspx)

<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[3-tbl]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-auditing-get-started/3_auditing_get_started_turn_on_table.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-auditing-get-started/5_auditing_get_started_audited_events.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-auditing-get-started/6_auditing_get_started_storage_key_regeneration.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-auditing-get-started/7_auditing_get_started_activity_log.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-auditing-get-started/8_auditing_get_started_regenerate_key.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-auditing-get-started/9_auditing_get_started_report_template.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-auditing-get-started/10_auditing_get_started_blob_view_audit_logs.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-auditing-get-started/11_auditing_get_started_blob_audit_records.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-auditing-get-started/12_auditing_get_started_table_audit_records.png

[101]: https://msdn.microsoft.com/library/azure/mt603731(v=azure.200).aspx
[102]: https://msdn.microsoft.com/library/azure/mt619329(v=azure.200).aspx
[103]: https://msdn.microsoft.com/library/azure/mt603796(v=azure.200).aspx
[104]: https://msdn.microsoft.com/library/azure/mt603574(v=azure.200).aspx
[105]: https://msdn.microsoft.com/library/azure/mt603531(v=azure.200).aspx
[106]: https://msdn.microsoft.com/library/azure/mt603794(v=azure.200).aspx
[107]: https://msdn.microsoft.com/library/azure/mt619353(v=azure.200).aspx













