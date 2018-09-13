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
# <a name="manage-analysis-services"></a><span data-ttu-id="b2af4-103">Manage Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b2af4-103">Manage Analysis Services</span></span>
<span data-ttu-id="b2af4-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need to perform right away or sometime down the road.</span><span class="sxs-lookup"><span data-stu-id="b2af4-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need to perform right away or sometime down the road.</span></span> <span data-ttu-id="b2af4-105">For example, run processing to the refresh data, control who can access the models on your server, or monitor your server's health.</span><span class="sxs-lookup"><span data-stu-id="b2af4-105">For example, run processing to the refresh data, control who can access the models on your server, or monitor your server's health.</span></span> <span data-ttu-id="b2af4-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span><span class="sxs-lookup"><span data-stu-id="b2af4-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="b2af4-107">Azure portal</span><span class="sxs-lookup"><span data-stu-id="b2af4-107">Azure portal</span></span>
<span data-ttu-id="b2af4-108">The [Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access to your servers.</span><span class="sxs-lookup"><span data-stu-id="b2af4-108">The [Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access to your servers.</span></span>  <span data-ttu-id="b2af4-109">If you're having some problems, you can also submit a support request.</span><span class="sxs-lookup"><span data-stu-id="b2af4-109">If you're having some problems, you can also submit a support request.</span></span>

![Get server name in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="b2af4-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="b2af4-111">SQL Server Management Studio</span></span>
<span data-ttu-id="b2af4-112">Connecting to your server in Azure is just like connecting to a server instance in your own organization.</span><span class="sxs-lookup"><span data-stu-id="b2af4-112">Connecting to your server in Azure is just like connecting to a server instance in your own organization.</span></span> <span data-ttu-id="b2af4-113">From SSMS, you can perform many of the same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2af4-113">From SSMS, you can perform many of the same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="b2af4-115">Download and install SSMS</span><span class="sxs-lookup"><span data-stu-id="b2af4-115">Download and install SSMS</span></span>
<span data-ttu-id="b2af4-116">To get all the latest features, and the smoothest experience when connecting to your Azure Analysis Services server, be sure you're using the latest version of SSMS.</span><span class="sxs-lookup"><span data-stu-id="b2af4-116">To get all the latest features, and the smoothest experience when connecting to your Azure Analysis Services server, be sure you're using the latest version of SSMS.</span></span> 

<span data-ttu-id="b2af4-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="b2af4-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="to-connect-with-ssms"></a><span data-ttu-id="b2af4-118">To connect with SSMS</span><span class="sxs-lookup"><span data-stu-id="b2af4-118">To connect with SSMS</span></span>
 <span data-ttu-id="b2af4-119">When using SSMS, before connecting to your server the first time, make sure your username is included in the Analysis Services Admins group.</span><span class="sxs-lookup"><span data-stu-id="b2af4-119">When using SSMS, before connecting to your server the first time, make sure your username is included in the Analysis Services Admins group.</span></span> <span data-ttu-id="b2af4-120">To learn more, see [Server administrators](#server-administrators) later in this article.</span><span class="sxs-lookup"><span data-stu-id="b2af4-120">To learn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="b2af4-121">Before you connect, you need to get the server name.</span><span class="sxs-lookup"><span data-stu-id="b2af4-121">Before you connect, you need to get the server name.</span></span> <span data-ttu-id="b2af4-122">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span><span class="sxs-lookup"><span data-stu-id="b2af4-122">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Get server name in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="b2af4-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="b2af4-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="b2af4-125">In the **Connect to Server** dialog box, paste in the server name, then in **Authentication**, choose one of the following:</span><span class="sxs-lookup"><span data-stu-id="b2af4-125">In the **Connect to Server** dialog box, paste in the server name, then in **Authentication**, choose one of the following:</span></span>
   
    <span data-ttu-id="b2af4-126">**Windows Authentication** to use your Windows domain\username and password credentials.</span><span class="sxs-lookup"><span data-stu-id="b2af4-126">**Windows Authentication** to use your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="b2af4-127">**Active Directory Password Authentication** to use an organizational account.</span><span class="sxs-lookup"><span data-stu-id="b2af4-127">**Active Directory Password Authentication** to use an organizational account.</span></span> <span data-ttu-id="b2af4-128">For example, when connecting from a non-domain joined computer.</span><span class="sxs-lookup"><span data-stu-id="b2af4-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="b2af4-129">**Active Directory Universal Authentication** to use [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b2af4-129">**Active Directory Universal Authentication** to use [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Connect in SSMS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="b2af4-131">Server administrators and database users</span><span class="sxs-lookup"><span data-stu-id="b2af4-131">Server administrators and database users</span></span>
<span data-ttu-id="b2af4-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span><span class="sxs-lookup"><span data-stu-id="b2af4-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="b2af4-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span><span class="sxs-lookup"><span data-stu-id="b2af4-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="b2af4-134">This is different from on-premises tabular model databases, which support server administrators and database users by Windows domain usernames.</span><span class="sxs-lookup"><span data-stu-id="b2af4-134">This is different from on-premises tabular model databases, which support server administrators and database users by Windows domain usernames.</span></span> <span data-ttu-id="b2af4-135">To learn more, see [Manage users in Azure Analysis Services](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="b2af4-135">To learn more, see [Manage users in Azure Analysis Services](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="b2af4-136">Troubleshooting connection problems</span><span class="sxs-lookup"><span data-stu-id="b2af4-136">Troubleshooting connection problems</span></span>
<span data-ttu-id="b2af4-137">When connecting using SSMS, if you run into problems, you may need to clear the login cache.</span><span class="sxs-lookup"><span data-stu-id="b2af4-137">When connecting using SSMS, if you run into problems, you may need to clear the login cache.</span></span> <span data-ttu-id="b2af4-138">Nothing is cached to disc. To clear the cache, close and restart the connect process.</span><span class="sxs-lookup"><span data-stu-id="b2af4-138">Nothing is cached to disc. To clear the cache, close and restart the connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b2af4-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="b2af4-139">Next steps</span></span>
<span data-ttu-id="b2af4-140">If you haven't already deployed a tabular model to your new server, now is a good time.</span><span class="sxs-lookup"><span data-stu-id="b2af4-140">If you haven't already deployed a tabular model to your new server, now is a good time.</span></span> <span data-ttu-id="b2af4-141">To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b2af4-141">To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="b2af4-142">If you've deployed a model to your server, you're ready to connect to it using a client or browser.</span><span class="sxs-lookup"><span data-stu-id="b2af4-142">If you've deployed a model to your server, you're ready to connect to it using a client or browser.</span></span> <span data-ttu-id="b2af4-143">To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b2af4-143">To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>





