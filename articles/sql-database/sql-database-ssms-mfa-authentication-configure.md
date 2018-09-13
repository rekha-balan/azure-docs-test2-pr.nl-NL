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
# <a name="configure-azure-sql-database-multi-factor-authentication-for-sql-server-management-studio"></a><span data-ttu-id="4515f-103">Configure Azure SQL Database multi-factor authentication for SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="4515f-103">Configure Azure SQL Database multi-factor authentication for SQL Server Management Studio</span></span>

<span data-ttu-id="4515f-104">This topic shows you how to configure Azure SQL Database multi-factor authentication for SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="4515f-104">This topic shows you how to configure Azure SQL Database multi-factor authentication for SQL Server Management Studio.</span></span> 

<span data-ttu-id="4515f-105">For an overview of Azure SQL Database multi-factor authentication, see [Overview of Azure SQL Database multi-factor authentication for SQL Server Management Studio](sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4515f-105">For an overview of Azure SQL Database multi-factor authentication, see [Overview of Azure SQL Database multi-factor authentication for SQL Server Management Studio](sql-database-ssms-mfa-authentication.md).</span></span>

## <a name="configuration-steps"></a><span data-ttu-id="4515f-106">Configuration steps</span><span class="sxs-lookup"><span data-stu-id="4515f-106">Configuration steps</span></span>

1. <span data-ttu-id="4515f-107">**Configure an Azure Active Directory** - For more information, see [Integrating your on-premises identities with Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Add your own domain name to Azure AD](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure now supports federation with Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Administering your Azure AD directory](https://msdn.microsoft.com/library/azure/hh967611.aspx), and [Manage Azure AD using Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="4515f-107">**Configure an Azure Active Directory** - For more information, see [Integrating your on-premises identities with Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Add your own domain name to Azure AD](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure now supports federation with Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Administering your Azure AD directory](https://msdn.microsoft.com/library/azure/hh967611.aspx), and [Manage Azure AD using Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx).</span></span>
2. <span data-ttu-id="4515f-108">**Configure MFA** - For step-by-step instructions, see [Configuring Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="4515f-108">**Configure MFA** - For step-by-step instructions, see [Configuring Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> 
3. <span data-ttu-id="4515f-109">**Configure SQL Database or SQL Data Warehouse for Azure AD Authentication** - For step-by-step instructions, see [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4515f-109">**Configure SQL Database or SQL Data Warehouse for Azure AD Authentication** - For step-by-step instructions, see [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](sql-database-aad-authentication.md).</span></span>
4. <span data-ttu-id="4515f-110">**Download SSMS** - On the client computer, download the latest SSMS (at least August 2016), from [Download SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="4515f-110">**Download SSMS** - On the client computer, download the latest SSMS (at least August 2016), from [Download SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="connecting-by-using-universal-authentication-with-ssms"></a><span data-ttu-id="4515f-111">Connecting by using universal authentication with SSMS</span><span class="sxs-lookup"><span data-stu-id="4515f-111">Connecting by using universal authentication with SSMS</span></span>

<span data-ttu-id="4515f-112">The following steps show how to connect to SQL Database or SQL Data Warehouse by using the latest SSMS.</span><span class="sxs-lookup"><span data-stu-id="4515f-112">The following steps show how to connect to SQL Database or SQL Data Warehouse by using the latest SSMS.</span></span>

1. <span data-ttu-id="4515f-113">To connect using Universal Authentication, on the **Connect to Server** dialog box, select **Active Directory Universal Authentication**.</span><span class="sxs-lookup"><span data-stu-id="4515f-113">To connect using Universal Authentication, on the **Connect to Server** dialog box, select **Active Directory Universal Authentication**.</span></span>

   ![1mfa-universal-connect][1]
2. <span data-ttu-id="4515f-115">As usual for SQL Database and SQL Data Warehouse you must click **Options** and specify the database on the **Options** dialog box.</span><span class="sxs-lookup"><span data-stu-id="4515f-115">As usual for SQL Database and SQL Data Warehouse you must click **Options** and specify the database on the **Options** dialog box.</span></span> <span data-ttu-id="4515f-116">Then click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="4515f-116">Then click **Connect**.</span></span>
3. <span data-ttu-id="4515f-117">When the **Sign in to your account** dialog box appears, provide the account and password of your Azure Active Directory identity.</span><span class="sxs-lookup"><span data-stu-id="4515f-117">When the **Sign in to your account** dialog box appears, provide the account and password of your Azure Active Directory identity.</span></span>

   ![2mfa-sign-in][2]
   
   > [!NOTE]
   > <span data-ttu-id="4515f-119">For Universal Authentication with an account which does not require MFA, you connect at this point.</span><span class="sxs-lookup"><span data-stu-id="4515f-119">For Universal Authentication with an account which does not require MFA, you connect at this point.</span></span> <span data-ttu-id="4515f-120">For users requiring MFA, continue with the following steps.</span><span class="sxs-lookup"><span data-stu-id="4515f-120">For users requiring MFA, continue with the following steps.</span></span>
   > 
   > 
4. <span data-ttu-id="4515f-121">Two MFA setup dialog boxes might appear.</span><span class="sxs-lookup"><span data-stu-id="4515f-121">Two MFA setup dialog boxes might appear.</span></span> <span data-ttu-id="4515f-122">This one time operation depends on the MFA administrator setting, and therefore may be optional.</span><span class="sxs-lookup"><span data-stu-id="4515f-122">This one time operation depends on the MFA administrator setting, and therefore may be optional.</span></span> <span data-ttu-id="4515f-123">For an MFA enabled domain this step is sometimes pre-defined (for example, the domain requires users to use a smartcard and pin).</span><span class="sxs-lookup"><span data-stu-id="4515f-123">For an MFA enabled domain this step is sometimes pre-defined (for example, the domain requires users to use a smartcard and pin).</span></span>  

   ![3mfa-setup][3]
5. <span data-ttu-id="4515f-125">The second possible one time dialog box allows you to select the details of your authentication method.</span><span class="sxs-lookup"><span data-stu-id="4515f-125">The second possible one time dialog box allows you to select the details of your authentication method.</span></span> <span data-ttu-id="4515f-126">The possible options are configured by your administrator.</span><span class="sxs-lookup"><span data-stu-id="4515f-126">The possible options are configured by your administrator.</span></span>

   ![4mfa-verify-1][4]
6. <span data-ttu-id="4515f-128">The Azure Active Directory sends the confirming information to you.</span><span class="sxs-lookup"><span data-stu-id="4515f-128">The Azure Active Directory sends the confirming information to you.</span></span> <span data-ttu-id="4515f-129">When you receive the verification code, enter it into the **Enter verification code** box, and click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="4515f-129">When you receive the verification code, enter it into the **Enter verification code** box, and click **Sign in**.</span></span>

   ![5mfa-verify-2][5]

<span data-ttu-id="4515f-131">When verification is complete, SSMS connects normally presuming valid credentials and firewall access.</span><span class="sxs-lookup"><span data-stu-id="4515f-131">When verification is complete, SSMS connects normally presuming valid credentials and firewall access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4515f-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="4515f-132">Next steps</span></span>

* <span data-ttu-id="4515f-133">For an overview of Azure SQL Database multi-factor authentication, see [Overview of Azure SQL Database multi-factor authentication for SQL Server Management Studio](sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4515f-133">For an overview of Azure SQL Database multi-factor authentication, see [Overview of Azure SQL Database multi-factor authentication for SQL Server Management Studio](sql-database-ssms-mfa-authentication.md).</span></span>
* <span data-ttu-id="4515f-134">Grant others access to your database: [SQL Database Authentication and Authorization: Granting Access](sql-database-manage-logins.md)</span><span class="sxs-lookup"><span data-stu-id="4515f-134">Grant others access to your database: [SQL Database Authentication and Authorization: Granting Access](sql-database-manage-logins.md)</span></span>  
<span data-ttu-id="4515f-135">Make sure others can connect through the firewall: [Configure an Azure SQL Database server-level firewall rule using the Azure portal](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="4515f-135">Make sure others can connect through the firewall: [Configure an Azure SQL Database server-level firewall rule using the Azure portal](sql-database-configure-firewall-settings.md)</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-mfa-auth/5mfa-verify-2.png






