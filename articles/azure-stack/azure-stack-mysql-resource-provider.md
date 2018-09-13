---
title: Use MySQL databases as PaaS on Azure Stack | Microsoft Docs
description: Learn how you can deploy the MySQL Resource Provider and provide MySQL databases as a service on Azure Stack.
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
ms.openlocfilehash: 24ba595413cde07c420a94de234d7926e0eb0e7f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871328"
---
# <a name="use-mysql-databases-on-microsoft-azure-stack"></a><span data-ttu-id="5d2ba-103">Use MySQL databases on Microsoft Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5d2ba-103">Use MySQL databases on Microsoft Azure Stack</span></span>

<span data-ttu-id="5d2ba-104">You can deploy the MySQL resource provider API to use MySQL databases deployed in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-104">You can deploy the MySQL resource provider API to use MySQL databases deployed in Azure Stack.</span></span> <span data-ttu-id="5d2ba-105">For more information about the resource provider API, see [Windows Azure Pack MySQL Resource Provider REST API Reference](https://msdn.microsoft.com/library/dn528442.aspx).</span><span class="sxs-lookup"><span data-stu-id="5d2ba-105">For more information about the resource provider API, see [Windows Azure Pack MySQL Resource Provider REST API Reference](https://msdn.microsoft.com/library/dn528442.aspx).</span></span>

<span data-ttu-id="5d2ba-106">MySQL databases are common on websites and support many website platforms.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-106">MySQL databases are common on websites and support many website platforms.</span></span> <span data-ttu-id="5d2ba-107">For example, you can create WordPress websites using the Web Apps platform as a service (PaaS) add-on.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-107">For example, you can create WordPress websites using the Web Apps platform as a service (PaaS) add-on.</span></span>

<span data-ttu-id="5d2ba-108">After you deploy the resource provider, you can:</span><span class="sxs-lookup"><span data-stu-id="5d2ba-108">After you deploy the resource provider, you can:</span></span>

* <span data-ttu-id="5d2ba-109">Create MySQL servers and databases using Azure Resource Manager deployment templates.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-109">Create MySQL servers and databases using Azure Resource Manager deployment templates.</span></span>
* <span data-ttu-id="5d2ba-110">Provide MySQL databases as a service.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-110">Provide MySQL databases as a service.</span></span>  

## <a name="mysql-resource-provider-adapter-architecture"></a><span data-ttu-id="5d2ba-111">MySQL resource provider adapter architecture</span><span class="sxs-lookup"><span data-stu-id="5d2ba-111">MySQL resource provider adapter architecture</span></span>

<span data-ttu-id="5d2ba-112">The resource provider has the following components:</span><span class="sxs-lookup"><span data-stu-id="5d2ba-112">The resource provider has the following components:</span></span>

* <span data-ttu-id="5d2ba-113">**The MySQL resource provider adapter virtual machine (VM)**, which is a Windows Server VM that's running the provider services.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-113">**The MySQL resource provider adapter virtual machine (VM)**, which is a Windows Server VM that's running the provider services.</span></span>
* <span data-ttu-id="5d2ba-114">**The resource provider**, which processes requests and accesses database resources.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-114">**The resource provider**, which processes requests and accesses database resources.</span></span>
* <span data-ttu-id="5d2ba-115">**Servers that host MySQL Server**, which provide capacity for databases that are called hosting servers.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-115">**Servers that host MySQL Server**, which provide capacity for databases that are called hosting servers.</span></span> <span data-ttu-id="5d2ba-116">You can create MySQL instances yourself, or provide access to external MySQL instances.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-116">You can create MySQL instances yourself, or provide access to external MySQL instances.</span></span> <span data-ttu-id="5d2ba-117">The [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) has an example template that you can use to:</span><span class="sxs-lookup"><span data-stu-id="5d2ba-117">The [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) has an example template that you can use to:</span></span>

  * <span data-ttu-id="5d2ba-118">Create a MySQL server for you.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-118">Create a MySQL server for you.</span></span>
  * <span data-ttu-id="5d2ba-119">Download and deploy a MySQL Server from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-119">Download and deploy a MySQL Server from the Azure Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="5d2ba-120">Hosting servers that are installed on Azure Stack integrated systems must be created from a tenant subscription.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-120">Hosting servers that are installed on Azure Stack integrated systems must be created from a tenant subscription.</span></span> <span data-ttu-id="5d2ba-121">They can't be created from the default provider subscription.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-121">They can't be created from the default provider subscription.</span></span> <span data-ttu-id="5d2ba-122">They must be created from the tenant portal or from a PowerShell session with an appropriate sign-in.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-122">They must be created from the tenant portal or from a PowerShell session with an appropriate sign-in.</span></span> <span data-ttu-id="5d2ba-123">All hosting servers are billable VMs and must have licenses.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-123">All hosting servers are billable VMs and must have licenses.</span></span> <span data-ttu-id="5d2ba-124">The service administrator can be the owner of the tenant subscription.</span><span class="sxs-lookup"><span data-stu-id="5d2ba-124">The service administrator can be the owner of the tenant subscription.</span></span>

### <a name="required-privileges"></a><span data-ttu-id="5d2ba-125">Required privileges</span><span class="sxs-lookup"><span data-stu-id="5d2ba-125">Required privileges</span></span>

<span data-ttu-id="5d2ba-126">The system account must have the following privileges:</span><span class="sxs-lookup"><span data-stu-id="5d2ba-126">The system account must have the following privileges:</span></span>

* <span data-ttu-id="5d2ba-127">**Database:** create, drop</span><span class="sxs-lookup"><span data-stu-id="5d2ba-127">**Database:** create, drop</span></span>
* <span data-ttu-id="5d2ba-128">**Login:** create, set, drop, grant, revoke</span><span class="sxs-lookup"><span data-stu-id="5d2ba-128">**Login:** create, set, drop, grant, revoke</span></span>  

## <a name="next-steps"></a><span data-ttu-id="5d2ba-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="5d2ba-129">Next steps</span></span>

[<span data-ttu-id="5d2ba-130">Deploy the MySQL resource provider</span><span class="sxs-lookup"><span data-stu-id="5d2ba-130">Deploy the MySQL resource provider</span></span>](azure-stack-mysql-resource-provider-deploy.md)
