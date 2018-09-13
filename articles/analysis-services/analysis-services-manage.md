---
title: Manage Azure Analysis Services | Microsoft Docs
description: Learn how to manage an Analysis Services server in Azure.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: fa5eeaad6ec98bb7ce725e1bf4c977cb2d5398a6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800519"
---
# <a name="manage-analysis-services"></a><span data-ttu-id="5722c-103">Manage Analysis Services</span><span class="sxs-lookup"><span data-stu-id="5722c-103">Manage Analysis Services</span></span>
<span data-ttu-id="5722c-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need to perform right away or sometime down the road.</span><span class="sxs-lookup"><span data-stu-id="5722c-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need to perform right away or sometime down the road.</span></span> <span data-ttu-id="5722c-105">For example, run processing to the refresh data, control who can access the models on your server, or monitor your server's health.</span><span class="sxs-lookup"><span data-stu-id="5722c-105">For example, run processing to the refresh data, control who can access the models on your server, or monitor your server's health.</span></span> <span data-ttu-id="5722c-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span><span class="sxs-lookup"><span data-stu-id="5722c-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="5722c-107">Azure portal</span><span class="sxs-lookup"><span data-stu-id="5722c-107">Azure portal</span></span>
<span data-ttu-id="5722c-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access to your servers.</span><span class="sxs-lookup"><span data-stu-id="5722c-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access to your servers.</span></span>  <span data-ttu-id="5722c-109">If you're having some problems, you can also submit a support request.</span><span class="sxs-lookup"><span data-stu-id="5722c-109">If you're having some problems, you can also submit a support request.</span></span>

![Get server name in Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="5722c-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="5722c-111">SQL Server Management Studio</span></span>
<span data-ttu-id="5722c-112">Connecting to your server in Azure is just like connecting to a server instance in your own organization.</span><span class="sxs-lookup"><span data-stu-id="5722c-112">Connecting to your server in Azure is just like connecting to a server instance in your own organization.</span></span> <span data-ttu-id="5722c-113">From SSMS, you can perform many of the same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5722c-113">From SSMS, you can perform many of the same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="5722c-115">Download and install SSMS</span><span class="sxs-lookup"><span data-stu-id="5722c-115">Download and install SSMS</span></span>
<span data-ttu-id="5722c-116">To get all the latest features, and the smoothest experience when connecting to your Azure Analysis Services server, be sure you're using the latest version of SSMS.</span><span class="sxs-lookup"><span data-stu-id="5722c-116">To get all the latest features, and the smoothest experience when connecting to your Azure Analysis Services server, be sure you're using the latest version of SSMS.</span></span> 

<span data-ttu-id="5722c-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="5722c-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="to-connect-with-ssms"></a><span data-ttu-id="5722c-118">To connect with SSMS</span><span class="sxs-lookup"><span data-stu-id="5722c-118">To connect with SSMS</span></span>
 <span data-ttu-id="5722c-119">When using SSMS, before connecting to your server the first time, make sure your username is included in the Analysis Services Admins group.</span><span class="sxs-lookup"><span data-stu-id="5722c-119">When using SSMS, before connecting to your server the first time, make sure your username is included in the Analysis Services Admins group.</span></span> <span data-ttu-id="5722c-120">To learn more, see [Server administrators](#server-administrators) later in this article.</span><span class="sxs-lookup"><span data-stu-id="5722c-120">To learn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="5722c-121">Before you connect, you need to get the server name.</span><span class="sxs-lookup"><span data-stu-id="5722c-121">Before you connect, you need to get the server name.</span></span> <span data-ttu-id="5722c-122">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span><span class="sxs-lookup"><span data-stu-id="5722c-122">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Get server name in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="5722c-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="5722c-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="5722c-125">In the **Connect to Server** dialog box, paste in the server name, then in **Authentication**, choose one of the following authentication types:</span><span class="sxs-lookup"><span data-stu-id="5722c-125">In the **Connect to Server** dialog box, paste in the server name, then in **Authentication**, choose one of the following authentication types:</span></span>   
    > [!NOTE]
    > <span data-ttu-id="5722c-126">Authentication type, **Active Directory - Universal with MFA support**, is recommended.</span><span class="sxs-lookup"><span data-stu-id="5722c-126">Authentication type, **Active Directory - Universal with MFA support**, is recommended.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5722c-127">If you sign in with a Microsoft Account, Live ID, Yanoo, Gmail, etc., leave the password field blank.</span><span class="sxs-lookup"><span data-stu-id="5722c-127">If you sign in with a Microsoft Account, Live ID, Yanoo, Gmail, etc., leave the password field blank.</span></span> <span data-ttu-id="5722c-128">You are prompted for a password after clicking Connect.</span><span class="sxs-lookup"><span data-stu-id="5722c-128">You are prompted for a password after clicking Connect.</span></span>

    <span data-ttu-id="5722c-129">**Windows Authentication** to use your Windows domain\username and password credentials.</span><span class="sxs-lookup"><span data-stu-id="5722c-129">**Windows Authentication** to use your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="5722c-130">**Active Directory Password Authentication** to use an organizational account.</span><span class="sxs-lookup"><span data-stu-id="5722c-130">**Active Directory Password Authentication** to use an organizational account.</span></span> <span data-ttu-id="5722c-131">For example, when connecting from a non-domain joined computer.</span><span class="sxs-lookup"><span data-stu-id="5722c-131">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="5722c-132">**Active Directory - Universal with MFA support** to use [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5722c-132">**Active Directory - Universal with MFA support** to use [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Connect in SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="5722c-134">Server administrators and database users</span><span class="sxs-lookup"><span data-stu-id="5722c-134">Server administrators and database users</span></span>
<span data-ttu-id="5722c-135">In Azure Analysis Services, there are two types of users, server administrators and database users.</span><span class="sxs-lookup"><span data-stu-id="5722c-135">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="5722c-136">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span><span class="sxs-lookup"><span data-stu-id="5722c-136">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="5722c-137">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="5722c-137">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="5722c-138">Troubleshooting connection problems</span><span class="sxs-lookup"><span data-stu-id="5722c-138">Troubleshooting connection problems</span></span>
<span data-ttu-id="5722c-139">When connecting using SSMS, if you run into problems, you may need to clear the login cache.</span><span class="sxs-lookup"><span data-stu-id="5722c-139">When connecting using SSMS, if you run into problems, you may need to clear the login cache.</span></span> <span data-ttu-id="5722c-140">Nothing is cached to disc. To clear the cache, close and restart the connect process.</span><span class="sxs-lookup"><span data-stu-id="5722c-140">Nothing is cached to disc. To clear the cache, close and restart the connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5722c-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="5722c-141">Next steps</span></span>
<span data-ttu-id="5722c-142">If you haven't already deployed a tabular model to your new server, now is a good time.</span><span class="sxs-lookup"><span data-stu-id="5722c-142">If you haven't already deployed a tabular model to your new server, now is a good time.</span></span> <span data-ttu-id="5722c-143">To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5722c-143">To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="5722c-144">If you've deployed a model to your server, you're ready to connect to it using a client or browser.</span><span class="sxs-lookup"><span data-stu-id="5722c-144">If you've deployed a model to your server, you're ready to connect to it using a client or browser.</span></span> <span data-ttu-id="5722c-145">To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="5722c-145">To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

