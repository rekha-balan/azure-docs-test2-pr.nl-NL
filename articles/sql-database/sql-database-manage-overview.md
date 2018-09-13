---
title: Tools to manage & develop with Azure SQL Database | Microsoft Docs
description: Introduces the management and development tools and options for Azure SQL Database
services: sql-database
documentationcenter: ''
author: CarlRabeler
manager: jhubbard
editor: ''
ms.assetid: 37767380-975f-4dee-a28d-80bc2036dda3
ms.service: sql-database
ms.custom: manage
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: carlrab
ms.openlocfilehash: 596455f582acdec127e4e9a85b51692b5ec11d78
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551318"
---
# <a name="overview-tools-to-manage--develop-with-azure-sql-database"></a><span data-ttu-id="407f0-103">Overview: Tools to manage & develop with Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="407f0-103">Overview: Tools to manage & develop with Azure SQL Database</span></span>
<span data-ttu-id="407f0-104">This topic introduces the tools for managing and developing with Azure SQL databases.</span><span class="sxs-lookup"><span data-stu-id="407f0-104">This topic introduces the tools for managing and developing with Azure SQL databases.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="407f0-105">This documentation set includes QuickStarts, Sample, and How-to guides showing you how to management and develop with Azure SQL Database using the tools introduced in the following paragraphs.</span><span class="sxs-lookup"><span data-stu-id="407f0-105">This documentation set includes QuickStarts, Sample, and How-to guides showing you how to management and develop with Azure SQL Database using the tools introduced in the following paragraphs.</span></span> <span data-ttu-id="407f0-106">Use the left-hand navigation pane and filter box to find specific content for the Azure portal, PowerShell, and T-SQL.</span><span class="sxs-lookup"><span data-stu-id="407f0-106">Use the left-hand navigation pane and filter box to find specific content for the Azure portal, PowerShell, and T-SQL.</span></span>
>

## <a name="azure-portal"></a><span data-ttu-id="407f0-107">Azure portal</span><span class="sxs-lookup"><span data-stu-id="407f0-107">Azure portal</span></span>
<span data-ttu-id="407f0-108">The [Azure portal](https://portal.azure.com) is a web-based application where you can create, update, and delete databases and logical servers and monitor database activity.</span><span class="sxs-lookup"><span data-stu-id="407f0-108">The [Azure portal](https://portal.azure.com) is a web-based application where you can create, update, and delete databases and logical servers and monitor database activity.</span></span> <span data-ttu-id="407f0-109">This tool is great if you're just getting started with Azure, managing a few databases, or need to do something quickly.</span><span class="sxs-lookup"><span data-stu-id="407f0-109">This tool is great if you're just getting started with Azure, managing a few databases, or need to do something quickly.</span></span>

## <a name="sql-server-management-studio-and-transact-sql"></a><span data-ttu-id="407f0-110">SQL Server Management Studio and Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="407f0-110">SQL Server Management Studio and Transact-SQL</span></span>
<span data-ttu-id="407f0-111">SQL Server Management Studio (SSMS) is a client tool that runs on your computer for managing your database in the cloud using Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="407f0-111">SQL Server Management Studio (SSMS) is a client tool that runs on your computer for managing your database in the cloud using Transact-SQL.</span></span> <span data-ttu-id="407f0-112">Many database administrators are familiar with SSMS, which can be used with Azure SQL databases.</span><span class="sxs-lookup"><span data-stu-id="407f0-112">Many database administrators are familiar with SSMS, which can be used with Azure SQL databases.</span></span> <span data-ttu-id="407f0-113">[Download the latest version of SSMS](https://msdn.microsoft.com/library/mt238290) and always use the latest release when working with Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="407f0-113">[Download the latest version of SSMS](https://msdn.microsoft.com/library/mt238290) and always use the latest release when working with Azure SQL Database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="407f0-114">Always use the latest version of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290).</span><span class="sxs-lookup"><span data-stu-id="407f0-114">Always use the latest version of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290).</span></span>
>  

## <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="407f0-115">SQL Server Data Tools in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="407f0-115">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="407f0-116">SQL Server Data Tools (SSDT) is a client tool that runs on your computer for developing your database in the cloud.</span><span class="sxs-lookup"><span data-stu-id="407f0-116">SQL Server Data Tools (SSDT) is a client tool that runs on your computer for developing your database in the cloud.</span></span> <span data-ttu-id="407f0-117">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), [try using SSDT in Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx).</span><span class="sxs-lookup"><span data-stu-id="407f0-117">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), [try using SSDT in Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="407f0-118">Always use the latest version of [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) to remain synchronized with updates to Microsoft Azure and SQL Database.</span><span class="sxs-lookup"><span data-stu-id="407f0-118">Always use the latest version of [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span>
>  
## <a name="powershell"></a><span data-ttu-id="407f0-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="407f0-119">PowerShell</span></span>
<span data-ttu-id="407f0-120">You can use PowerShell to manage databases and elastic pools, and to automate Azure resource deployments.</span><span class="sxs-lookup"><span data-stu-id="407f0-120">You can use PowerShell to manage databases and elastic pools, and to automate Azure resource deployments.</span></span> <span data-ttu-id="407f0-121">Microsoft recommends this tool for managing a large number of databases and automating deployment and resource changes in a production environment.</span><span class="sxs-lookup"><span data-stu-id="407f0-121">Microsoft recommends this tool for managing a large number of databases and automating deployment and resource changes in a production environment.</span></span>

## <a name="elastic-database-tools"></a><span data-ttu-id="407f0-122">Elastic Database tools</span><span class="sxs-lookup"><span data-stu-id="407f0-122">Elastic Database tools</span></span>
<span data-ttu-id="407f0-123">Use the elastic database tools to perform actions such as</span><span class="sxs-lookup"><span data-stu-id="407f0-123">Use the elastic database tools to perform actions such as</span></span> 

* <span data-ttu-id="407f0-124">Executing a T-SQL script against a set of databases using an [elastic job](sql-database-elastic-jobs-overview.md)</span><span class="sxs-lookup"><span data-stu-id="407f0-124">Executing a T-SQL script against a set of databases using an [elastic job](sql-database-elastic-jobs-overview.md)</span></span>
* <span data-ttu-id="407f0-125">Moving multi-tenant model databases to a single-tenant model with the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="407f0-125">Moving multi-tenant model databases to a single-tenant model with the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>
* <span data-ttu-id="407f0-126">Managing databases in a single-tenant model or a multi-tenant model using the [elastic scale client library](sql-database-elastic-database-client-library.md).</span><span class="sxs-lookup"><span data-stu-id="407f0-126">Managing databases in a single-tenant model or a multi-tenant model using the [elastic scale client library](sql-database-elastic-database-client-library.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="407f0-127">Additional resources</span><span class="sxs-lookup"><span data-stu-id="407f0-127">Additional resources</span></span>
* [<span data-ttu-id="407f0-128">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="407f0-128">Azure Resource Manager</span></span>](https://azure.microsoft.com/features/resource-manager/)
* [<span data-ttu-id="407f0-129">Azure Automation</span><span class="sxs-lookup"><span data-stu-id="407f0-129">Azure Automation</span></span>](https://azure.microsoft.com/documentation/services/automation/)
* [<span data-ttu-id="407f0-130">Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="407f0-130">Azure Scheduler</span></span>](https://azure.microsoft.com/documentation/services/scheduler/)

