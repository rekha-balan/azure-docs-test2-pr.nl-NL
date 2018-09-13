---
title: How to deploy a Web Service to multiple regions | Microsoft Docs
description: Steps to deploy (Copy) a New Web Service to other regions.
services: machine-learning
documentationcenter: ''
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3895537bbca72e687838ff5013c291dfee3be707
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564008"
---
# <a name="how-to-deploy-a-web-service-to-multiple-regions"></a><span data-ttu-id="08cbc-103">How to deploy a Web Service to multiple regions</span><span class="sxs-lookup"><span data-stu-id="08cbc-103">How to deploy a Web Service to multiple regions</span></span>
<span data-ttu-id="08cbc-104">The New Azure Web Services allow you to easily deploy a web service to multiple regions without needing multiple subscriptions or workspaces.</span><span class="sxs-lookup"><span data-stu-id="08cbc-104">The New Azure Web Services allow you to easily deploy a web service to multiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="08cbc-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy the web service.</span><span class="sxs-lookup"><span data-stu-id="08cbc-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy the web service.</span></span>

## <a name="to-create-a-plan-in-another-region"></a><span data-ttu-id="08cbc-106">To create a plan in another region</span><span class="sxs-lookup"><span data-stu-id="08cbc-106">To create a plan in another region</span></span>
1. <span data-ttu-id="08cbc-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="08cbc-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="08cbc-108">Click the **Plans** menu option.</span><span class="sxs-lookup"><span data-stu-id="08cbc-108">Click the **Plans** menu option.</span></span>
3. <span data-ttu-id="08cbc-109">On the Plans over view page, click **New**.</span><span class="sxs-lookup"><span data-stu-id="08cbc-109">On the Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="08cbc-110">From the **Subscription** dropdown, select the subscription in which the new plan will reside.</span><span class="sxs-lookup"><span data-stu-id="08cbc-110">From the **Subscription** dropdown, select the subscription in which the new plan will reside.</span></span>
5. <span data-ttu-id="08cbc-111">From the **Region** dropdown, select a region for the new plan.</span><span class="sxs-lookup"><span data-stu-id="08cbc-111">From the **Region** dropdown, select a region for the new plan.</span></span> <span data-ttu-id="08cbc-112">The Plan Options for the selected region will display in the **Plan Options** section of the page.</span><span class="sxs-lookup"><span data-stu-id="08cbc-112">The Plan Options for the selected region will display in the **Plan Options** section of the page.</span></span>
6. <span data-ttu-id="08cbc-113">From the **Resource Group** dropdown, select a resource group for the plan.</span><span class="sxs-lookup"><span data-stu-id="08cbc-113">From the **Resource Group** dropdown, select a resource group for the plan.</span></span> <span data-ttu-id="08cbc-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="08cbc-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="08cbc-115">In **Plan Name** type the name of the plan.</span><span class="sxs-lookup"><span data-stu-id="08cbc-115">In **Plan Name** type the name of the plan.</span></span>
8. <span data-ttu-id="08cbc-116">Under **Plan Options**, click the billing level for the new plan.</span><span class="sxs-lookup"><span data-stu-id="08cbc-116">Under **Plan Options**, click the billing level for the new plan.</span></span>
9. <span data-ttu-id="08cbc-117">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="08cbc-117">Click **Create**.</span></span>

## <a name="deploying-the-web-service-to-another-region"></a><span data-ttu-id="08cbc-118">Deploying the web service to another region</span><span class="sxs-lookup"><span data-stu-id="08cbc-118">Deploying the web service to another region</span></span>
1. <span data-ttu-id="08cbc-119">Click the **Web Services** menu option.</span><span class="sxs-lookup"><span data-stu-id="08cbc-119">Click the **Web Services** menu option.</span></span>
2. <span data-ttu-id="08cbc-120">Select the Web Service you are deploying to a new region.</span><span class="sxs-lookup"><span data-stu-id="08cbc-120">Select the Web Service you are deploying to a new region.</span></span>
3. <span data-ttu-id="08cbc-121">Click **Copy**.</span><span class="sxs-lookup"><span data-stu-id="08cbc-121">Click **Copy**.</span></span>
4. <span data-ttu-id="08cbc-122">In **Web Service Name**, type a new name for the web service.</span><span class="sxs-lookup"><span data-stu-id="08cbc-122">In **Web Service Name**, type a new name for the web service.</span></span>
5. <span data-ttu-id="08cbc-123">In **Web service description**, type a description for the web service.</span><span class="sxs-lookup"><span data-stu-id="08cbc-123">In **Web service description**, type a description for the web service.</span></span>
6. <span data-ttu-id="08cbc-124">From the **Subscription** dropdown, select the subscription in which the new web service will reside.</span><span class="sxs-lookup"><span data-stu-id="08cbc-124">From the **Subscription** dropdown, select the subscription in which the new web service will reside.</span></span>
7. <span data-ttu-id="08cbc-125">From the **Resource Group** dropdown, select a resource group for the web service.</span><span class="sxs-lookup"><span data-stu-id="08cbc-125">From the **Resource Group** dropdown, select a resource group for the web service.</span></span> <span data-ttu-id="08cbc-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="08cbc-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="08cbc-127">From the **Region** dropdown, select the region in which to deploy the web service.</span><span class="sxs-lookup"><span data-stu-id="08cbc-127">From the **Region** dropdown, select the region in which to deploy the web service.</span></span>
9. <span data-ttu-id="08cbc-128">From the **Storage account** dropdown, select a storage account in which to store the web service.</span><span class="sxs-lookup"><span data-stu-id="08cbc-128">From the **Storage account** dropdown, select a storage account in which to store the web service.</span></span>
10. <span data-ttu-id="08cbc-129">From the **Price Plan** dropdown, select a plan in the region you selected in step 8.</span><span class="sxs-lookup"><span data-stu-id="08cbc-129">From the **Price Plan** dropdown, select a plan in the region you selected in step 8.</span></span>
11. <span data-ttu-id="08cbc-130">Click **Copy**.</span><span class="sxs-lookup"><span data-stu-id="08cbc-130">Click **Copy**.</span></span>

