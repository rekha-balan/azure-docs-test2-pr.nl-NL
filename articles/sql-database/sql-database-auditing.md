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
# <a name="get-started-with-sql-database-auditing"></a>Get started with SQL database auditing
Azure SQL Database Auditing tracks database events and writes them to an audit log in your Azure Storage account.

Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.

Auditing enables and facilitates adherence to compliance standards but doesn't guarantee compliance. For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).

* [Azure SQL Database Auditing overview]
* [Set up auditing for your database]
* [Analyze audit logs and reports]

## <a id="subheading-1"></a>Azure SQL Database auditing overview
SQL Database Auditing allows you to:

* **Retain** an audit trail of selected events. You can define categories of database actions to be audited.
* **Report** on database activity. You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.
* **Analyze** reports. You can find suspicious events, unusual activity, and trends.

There are two **Auditing methods**:

* **Blob Auditing** - logs are written to Azure Blob Storage. This is a newer auditing method, which provides **higher performance**, supports **higher granularity object-level auditing**, and is **more cost effective**. Blob Auditing will be replacing Table Auditing.
* **Table Auditing (deprecated)** - logs are written to Azure Table Storage.

> [!IMPORTANT]
> The introduction of the new Blob Auditing brings a major change to the way server auditing policy is being inherited by the database. See [Blob/Table differences in server auditing policy inheritance](#subheading-8) section for additional details.

You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.

<!--For each Event Category, auditing of **Success** and **Failure** operations are configured separately.-->

An auditing policy can be defined for a specific database or as a default server policy. A default server auditing policy applies to all existing and newly created databases on a server.

## <a id="subheading-2"></a>Set up auditing for your database
The following section describes the configuration of auditing using the Azure portal.

### <a id="subheading-2-1">Blob Auditing</a>
1. Launch the [Azure portal](https://portal.azure.com) at https://portal.azure.com.
2. Navigate to the settings blade of the SQL Database / SQL Server you want to audit. In the Settings blade, select **Auditing & Threat detection**.

    <a id="auditing-screenshot"></a> ![Navigation pane][1]
3. In the database auditing configuration blade, you can check the **Inherit settings from server** checkbox to designate that this database will be audited according to its server's settings. If this option is checked, you will see a **View server auditing settings** link that allows you to view or modify the server auditing settings from this context.

    ![Navigation pane][2]
4. If you prefer to enable Blob Auditing on the database-level (in addition or instead of server-level auditing), **uncheck** the **Inherit Auditing settings from server** option, turn **ON** Auditing, and choose the **Blob** Auditing Type.

   > If server Blob auditing is enabled, the database configured audit will exist side by side with the server Blob audit.  

    ![Navigation pane][3]
5. Select **Storage Details** to open the Audit Logs Storage Blade. Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted, then click **OK** at the bottom. **Tip:** Use the same storage account for all audited databases to get the most out of the auditing reports templates.

    <a id="storage-screenshot"></a> ![Navigation pane][4]
6. If you want to customize the audited events, you can do this via PowerShell or REST API - see the [Automation (PowerShell / REST API)](#subheading-7) section for more details.
7. Once you've configured your auditing settings, you can turn on the new **Threat Detection** (preview) feature, and configure the emails to receive security alerts. Threat Detection allows you to receive proactive alerts on anomalous database activities that may indicate potential security threats. See [Getting Started with Threat Detection](sql-database-threat-detection-get-started.md) for more details.
8. Click **Save**.

### <a id="subheading-2-2">Table Auditing</a> (deprecated)

> Before setting up **Table Auditing**, check if you are using a ["Downlevel Client"](sql-database-auditing-and-dynamic-data-masking-downlevel-clients.md). Also, if you have strict firewall settings, please note that the [IP endpoint of your database will change](sql-database-auditing-and-dynamic-data-masking-downlevel-clients.md) when enabling Table Auditing.


1. Launch the [Azure portal](https://portal.azure.com) at https://portal.azure.com.
2. Navigate to the settings blade of the SQL Database / SQL Server you want to audit. In the Settings blade, select **Auditing & Threat detection** (*[see screenshot in Blob Auditing section](#auditing-screenshot)*).
3. In the database auditing configuration blade, you can check the **Inherit settings from server** checkbox to designate that this database will be audited according to its server's settings. If this option is checked, you will see a **View server auditing settings** link that allows you to view or modify the server auditing settings from this context.

    ![Navigation pane][2]
4. If you prefer not to inherit Auditing settings from server, **uncheck** the **Inherit Auditing settings from server** option, turn **ON** Auditing, and choose **Table** Auditing Type.

    ![Navigation pane][3-tbl]
5. Select **Storage Details** to open the Audit Logs Storage Blade. Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted. **Tip:** Use the same storage account for all audited databases to get the most out of the auditing reports templates (*[see screenshot in Blob Auditing section](#storage-screenshot)*).
6. Click on **Audited Events** to customize which events to audit. In the **Logging by event** blade, click **Success** and **Failure** to log all events, or choose individual event categories.

   > Customizing audited events can also be done via PowerShell or REST API - see the [Automation (PowerShell / REST API)](#subheading-7) section for more details.

    ![Navigation pane][5]
7. Once you've configured your auditing settings, you can turn on the new **Threat Detection** (preview) feature, and configure the emails to receive security alerts. Threat Detection allows you to receive proactive alerts on anomalous database activities that may indicate potential security threats. See [Getting Started with Threat Detection](sql-database-threat-detection-get-started.md) for more details.
8. Click **Save**.


## <a id="subheading-8"></a>Blob/table differences in server auditing policy inheritance

###<a name="ablob-auditinga"></a><a>Blob auditing</a>

1. If **Server Blob auditing is enabled**, it **always applies to the database** (i.e. the database will be audited), regardless of:
    - The database auditing settings.
    - Whether or not the "Inherit settings from server" checkbox is checked in the database blade.

2. Enabling Blob auditing on the database, in addition to enabling it on the server, will **not** override or change any of the settings of the server Blob auditing - both audits will exist side by side. In other words, the database will be audited twice in parallel (once by the Server policy and once by the Database policy).

    > [!NOTE]
    > You should avoid enabling both server Blob auditing and database Blob auditing together, unless:
    > * You need to use a different *storage account* or *retention period* for a specific database.
    > * You want to audit different event types or categories for a specific database than are being audited for the rest of the databases on this server (e.g. if table inserts need to be audited only for a specific database).
    > <br><br>
    > Otherwise, it is **recommended to only enable server-level Blob Auditing** and leave the database-level auditing disabled for all databases.

###<a name="atable-auditinga-deprecated"></a><a>Table auditing</a> (deprecated)

If **server-level Table auditing is enabled**, it only applies to the database if the "Inherit settings from server" checkbox is checked in the database blade (this is checked by default for all existing and newly created databases).

- If the checkbox is *checked*, any changes made to the auditing settings in database **override** the server settings for this database.

- If the checkbox is *unchecked* and the database-level auditing is disabled, the database will not be audited.

## <a id="subheading-3"></a>Analyze audit logs and reports
Audit logs are aggregated in the Azure storage account you chose during setup.

You can explore audit logs using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).

See below specifics for analysis of both **Blob** and **Table** audit logs.

### <a id="subheading-3-1">Blob Auditing</a>
Blob Auditing logs are saved as a collection of blob files within a container named "**sqldbauditlogs**".

For further details about the Blob audit logs storage folder hierarchy, blob naming convention, and log format, see the [Blob Audit Log Format Reference (doc file download)](https://go.microsoft.com/fwlink/?linkid=829599).

There are several methods to view Blob Auditing logs:

1. Through the [Azure portal](https://portal.azure.com) - open the relevant database. At the top of the database's **Auditing & Threat detection** blade, click on **View audit logs**.

    ![Navigation Pane][10]

    An **Audit records** blade will open, where you'll be able to view the logs.

    - You can choose to view specific dates by clicking on **Filter** at the top area of the Audit records blade
    - You can toggle between audit records that were created by server policy or database policy audit

    ![Navigation Pane][11]
2. Download log files from your Azure Storage Blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).

    Once you have downloaded the log file locally, you can double-click the file to open, view and analyze the logs in SSMS.

    Additional methods:

   * You can **download multiple files simultaneously** via Azure Storage Explorer - right-click on a specific subfolder (e.g. a subfolder that includes all log files for a specific date) and choose "Save as" to save in a local folder.

       After downloading several files (or an entire day, as described above), you can merge them locally as follows:

       **Open SSMS -> File -> Open -> Merge Extended Events -> Choose all files to merge**
   * Programmatically:

     * Extended Events Reader **C# library** ([more info here](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/))
     * Querying Extended Events Files Using **PowerShell** ([more info here](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/))

3. We have created a **sample application** that runs in Azure and utilizes OMS public APIs to push SQL audit logs into OMS for consumption via the OMS dashboard ([more info here](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration)).

### <a id="subheading-3-2">Table auditing</a> (deprecated)
Table Auditing logs are saved as a collection of Azure Storage Tables with a **SQLDBAuditLogs** prefix.

For further details about the Table audit log format, see the [Table Audit Log Format Reference (doc file download)](http://go.microsoft.com/fwlink/?LinkId=506733).

There are several methods to view Table Auditing logs:

1. Through the [Azure portal](https://portal.azure.com) - open the relevant database. At the top of the database's **Auditing & Threat detection** blade, click on **View audit logs**.

    ![Navigation Pane][10]

    An **Audit records** blade will open, where you'll be able to view the logs.

    * You can choose to view specific dates by clicking on **Filter** at the top area of the Audit records blade
    * You can download and view the audit logs in Excel format by clicking on **Open in Excel** at the top area of the Audit records blade

    ![Navigation Pane][12]

2. Alternatively, a preconfigured report template is available as a [downloadable Excel spreadsheet](http://go.microsoft.com/fwlink/?LinkId=403540) to help you quickly analyze log data. To use the template on your audit logs, you need Excel 2013 or later and Power Query, which you can download [here](http://www.microsoft.com/download/details.aspx?id=39379).

    You can also import your audit logs into the Excel template directly from your Azure storage account using Power Query. You can then explore your audit records and create dashboards and reports on top of the log data.

    ![Navigation Pane][9]

## <a id="subheading-5"></a>Practices for usage in production
<!--The description in this section refers to screen captures above.-->

### <a id="subheading-6">Auditing geo-replicated databases</a>
When using Geo-replicated databases, it is possible to set up Auditing on either the Primary database, the Secondary database, or both, depending on the Audit type.

**Table Auditing** - you can configure a separate policy, on either the database or the server level, for each of the two databases (Primary and Secondary) as described in [Set up auditing for your database](#subheading-2-2) section.

**Blob auditing** - follow these instructions:

1. **Primary database** - turn on **Blob Auditing** either on the server or the database itself, as described in [Set up auditing for your database](#subheading-2-1) section.
2. **Secondary database** - Blob Auditing can only be turned on/off from the Primary database auditing settings.

   * Turn on **Blob Auditing** on the **Primary database**, as described in [Set up auditing for your database](#subheading-2-1) section. Blob Auditing must be enabled on the *primary database itself*, not the server.
   * Once Blob Auditing is enabled on the Primary database, it will also become enabled on the Secondary database.

    > [!IMPORTANT]
    > By default, the **storage settings** for the Secondary database will be identical to those of the Primary database, causing **cross-regional traffic**. You can avoid this by enabling Blob Auditing on the **Secondary server** and configuring a **local storage** in the Secondary server storage settings (this will override the storage location for the Secondary database and result in each database saving the Audit logs to a local storage).  

<br>

### <a id="subheading-6">Storage key regeneration</a>
In production, you are likely to refresh your storage keys periodically. When refreshing your keys, you need to re-save the auditing policy. The process is as follows:

1. In the storage details blade switch the **Storage Access Key** from *Primary* to *Secondary*, and then click **OK** at the bottom. Then click **SAVE** at the top of the auditing configuration blade.

    ![Navigation Pane][6]
2. Go to the storage configuration blade and **regenerate** the *Primary Access Key*.

    ![Navigation Pane][8]
3. Go back to the auditing configuration blade, switch the **Storage Access Key** from *Secondary* to *Primary*, and then click **OK** at the bottom. Then click **SAVE** at the top of the auditing configuration blade.
4. Go back to the storage configuration blade and **regenerate** the *Secondary Access Key* (in preparation for the next keys refresh cycle).

## <a id="subheading-7"></a>Automation (PowerShell / REST API)
You can also configure Auditing in Azure SQL Database using the following automation tools:

1. **PowerShell cmdlets**

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Use-AzureRMSqlServerAuditingPolicy][107]

   For an script example, see [Configure auditing and threat detectoin using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

2. **REST API - Blob Auditing**

   * [Create or Update Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [Create or Update Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [Get Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [Get Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [Get Server Blob Auditing Operation Result](https://msdn.microsoft.com/library/azure/mt771862.aspx)
3. **REST API - Table Auditing (deprecated)**

   * [Create or Update Database Auditing Policy](https://msdn.microsoft.com/library/azure/mt604471.aspx)
   * [Create or Update Server Auditing Policy](https://msdn.microsoft.com/library/azure/mt604383.aspx)
   * [Get Database Auditing Policy](https://msdn.microsoft.com/library/azure/mt604381.aspx)
   * [Get Server Auditing Policy](https://msdn.microsoft.com/library/azure/mt604382.aspx)

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













