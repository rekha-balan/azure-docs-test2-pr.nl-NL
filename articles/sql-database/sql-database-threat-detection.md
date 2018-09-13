---
title: Threat Detection - Azure SQL Database | Microsoft Docs
description: Threat Detection detects anomalous database activities indicating potential security threats to the database.
services: sql-database
documentationcenter: ''
author: ronitr
manager: jhubbard
editor: v-romcal
ms.assetid: b50d232a-4225-46ed-91e7-75288f55ee84
ms.service: sql-database
ms.custom: security-protect
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 07/10/2016
ms.author: ronmat; ronitr
ms.openlocfilehash: c7fc2c29c9478e1a9f8c1df4f2ffd2548c4390c4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554304"
---
# <a name="sql-database-threat-detection"></a><span data-ttu-id="c42b4-103">SQL Database Threat Detection</span><span class="sxs-lookup"><span data-stu-id="c42b4-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="c42b4-104">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span><span class="sxs-lookup"><span data-stu-id="c42b4-104">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span>  <span data-ttu-id="c42b4-105">Threat Detection is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="c42b4-105">Threat Detection is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="c42b4-106">Overview</span><span class="sxs-lookup"><span data-stu-id="c42b4-106">Overview</span></span>

<span data-ttu-id="c42b4-107">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span><span class="sxs-lookup"><span data-stu-id="c42b4-107">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="c42b4-108">Users can explore the suspicious events using [SQL Database Auditing](sql-database-auditing.md) to determine if they result from an attempt to access, breach or exploit data in the database.</span><span class="sxs-lookup"><span data-stu-id="c42b4-108">Users can explore the suspicious events using [SQL Database Auditing](sql-database-auditing.md) to determine if they result from an attempt to access, breach or exploit data in the database.</span></span>
<span data-ttu-id="c42b4-109">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span><span class="sxs-lookup"><span data-stu-id="c42b4-109">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="c42b4-110">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span><span class="sxs-lookup"><span data-stu-id="c42b4-110">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="c42b4-111">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span><span class="sxs-lookup"><span data-stu-id="c42b4-111">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="c42b4-112">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span><span class="sxs-lookup"><span data-stu-id="c42b4-112">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

## <a name="set-up-threat-detection-for-your-database-in-the-azure-portal"></a><span data-ttu-id="c42b4-113">Set up threat detection for your database in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c42b4-113">Set up threat detection for your database in the Azure portal</span></span>
1. <span data-ttu-id="c42b4-114">Launch the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c42b4-114">Launch the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c42b4-115">Navigate to the configuration blade of the SQL Database you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="c42b4-115">Navigate to the configuration blade of the SQL Database you want to monitor.</span></span> <span data-ttu-id="c42b4-116">In the Settings blade, select **Auditing & Threat Detection**.</span><span class="sxs-lookup"><span data-stu-id="c42b4-116">In the Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Navigation pane][1]
3. <span data-ttu-id="c42b4-118">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the threat detection settings.</span><span class="sxs-lookup"><span data-stu-id="c42b4-118">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the threat detection settings.</span></span>
   
    ![Navigation pane][2]
4. <span data-ttu-id="c42b4-120">Turn **ON** threat detection.</span><span class="sxs-lookup"><span data-stu-id="c42b4-120">Turn **ON** threat detection.</span></span>
5. <span data-ttu-id="c42b4-121">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span><span class="sxs-lookup"><span data-stu-id="c42b4-121">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="c42b4-122">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection policy.</span><span class="sxs-lookup"><span data-stu-id="c42b4-122">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection policy.</span></span>
   
    ![Navigation pane][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="c42b4-124">Set up threat detection using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c42b4-124">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="c42b4-125">For an script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c42b4-125">For an script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="c42b4-126">Explore anomalous database activities upon detection of a suspicious event</span><span class="sxs-lookup"><span data-stu-id="c42b4-126">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="c42b4-127">You will receive an email notification upon detection of anomalous database activities.</span><span class="sxs-lookup"><span data-stu-id="c42b4-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="c42b4-128">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span><span class="sxs-lookup"><span data-stu-id="c42b4-128">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="c42b4-129">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span><span class="sxs-lookup"><span data-stu-id="c42b4-129">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
   
    ![Navigation pane][4]
2. <span data-ttu-id="c42b4-131">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure portal and show the relevant Auditing records around the time of the suspicious event.</span><span class="sxs-lookup"><span data-stu-id="c42b4-131">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure portal and show the relevant Auditing records around the time of the suspicious event.</span></span>
   
    ![Navigation pane][5]
3. <span data-ttu-id="c42b4-133">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span><span class="sxs-lookup"><span data-stu-id="c42b4-133">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Navigation pane][6]
4. <span data-ttu-id="c42b4-135">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span><span class="sxs-lookup"><span data-stu-id="c42b4-135">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span><br/>
   <span data-ttu-id="c42b4-136">**Note:** In Excel 2010 or later, Power Query and the **Fast Combine** setting is required.</span><span class="sxs-lookup"><span data-stu-id="c42b4-136">**Note:** In Excel 2010 or later, Power Query and the **Fast Combine** setting is required.</span></span>
   
    ![Navigation pane][7]
5. <span data-ttu-id="c42b4-138">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span><span class="sxs-lookup"><span data-stu-id="c42b4-138">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="c42b4-139">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span><span class="sxs-lookup"><span data-stu-id="c42b4-139">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>
   
    ![Navigation pane][8]
6. <span data-ttu-id="c42b4-141">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span><span class="sxs-lookup"><span data-stu-id="c42b4-141">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>
   
    ![Navigation pane][9]
7. <span data-ttu-id="c42b4-143">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span><span class="sxs-lookup"><span data-stu-id="c42b4-143">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c42b4-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="c42b4-144">Next steps</span></span>

* <span data-ttu-id="c42b4-145">For an overview of SQL Database auditing, see [Database auditing](sql-database-auditing.md).</span><span class="sxs-lookup"><span data-stu-id="c42b4-145">For an overview of SQL Database auditing, see [Database auditing](sql-database-auditing.md).</span></span>
* <span data-ttu-id="c42b4-146">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c42b4-146">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-threat-detection-get-started/1_td_click_on_settings.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-threat-detection-get-started/2_td_turn_on_auditing.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-threat-detection-get-started/3_td_turn_on_threat_detection.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-threat-detection-get-started/4_td_email.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-threat-detection-get-started/5_td_audit_records.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-threat-detection-get-started/6_td_audit_record_details.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-threat-detection-get-started/9_td_excel_parameters.png










