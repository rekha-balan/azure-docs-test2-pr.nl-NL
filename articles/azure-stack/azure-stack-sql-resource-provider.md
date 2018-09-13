---
title: Using SQL databases on Azure Stack | Microsoft Docs
description: Learn how you can deploy SQL databases as a service on Azure Stack and the quick steps to deploy the SQL Server resource provider adapter.
services: azure-stack
documentationCenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2018
ms.author: jeffgilb
ms.reviewer: jeffgo
ms.openlocfilehash: 55d0e51606e8768a01c0b5a7766dbafe24d97a0d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866662"
---
# <a name="use-sql-databases-on-microsoft-azure-stack"></a><span data-ttu-id="b8f6f-103">Use SQL databases on Microsoft Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b8f6f-103">Use SQL databases on Microsoft Azure Stack</span></span>

<span data-ttu-id="b8f6f-104">Use the SQL Server resource provider adapter API to expose SQL databases as a service of [Azure Stack](azure-stack-poc.md).</span><span class="sxs-lookup"><span data-stu-id="b8f6f-104">Use the SQL Server resource provider adapter API to expose SQL databases as a service of [Azure Stack](azure-stack-poc.md).</span></span> <span data-ttu-id="b8f6f-105">After you install the resource provider and connect it to one or more SQL Server instances, you and your users can create:</span><span class="sxs-lookup"><span data-stu-id="b8f6f-105">After you install the resource provider and connect it to one or more SQL Server instances, you and your users can create:</span></span>

- <span data-ttu-id="b8f6f-106">Databases for cloud-native apps.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-106">Databases for cloud-native apps.</span></span>
- <span data-ttu-id="b8f6f-107">Websites that use SQL.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-107">Websites that use SQL.</span></span>
- <span data-ttu-id="b8f6f-108">Workloads that use SQL.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-108">Workloads that use SQL.</span></span>

<span data-ttu-id="b8f6f-109">The resource provider doesn't provide all the database management abilities of [Azure SQL Database](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="b8f6f-109">The resource provider doesn't provide all the database management abilities of [Azure SQL Database](https://azure.microsoft.com/services/sql-database/).</span></span> <span data-ttu-id="b8f6f-110">For example, elastic pools that automatically allocate resources aren't supported.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-110">For example, elastic pools that automatically allocate resources aren't supported.</span></span> <span data-ttu-id="b8f6f-111">However, the resource provider supports similar create, read, update, and delete (CRUD) operations on a SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-111">However, the resource provider supports similar create, read, update, and delete (CRUD) operations on a SQL Server database.</span></span> <span data-ttu-id="b8f6f-112">For more information about the resource provider API, see [Windows Azure Pack SQL Server Resource Provider REST API Reference](https://msdn.microsoft.com/library/dn528529.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8f6f-112">For more information about the resource provider API, see [Windows Azure Pack SQL Server Resource Provider REST API Reference](https://msdn.microsoft.com/library/dn528529.aspx).</span></span>

>[!NOTE]
<span data-ttu-id="b8f6f-113">The SQL Server resource provider API isn't compatible with Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-113">The SQL Server resource provider API isn't compatible with Azure SQL Database.</span></span>

## <a name="sql-resource-provider-adapter-architecture"></a><span data-ttu-id="b8f6f-114">SQL resource provider adapter architecture</span><span class="sxs-lookup"><span data-stu-id="b8f6f-114">SQL resource provider adapter architecture</span></span>

<span data-ttu-id="b8f6f-115">The resource provider consists of the following components:</span><span class="sxs-lookup"><span data-stu-id="b8f6f-115">The resource provider consists of the following components:</span></span>

- <span data-ttu-id="b8f6f-116">**The SQL resource provider adapter virtual machine (VM)**, which is a Windows Server VM that runs the provider services.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-116">**The SQL resource provider adapter virtual machine (VM)**, which is a Windows Server VM that runs the provider services.</span></span>
- <span data-ttu-id="b8f6f-117">**The resource provider**, which processes requests and accesses database resources.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-117">**The resource provider**, which processes requests and accesses database resources.</span></span>
- <span data-ttu-id="b8f6f-118">**Servers that host SQL Server**, which provide capacity for databases called hosting servers.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-118">**Servers that host SQL Server**, which provide capacity for databases called hosting servers.</span></span>

<span data-ttu-id="b8f6f-119">You must create at least one instance of SQL Server or provide access to external SQL Server instances.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-119">You must create at least one instance of SQL Server or provide access to external SQL Server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="b8f6f-120">Hosting servers that are installed on Azure Stack integrated systems must be created from a tenant subscription.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-120">Hosting servers that are installed on Azure Stack integrated systems must be created from a tenant subscription.</span></span> <span data-ttu-id="b8f6f-121">They can't be created from the default provider subscription.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-121">They can't be created from the default provider subscription.</span></span> <span data-ttu-id="b8f6f-122">They must be created from the tenant portal or by using PowerShell with the appropriate sign-in.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-122">They must be created from the tenant portal or by using PowerShell with the appropriate sign-in.</span></span> <span data-ttu-id="b8f6f-123">All hosting servers are billable virtual machines and must have licenses.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-123">All hosting servers are billable virtual machines and must have licenses.</span></span> <span data-ttu-id="b8f6f-124">The service administrator can be the owner of the tenant subscription.</span><span class="sxs-lookup"><span data-stu-id="b8f6f-124">The service administrator can be the owner of the tenant subscription.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8f6f-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="b8f6f-125">Next steps</span></span>

[<span data-ttu-id="b8f6f-126">Deploy the SQL Server resource provider</span><span class="sxs-lookup"><span data-stu-id="b8f6f-126">Deploy the SQL Server resource provider</span></span>](azure-stack-sql-resource-provider-deploy.md)
