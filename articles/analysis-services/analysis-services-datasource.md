---
title: Datasource connections | Microsoft Docs
description: Describes data source connections for data models in Azure Analysis Services.
services: analysis-services
documentationcenter: ''
author: minewiskan
manager: erikre
editor: ''
tags: ''
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 04/14/2017
ms.author: owend
ms.openlocfilehash: b396e2bbaa075a735bb474b428a91a5dfe3a341a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662687"
---
# <a name="datasource-connections"></a>Datasource connections
Data models in Azure Analysis Services may require different data providers when connecting to certain data sources. In some cases, tabular models connecting to data sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error.

For example; if you have an in-memory or Direct Query data model that connects to a cloud data source such as Azure SQL Database, if you use native providers other than SQLOLEDB, you may see error message: **“The provider 'SQLNCLI11.1' is not registered”**.

Or, if you have a DirectQuery model connecting to on-premises data sources, if you use native providers you may see error message: **“Error creating OLE DB row set. Incorrect syntax near 'LIMIT'”**.

## <a name="data-source-providers"></a>Data source providers
The following datasource providers are supported for in-memory or Direct Query data models when connecting to data sources in the cloud or on-premises:

### <a name="cloud"></a>Cloud
| **Datasource** | **In-memory** | **Direct Query** |
|  --- | --- | --- |
| Azure SQL Data Warehouse |.NET Framework Data Provider for SQL Server |.NET Framework Data Provider for SQL Server |
| Azure SQL Database |.NET Framework Data Provider for SQL Server |.NET Framework Data Provider for SQL Server | |

### <a name="on-premises-via-gateway"></a>On-premises (via Gateway)
|**Datasource** | **In-memory** | **Direct Query** |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0 |.NET Framework Data Provider for SQL Server |
| SQL Server |Microsoft OLE DB Provider for SQL Server |.NET Framework Data Provider for SQL Server | |
| SQL Server |.NET Framework Data Provider for SQL Server |.NET Framework Data Provider for SQL Server | |
| Oracle |Microsoft OLE DB Provider for Oracle |Oracle Data Provider for .NET | |
| Oracle |Oracle Data Provider for .NET |Oracle Data Provider for .NET | |
| Teradata |OLE DB Provider for Teradata |Teradata Data Provider for .NET | |
| Teradata |Teradata Data Provider for .NET |Teradata Data Provider for .NET | |
| Analytics Platform System |.NET Framework Data Provider for SQL Server |.NET Framework Data Provider for SQL Server | |

> [!NOTE]
> Ensure 64-bit providers are installed when using On-premises gateway.
> 
> 

When migrating an on-premises SQL Server Analysis Services tabular model to Azure Analysis Services, it may be necessary to change the provider.

**To specify a datasource provider**

1. In SSDT > **Tabular Model Explorer** > **Data Sources**, right-click a data source connection, and then click **Edit Data Source**.
2. In **Edit Connection**, click **Advanced** to open the Advance properties window.
3. In **Set Advanced Properties** > **Providers**, then select the appropriate provider.

## <a name="impersonation"></a>Impersonation
In some cases, it may be necessary to specify a different impersonation account. Impersonation account can be specified in SSDT or SSMS.

For on-premises data sources:

* If using SQL authentication, impersonation should be Service Account.
* If using Windows authentication, set Windows user/password. For SQL Server, Windows authentication with a specific impersonation account is supported only for in-memory data models.

For cloud data sources:

* If using SQL authentication, impersonation should be Service Account.

## <a name="next-steps"></a>Next steps
If you have on-premises data sources, be sure to install the [On-premises gateway](analysis-services-gateway.md). To learn more about managing your server in SSDT or SSMS, see [Manage your server](analysis-services-manage.md).

