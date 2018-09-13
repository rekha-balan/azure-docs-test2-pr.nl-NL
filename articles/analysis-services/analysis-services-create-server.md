---
title: Create an Analysis Services server in Azure | Microsoft Docs
description: Learn how to create an Analysis Services server instance in Azure.
services: analysis-services
documentationcenter: ''
author: minewiskan
manager: erikre
editor: ''
tags: ''
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 04/17/2017
ms.author: owend
ms.openlocfilehash: 178643f8c418136e3d53c4cf0a0acc1ae0aeeae3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563720"
---
# <a name="create-an-analysis-services-server"></a><span data-ttu-id="f972f-103">Create an Analysis Services server</span><span class="sxs-lookup"><span data-stu-id="f972f-103">Create an Analysis Services server</span></span>
<span data-ttu-id="f972f-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f972f-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f972f-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="f972f-105">Before you begin</span></span>
<span data-ttu-id="f972f-106">To get started, you need:</span><span class="sxs-lookup"><span data-stu-id="f972f-106">To get started, you need:</span></span>

* <span data-ttu-id="f972f-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span><span class="sxs-lookup"><span data-stu-id="f972f-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="f972f-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span><span class="sxs-lookup"><span data-stu-id="f972f-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="f972f-109">And, you need to be signed in to Azure with an account in that Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f972f-109">And, you need to be signed in to Azure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="f972f-110">Microsoft accounts are not supported.</span><span class="sxs-lookup"><span data-stu-id="f972f-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="f972f-111">To learn more, see [User authentication](analysis-services-overview.md#secure).</span><span class="sxs-lookup"><span data-stu-id="f972f-111">To learn more, see [User authentication](analysis-services-overview.md#secure).</span></span>
* <span data-ttu-id="f972f-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f972f-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f972f-113">Creating an Analysis Services server might result in a new billable service.</span><span class="sxs-lookup"><span data-stu-id="f972f-113">Creating an Analysis Services server might result in a new billable service.</span></span> <span data-ttu-id="f972f-114">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="f972f-114">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="create-an-analysis-services-server"></a><span data-ttu-id="f972f-115">Create an Analysis Services server</span><span class="sxs-lookup"><span data-stu-id="f972f-115">Create an Analysis Services server</span></span>
1. <span data-ttu-id="f972f-116">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f972f-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f972f-117">Click **+ New** > **Intelligence + analytics** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="f972f-117">Click **+ New** > **Intelligence + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="f972f-118">In the **Analysis Services** blade, fill in the required fields, and then press **Create**.</span><span class="sxs-lookup"><span data-stu-id="f972f-118">In the **Analysis Services** blade, fill in the required fields, and then press **Create**.</span></span>
   
    ![Create server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="f972f-120">**Server name**: Type a unique name used to reference the server.</span><span class="sxs-lookup"><span data-stu-id="f972f-120">**Server name**: Type a unique name used to reference the server.</span></span>
   * <span data-ttu-id="f972f-121">**Subscription**: Select the subscription this server bills to.</span><span class="sxs-lookup"><span data-stu-id="f972f-121">**Subscription**: Select the subscription this server bills to.</span></span>
   * <span data-ttu-id="f972f-122">**Resource group**: These containers are designed to help you manage a collection of Azure resources.</span><span class="sxs-lookup"><span data-stu-id="f972f-122">**Resource group**: These containers are designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="f972f-123">To learn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f972f-123">To learn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="f972f-124">**Location**: This Azure datacenter location hosts the server.</span><span class="sxs-lookup"><span data-stu-id="f972f-124">**Location**: This Azure datacenter location hosts the server.</span></span> <span data-ttu-id="f972f-125">Choose a location nearest your largest user base.</span><span class="sxs-lookup"><span data-stu-id="f972f-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="f972f-126">**Pricing tier**: Select a pricing tier.</span><span class="sxs-lookup"><span data-stu-id="f972f-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="f972f-127">Tabular models up to 100 GB are supported.</span><span class="sxs-lookup"><span data-stu-id="f972f-127">Tabular models up to 100 GB are supported.</span></span> <span data-ttu-id="f972f-128">To learn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="f972f-128">To learn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="f972f-129">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f972f-129">Click **Create**.</span></span>

<span data-ttu-id="f972f-130">Create usually takes under a minute; often just a few seconds.</span><span class="sxs-lookup"><span data-stu-id="f972f-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="f972f-131">If you selected **Add to Portal**, navigate to your portal to see your new server.</span><span class="sxs-lookup"><span data-stu-id="f972f-131">If you selected **Add to Portal**, navigate to your portal to see your new server.</span></span> <span data-ttu-id="f972f-132">Or, navigate to **More services** > **Analysis Services** to see if your server is ready.</span><span class="sxs-lookup"><span data-stu-id="f972f-132">Or, navigate to **More services** > **Analysis Services** to see if your server is ready.</span></span>

 ![Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-create-server/aas-create-server-dashboard.png)

## <a name="automate-server-creation"></a><span data-ttu-id="f972f-134">Automate server creation</span><span class="sxs-lookup"><span data-stu-id="f972f-134">Automate server creation</span></span>
<span data-ttu-id="f972f-135">You can automate server provisioning on-the-fly with Azure Resource Manager template files.</span><span class="sxs-lookup"><span data-stu-id="f972f-135">You can automate server provisioning on-the-fly with Azure Resource Manager template files.</span></span> <span data-ttu-id="f972f-136">To learn more, watch this helpful video.</span><span class="sxs-lookup"><span data-stu-id="f972f-136">To learn more, watch this helpful video.</span></span>

>[!VIDEO https://channel9.msdn.com/series/Azure-Analysis-Services/AzureAnalysisServicesAutomation/player]
>
>


## <a name="next-steps"></a><span data-ttu-id="f972f-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="f972f-137">Next steps</span></span>
<span data-ttu-id="f972f-138">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) to it by using SSDT or with SSMS.</span><span class="sxs-lookup"><span data-stu-id="f972f-138">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) to it by using SSDT or with SSMS.</span></span>

<span data-ttu-id="f972f-139">If a model you deploy to your server connects to on-premises data sources, you need to install an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span><span class="sxs-lookup"><span data-stu-id="f972f-139">If a model you deploy to your server connects to on-premises data sources, you need to install an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>



