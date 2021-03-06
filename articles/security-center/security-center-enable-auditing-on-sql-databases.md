---
title: Enable auditing and threat detection on SQL databases in Azure Security Center | Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendation **Enable auditing and threat detection on SQL databases**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: ae15ba3c64492c1459d759834c8c4c2ee5dfe34a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564489"
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a>Enable auditing and threat detection on SQL databases in Azure Security Center
Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled. Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.

Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts. Threat Detection detects anomalous database activities indicating potential security threats to the database. This enables you to detect and respond to potential threats as they occur.

This recommendation applies to the Azure SQL service only; it doesn't include SQL running on your virtual machines.

> [!NOTE]
> This document introduces the service by using an example deployment.  This is not a step-by-step guide.
>
>

## <a name="implement-the-recommendation"></a>Implement the recommendation
1. In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.  This opens the **Enable Auditing & Threat detection on SQL databases** blade.

   ![Enable auditing on SQL databases][1]
2. Select a SQL database to enable auditing on. This opens the **Auditing & Threat Detection** blade.

3. On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.

   ![Turn on auditing and threat detection][2]
4. Follow the steps in [SQL Database Threat Detection in the Azure portal](../sql-database/sql-database-threat-detection-portal.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.

## <a name="see-also"></a>See also
This article showed you how to implement the Security Center recommendation "Enable Auditing & Threat detection on SQL databases." To learn more about securing your SQL database, see the following:

* [Securing your SQL Database](../sql-database/sql-database-security-overview.md)

To learn more about Security Center, see the following:

* [Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.
* [Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.
* [Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.
* [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.
* [Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.
* [Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png


