---
title: Azure Data Catalog release notes | Microsoft Docs
description: Release notes for Azure Data Catalog.
services: data-catalog
documentationcenter: ''
author: steelanddata
manager: NA
editor: ''
tags: ''
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 01/23/2017
ms.author: maroche
ms.openlocfilehash: 91fc507024b13cf95b61c471bd098b4b9ab4a428
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550868"
---
# <a name="azure-data-catalog-release-notes"></a>Azure Data Catalog release notes
## <a name="notes-for-the-november-20-2015-release-of-azure-data-catalog"></a>Notes for the November 20, 2015 release of Azure Data Catalog
### <a name="opening-data-sources-in-power-bi-desktop"></a>Opening Data Sources in Power BI Desktop
When using the "Open in Power BI Desktop" option from the **Azure Data Catalog** portal, users may encounter one of two problems in the Power BI Desktop application:

* A dialog box with the title "Unable to Open Document" is displayed
* The Power BI Desktop application opens, but the file appears to be empty

For each situation, the problem can be resolved by downloading and installing the latest version of Power BI Desktop from [PowerBI.com](https://powerbi.com).

## <a name="notes-for-the-november-13-2015-release-of-azure-data-catalog"></a>Notes for the November 13, 2015 release of Azure Data Catalog
### <a name="registering-and-connecting-to-teradata"></a>Registering and connecting to Teradata
When connecting to Teradata data sources users must have installed the correct Teradata ODBC driver that match the bitness (32-bit or 64-bit) of the software being used.

As of this ADC release date, the most recent [Teradata ODBC driver for windows ( version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatible with Office 2013, but not with Office 2016.

## <a name="notes-for-the-july-13-2015-release-of-azure-data-catalog"></a>Notes for the July 13, 2015 release of Azure Data Catalog
### <a name="registering-and-connecting-to-oracle-database"></a>Registering and connecting to Oracle Database
When connecting to Oracle Database data sources users must have installed the correct Oracle drivers that match the bitness (32-bit or 64-bit) of the software being used.

* When registering Oracle data sources on a computer running 32-bit Windows, the 32-bit Oracle drivers will be used
* When registering Oracle data sources on a computer running 64-bit Windows, the 64-bit Oracle drivers will be used
* When connecting to Oracle data sources using Excel on a computer running the 32-bit version of Microsoft Office, including on 64-bit Windows, the 32-bit Oracle drivers will be used
* When connecting to Oracle data sources using Excel on a computer running the 64-bit version of Microsoft Office, the 64-bit Oracle drivers will be used

### <a name="registering-and-connecting-to-sql-server-reporting-services"></a>Registering and connecting to SQL Server Reporting Services
Support for SQL Server Reporting Services (SSRS) data sources is currently limited to Native Mode servers only. Support for SSRS in SharePoint mode will be added in a later release.

### <a name="opening-data-assets-in-excel"></a>Opening data assets in Excel
When opening data assets in Microsoft Excel from the **Azure Data Catalog** portal, users may be prompted with a **Microsoft Excel Security Notice** dialog box. This is standard, expected behavior, and users can select **Enable** to continue.

For more information, see [Enable or disable security alerts about links and files from suspicious websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a>Proxy and policy configuration and data source registration
Users may encounter a situation where they can log on to the Azure Data Catalog portal, but when they attempt to log on to the data source registration tool they encounter an error message that prevents them from logging on.

There are two potential causes for this problem behavior:

**Cause 1: Active Directory Federation Services configuration** The data source registration tool uses Forms Authentication to validate user logons against Active Directory. For successful logon, Forms Authentication must be enabled in the Global Authentication Policy by an Active Directory administrator.

In some situations, this error behavior may occur only when the user is on the company network, or only when the user is connecting from outside the company network. The Global Authentication Policy allows authentication methods to be enabled separately for intranet and extranet connections. Logon errors may occur if Forms Authentication is not enabled for the network from which the user is connecting.

For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).

**Cause 2: Network proxy configuration** If the corporate network uses a proxy server, the registration tool may not be able to connect to Azure Active Directory through the proxy. Users can ensure that the registration tool by editing the tool’s configuration file, adding this section to the file:

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


To locate the RegistrationTool.exe.config file, launch the registration tool, and then open the Windows Task Manager utility. On the Details tab in Task manager, right-click on RegistrationTool.exe and choose Open file location from the pop-up menu.