---
title: Set up Azure accounts for acoustics - Cognitive Services
description: Follow this guide for setting up Azure Batch and Storage accounts necessary for working with acoustics.
services: cognitive-services
author: ashtat
manager: noelc
ms.service: cognitive-services
ms.component: acoustics
ms.topic: article
ms.date: 08/17/2018
ms.author: kegodin
ms.openlocfilehash: d8b7a4b88887d24880673df61a15c7eb66cbe2d3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966805"
---
# <a name="create-an-azure-batch-account"></a><span data-ttu-id="08c8a-103">Create an Azure Batch account</span><span class="sxs-lookup"><span data-stu-id="08c8a-103">Create an Azure Batch account</span></span>
<span data-ttu-id="08c8a-104">Follow this guide for setting up Azure Batch and Storage accounts necessary for working with acoustics.</span><span class="sxs-lookup"><span data-stu-id="08c8a-104">Follow this guide for setting up Azure Batch and Storage accounts necessary for working with acoustics.</span></span> <span data-ttu-id="08c8a-105">For information about the Unity plugin developed as part of Project Acoustics, see [What is acoustics](what-is-acoustics.md).</span><span class="sxs-lookup"><span data-stu-id="08c8a-105">For information about the Unity plugin developed as part of Project Acoustics, see [What is acoustics](what-is-acoustics.md).</span></span> <span data-ttu-id="08c8a-106">For information about how to incorporate acoustics into your Unity project, see [Getting Started](getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="08c8a-106">For information about how to incorporate acoustics into your Unity project, see [Getting Started](getting-started.md).</span></span>  

## <a name="get-an-azure-subscription"></a><span data-ttu-id="08c8a-107">Get an Azure subscription</span><span class="sxs-lookup"><span data-stu-id="08c8a-107">Get an Azure subscription</span></span>
<span data-ttu-id="08c8a-108">An [Azure Subscription](https://azure.microsoft.com/free/) is required before setting up Batch and Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="08c8a-108">An [Azure Subscription](https://azure.microsoft.com/free/) is required before setting up Batch and Storage accounts.</span></span> <span data-ttu-id="08c8a-109">If you're signing up for the first time, Azure provides a few time-limited free resources and $200 credit.</span><span class="sxs-lookup"><span data-stu-id="08c8a-109">If you're signing up for the first time, Azure provides a few time-limited free resources and $200 credit.</span></span>

## <a name="create-azure-batch-and-storage-accounts"></a><span data-ttu-id="08c8a-110">Create Azure Batch and storage accounts</span><span class="sxs-lookup"><span data-stu-id="08c8a-110">Create Azure Batch and storage accounts</span></span>
<span data-ttu-id="08c8a-111">Next, follow [these instructions](https://docs.microsoft.com/azure/batch/batch-account-create-portal) to set up your Azure Batch and associated Azure Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="08c8a-111">Next, follow [these instructions](https://docs.microsoft.com/azure/batch/batch-account-create-portal) to set up your Azure Batch and associated Azure Storage accounts.</span></span>

<span data-ttu-id="08c8a-112">Pick default options for both Batch and Storage accounts:</span><span class="sxs-lookup"><span data-stu-id="08c8a-112">Pick default options for both Batch and Storage accounts:</span></span>
  
  ![New Batch Account](media/NewBatchAccountCreate.png)

  ![New Storage Account](media/BatchStorageAccountCreate.png)

<span data-ttu-id="08c8a-115">It takes a few minutes for Azure to deploy the accounts.</span><span class="sxs-lookup"><span data-stu-id="08c8a-115">It takes a few minutes for Azure to deploy the accounts.</span></span> <span data-ttu-id="08c8a-116">Look for a completion notification in the upper right corner on the portal.</span><span class="sxs-lookup"><span data-stu-id="08c8a-116">Look for a completion notification in the upper right corner on the portal.</span></span>
  
  ![Accounts Deployed](media/BatchAccountsDeployNotification.png)

<span data-ttu-id="08c8a-118">Your accounts should now be visible on your dashboard.</span><span class="sxs-lookup"><span data-stu-id="08c8a-118">Your accounts should now be visible on your dashboard.</span></span>
  
  ![Portal Dashboard](media/AzurePortalDashboard.png)

## <a name="set-up-acoustics-bake-ui-with-azure-credentials"></a><span data-ttu-id="08c8a-120">Set up acoustics bake UI with Azure credentials</span><span class="sxs-lookup"><span data-stu-id="08c8a-120">Set up acoustics bake UI with Azure credentials</span></span>
<span data-ttu-id="08c8a-121">Click on the Batch account link on the dashboard, then click on the **Keys** link on the Batch account page to access your credentials.</span><span class="sxs-lookup"><span data-stu-id="08c8a-121">Click on the Batch account link on the dashboard, then click on the **Keys** link on the Batch account page to access your credentials.</span></span>
  
  ![Batch Keys Link](media/BatchAccessKeys.png)

  ![Batch Account Credentials](media/BatchKeysInfo.png)

<span data-ttu-id="08c8a-124">Click on the **Storage Account** link on the page to access your Azure Storage account credentials.</span><span class="sxs-lookup"><span data-stu-id="08c8a-124">Click on the **Storage Account** link on the page to access your Azure Storage account credentials.</span></span>
  
  ![Storage Account Credentials](media/StorageKeysInfo.png)

<span data-ttu-id="08c8a-126">Enter these credentials in the Bake tab as described in the [bake UI walkthrough](bake-ui-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="08c8a-126">Enter these credentials in the Bake tab as described in the [bake UI walkthrough](bake-ui-walkthrough.md).</span></span>

## <a name="node-types-and-region-support"></a><span data-ttu-id="08c8a-127">Node types and region support</span><span class="sxs-lookup"><span data-stu-id="08c8a-127">Node types and region support</span></span>
<span data-ttu-id="08c8a-128">Project Acoustics requires F- and H-series compute optimized Azure VM nodes which may not be supported in all Azure regions.</span><span class="sxs-lookup"><span data-stu-id="08c8a-128">Project Acoustics requires F- and H-series compute optimized Azure VM nodes which may not be supported in all Azure regions.</span></span> <span data-ttu-id="08c8a-129">Please check [this table](https://azure.microsoft.com/global-infrastructure/services) to ensure you're picking the right location for your Batch account.</span><span class="sxs-lookup"><span data-stu-id="08c8a-129">Please check [this table](https://azure.microsoft.com/global-infrastructure/services) to ensure you're picking the right location for your Batch account.</span></span> <span data-ttu-id="08c8a-130">At this moment H series virtual machines are supported in East US, North Central US, South Central US, West US, West US 2, North Europe, West Europe and Japan West.</span><span class="sxs-lookup"><span data-stu-id="08c8a-130">At this moment H series virtual machines are supported in East US, North Central US, South Central US, West US, West US 2, North Europe, West Europe and Japan West.</span></span>

## <a name="upgrading-your-quota"></a><span data-ttu-id="08c8a-131">Upgrading your quota</span><span class="sxs-lookup"><span data-stu-id="08c8a-131">Upgrading your quota</span></span>
<span data-ttu-id="08c8a-132">Azure Batch accounts are provisioned on account creation with a limit of 20 compute cores.</span><span class="sxs-lookup"><span data-stu-id="08c8a-132">Azure Batch accounts are provisioned on account creation with a limit of 20 compute cores.</span></span> <span data-ttu-id="08c8a-133">You may want to increase this limit for faster bake times, because you can parallelize your acoustics workload across many nodes, up to the number of probe points in your scene.</span><span class="sxs-lookup"><span data-stu-id="08c8a-133">You may want to increase this limit for faster bake times, because you can parallelize your acoustics workload across many nodes, up to the number of probe points in your scene.</span></span> <span data-ttu-id="08c8a-134">You can request a quota increase by clicking on the **Quota** link on your Azure Batch portal page and then clicking on **Request Quota Increase**:</span><span class="sxs-lookup"><span data-stu-id="08c8a-134">You can request a quota increase by clicking on the **Quota** link on your Azure Batch portal page and then clicking on **Request Quota Increase**:</span></span>

![Azure Quota Increase](media/azurequotas.png)

## <a name="next-steps"></a><span data-ttu-id="08c8a-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="08c8a-136">Next steps</span></span>
* <span data-ttu-id="08c8a-137">Get started [integrating acoustics into your Unity project](getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="08c8a-137">Get started [integrating acoustics into your Unity project](getting-started.md)</span></span>
* <span data-ttu-id="08c8a-138">Explore the [sample scene](sample-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="08c8a-138">Explore the [sample scene](sample-walkthrough.md)</span></span>

