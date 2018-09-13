---
title: Configure multi-factor authentication - Azure SQL | Microsoft Docs
description: Use Multi-Factored Authentication with SSMS for SQL Database and SQL Data Warehouse.
services: sql-database
documentationcenter: ''
author: BYHAM
manager: jhubbard
editor: ''
tags: ''
ms.assetid: ''
ms.service: sql-database
ms.custom: security-access
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/23/2017
ms.author: rickbyh
ms.openlocfilehash: a61f30416668ca2356b09eadc063c00dc0dc0aa3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663066"
---
# <a name="configure-azure-sql-database-multi-factor-authentication-for-sql-server-management-studio"></a>Configure Azure SQL Database multi-factor authentication for SQL Server Management Studio

This topic shows you how to configure Azure SQL Database multi-factor authentication for SQL Server Management Studio. 

For an overview of Azure SQL Database multi-factor authentication, see [Overview of Azure SQL Database multi-factor authentication for SQL Server Management Studio](sql-database-ssms-mfa-authentication.md).

## <a name="configuration-steps"></a>Configuration steps

1. **Configure an Azure Active Directory** - For more information, see [Integrating your on-premises identities with Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Add your own domain name to Azure AD](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure now supports federation with Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Administering your Azure AD directory](https://msdn.microsoft.com/library/azure/hh967611.aspx), and [Manage Azure AD using Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx).
2. **Configure MFA** - For step-by-step instructions, see [Configuring Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-whats-next.md). 
3. **Configure SQL Database or SQL Data Warehouse for Azure AD Authentication** - For step-by-step instructions, see [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](sql-database-aad-authentication.md).
4. **Download SSMS** - On the client computer, download the latest SSMS (at least August 2016), from [Download SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).

## <a name="connecting-by-using-universal-authentication-with-ssms"></a>Connecting by using universal authentication with SSMS

The following steps show how to connect to SQL Database or SQL Data Warehouse by using the latest SSMS.

1. To connect using Universal Authentication, on the **Connect to Server** dialog box, select **Active Directory Universal Authentication**.

   ![1mfa-universal-connect][1]
2. As usual for SQL Database and SQL Data Warehouse you must click **Options** and specify the database on the **Options** dialog box. Then click **Connect**.
3. When the **Sign in to your account** dialog box appears, provide the account and password of your Azure Active Directory identity.

   ![2mfa-sign-in][2]
   
   > [!NOTE]
   > For Universal Authentication with an account which does not require MFA, you connect at this point. For users requiring MFA, continue with the following steps.
   > 
   > 
4. Two MFA setup dialog boxes might appear. This one time operation depends on the MFA administrator setting, and therefore may be optional. For an MFA enabled domain this step is sometimes pre-defined (for example, the domain requires users to use a smartcard and pin).  

   ![3mfa-setup][3]
5. The second possible one time dialog box allows you to select the details of your authentication method. The possible options are configured by your administrator.

   ![4mfa-verify-1][4]
6. The Azure Active Directory sends the confirming information to you. When you receive the verification code, enter it into the **Enter verification code** box, and click **Sign in**.

   ![5mfa-verify-2][5]

When verification is complete, SSMS connects normally presuming valid credentials and firewall access.

## <a name="next-steps"></a>Next steps

* For an overview of Azure SQL Database multi-factor authentication, see [Overview of Azure SQL Database multi-factor authentication for SQL Server Management Studio](sql-database-ssms-mfa-authentication.md).
* Grant others access to your database: [SQL Database Authentication and Authorization: Granting Access](sql-database-manage-logins.md)  
Make sure others can connect through the firewall: [Configure an Azure SQL Database server-level firewall rule using the Azure portal](sql-database-configure-firewall-settings.md)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-mfa-auth/5mfa-verify-2.png






