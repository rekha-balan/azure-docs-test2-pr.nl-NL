---
title: Manage Azure Analysis Services | Microsoft Docs
description: Learn how to manage an Analysis Services server in Azure.
services: analysis-services
documentationcenter: ''
author: minewiskan
manager: erikre
editor: ''
tags: ''
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 04/18/2017
ms.author: owend
ms.openlocfilehash: cb47305485686a6c456d70dcc3b1cb9109875925
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555603"
---
# <a name="manage-analysis-services"></a>Manage Analysis Services
Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need to perform right away or sometime down the road. For example, run processing to the refresh data, control who can access the models on your server, or monitor your server's health. Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.

## <a name="azure-portal"></a>Azure portal
The [Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access to your servers.  If you're having some problems, you can also submit a support request.

![Get server name in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a>SQL Server Management Studio
Connecting to your server in Azure is just like connecting to a server instance in your own organization. From SSMS, you can perform many of the same tasks such as process data or create a processing script, manage roles, and use PowerShell.
  
![SQL Server Management Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a>Download and install SSMS
To get all the latest features, and the smoothest experience when connecting to your Azure Analysis Services server, be sure you're using the latest version of SSMS. 

[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


### <a name="to-connect-with-ssms"></a>To connect with SSMS
 When using SSMS, before connecting to your server the first time, make sure your username is included in the Analysis Services Admins group. To learn more, see [Server administrators](#server-administrators) later in this article.

1. Before you connect, you need to get the server name. In **Azure portal** > server > **Overview** > **Server name**, copy the server name.
   
    ![Get server name in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.
3. In the **Connect to Server** dialog box, paste in the server name, then in **Authentication**, choose one of the following:
   
    **Windows Authentication** to use your Windows domain\username and password credentials.

    **Active Directory Password Authentication** to use an organizational account. For example, when connecting from a non-domain joined computer.

    **Active Directory Universal Authentication** to use [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md). 
   
    ![Connect in SSMS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a>Server administrators and database users
In Azure Analysis Services, there are two types of users, server administrators and database users. Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN. This is different from on-premises tabular model databases, which support server administrators and database users by Windows domain usernames. To learn more, see [Manage users in Azure Analysis Services](analysis-services-manage-users.md).


## <a name="troubleshooting-connection-problems"></a>Troubleshooting connection problems
When connecting using SSMS, if you run into problems, you may need to clear the login cache. Nothing is cached to disc. To clear the cache, close and restart the connect process. 

## <a name="next-steps"></a>Next steps
If you haven't already deployed a tabular model to your new server, now is a good time. To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).

If you've deployed a model to your server, you're ready to connect to it using a client or browser. To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).





