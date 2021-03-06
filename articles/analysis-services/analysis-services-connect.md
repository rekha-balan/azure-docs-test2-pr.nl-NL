---
title: Connect to Azure Analysis Services | Microsoft Docs
description: Learn how to connect to and get data from an Analysis Services server in Azure.
services: analysis-services
documentationcenter: ''
author: minewiskan
manager: erikre
editor: ''
tags: ''
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 04/17/2017
ms.author: owend
ms.openlocfilehash: a9edd5068d2f1d5936c52012a25e76d75d631142
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564048"
---
# <a name="connect-to-an-azure-analysis-services-server"></a>Connect to an Azure Analysis Services server

This article describes connecting to a server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT). Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications. Connections to Azure Analysis Services use HTTPS.

## <a name="client-libraries"></a>Client libraries
[Get the latest Client libraries](analysis-services-data-providers.md)

All connections to a server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries to connect to and interface with an Analysis Services server. For SSMS, SSDT, Excel 2016, and Power BI, the latest client libraries are installed or updated with monthly releases. However, in some cases, it's possible an application may not have the latest. For example, when policies delay updates, or Office 365 updates are on the Deferred Channel.

## <a name="server-name"></a>Server name

When you create an Analysis Services server in Azure, you specify a unique name and the region where the server is to be created. When specifying the server name in a connection, the server naming scheme is:

```
<protocol>://<region>/<servername>
```
 Where protocol is string **asazure**, region is the Uri where the server was created (for example, westus.asazure.windows.net) and servername is the name of your unique server within the region.

### <a name="get-the-server-name"></a>Get the server name
In **Azure portal** > server > **Overview** > **Server name**, copy the entire server name. If other users in your organization are connecting to this server too, you can share this server name with them. When specifying a server name, the entire path must be used.

![Get server name in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a>Connection string

When connecting to Azure Analysis Services using the Tabular Object Model, use the following connection string formats:

###### <a name="integrated-azure-active-directory-authentication"></a>Integrated Azure Active Directory authentication
Integrated authentication picks up the Azure Active Directory credential cache if available. If not, the Azure login window is shown.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a>Azure Active Directory authentication with username and password

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a>Windows authentication (Integrated security)
Use the Windows account running the current process.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a>Connect using an .odc file
With older versions of Excel, users can connect to an Azure Analysis Services server by using an Office Data Connection (.odc) file. To learn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).


## <a name="next-steps"></a>Next steps
[Connect with Excel](analysis-services-connect-excel.md)    
[Connect with Power BI](analysis-services-connect-pbi.md)   
[Manage your server](analysis-services-manage.md)   


