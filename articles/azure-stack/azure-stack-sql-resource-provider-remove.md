---
title: Removing the SQL resource provider on Azure Stack | Microsoft Docs
description: Learn how you to remove the SQL resource provider from your Azure Stack deployment.
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
ms.date: 06/27/2018
ms.author: jeffgilb
ms.reviewer: jeffgo
ms.openlocfilehash: b73deebb10d0c81a06df9cd192eaa2ef28de744d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868907"
---
# <a name="remove-the-sql-resource-provider"></a><span data-ttu-id="3f9b2-103">Remove the SQL resource provider</span><span class="sxs-lookup"><span data-stu-id="3f9b2-103">Remove the SQL resource provider</span></span>

<span data-ttu-id="3f9b2-104">Before you remove the SQL resource provider, you must remove all the provider dependencies.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-104">Before you remove the SQL resource provider, you must remove all the provider dependencies.</span></span> <span data-ttu-id="3f9b2-105">You'll also need a copy of the deployment package that was used to install the resource provider.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-105">You'll also need a copy of the deployment package that was used to install the resource provider.</span></span>

<span data-ttu-id="3f9b2-106">There are several cleanup tasks to do before you run the _DeploySqlProvider.ps1_ script to remove the resource provider.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-106">There are several cleanup tasks to do before you run the _DeploySqlProvider.ps1_ script to remove the resource provider.</span></span>
<span data-ttu-id="3f9b2-107">The tenants are responsible for the following cleanup tasks:</span><span class="sxs-lookup"><span data-stu-id="3f9b2-107">The tenants are responsible for the following cleanup tasks:</span></span>

* <span data-ttu-id="3f9b2-108">Delete all their databases from the resource provider.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-108">Delete all their databases from the resource provider.</span></span> <span data-ttu-id="3f9b2-109">(Deleting the tenant databases doesn't delete the data.)</span><span class="sxs-lookup"><span data-stu-id="3f9b2-109">(Deleting the tenant databases doesn't delete the data.)</span></span>
* <span data-ttu-id="3f9b2-110">Unregister from the resource provider namespace.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-110">Unregister from the resource provider namespace.</span></span>

<span data-ttu-id="3f9b2-111">The administrator is responsible for the following cleanup tasks:</span><span class="sxs-lookup"><span data-stu-id="3f9b2-111">The administrator is responsible for the following cleanup tasks:</span></span>

* <span data-ttu-id="3f9b2-112">Deletes the hosting servers from the SQL resource provider.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-112">Deletes the hosting servers from the SQL resource provider.</span></span>
* <span data-ttu-id="3f9b2-113">Deletes any plans that reference the SQL resource provider.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-113">Deletes any plans that reference the SQL resource provider.</span></span>
* <span data-ttu-id="3f9b2-114">Deletes any quotas that are associated with the SQL resource provider.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-114">Deletes any quotas that are associated with the SQL resource provider.</span></span>

## <a name="to-remove-the-sql-resource-provider"></a><span data-ttu-id="3f9b2-115">To remove the SQL resource provider</span><span class="sxs-lookup"><span data-stu-id="3f9b2-115">To remove the SQL resource provider</span></span>

1. <span data-ttu-id="3f9b2-116">Verify that you've removed all the existing SQL resource provider dependencies.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-116">Verify that you've removed all the existing SQL resource provider dependencies.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3f9b2-117">Uninstalling the SQL resource provider will proceed even if dependent resources are currently using the resource provider.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-117">Uninstalling the SQL resource provider will proceed even if dependent resources are currently using the resource provider.</span></span>
  
2. <span data-ttu-id="3f9b2-118">Get a copy of the SQL resource provider binary and then run the self-extractor to extract the contents to a temporary directory.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-118">Get a copy of the SQL resource provider binary and then run the self-extractor to extract the contents to a temporary directory.</span></span>

3. <span data-ttu-id="3f9b2-119">Open a new elevated PowerShell console window and change to the directory where you extracted the SQL resource provider binary files.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-119">Open a new elevated PowerShell console window and change to the directory where you extracted the SQL resource provider binary files.</span></span>

4. <span data-ttu-id="3f9b2-120">Run the DeploySqlProvider.ps1 script using the following parameters:</span><span class="sxs-lookup"><span data-stu-id="3f9b2-120">Run the DeploySqlProvider.ps1 script using the following parameters:</span></span>

    * <span data-ttu-id="3f9b2-121">**Uninstall**.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-121">**Uninstall**.</span></span> <span data-ttu-id="3f9b2-122">Removes the resource provider and all associated resources.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-122">Removes the resource provider and all associated resources.</span></span>
    * <span data-ttu-id="3f9b2-123">**PrivilegedEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-123">**PrivilegedEndpoint**.</span></span> <span data-ttu-id="3f9b2-124">The IP address or DNS name of the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-124">The IP address or DNS name of the privileged endpoint.</span></span>
    * <span data-ttu-id="3f9b2-125">**CloudAdminCredential**.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-125">**CloudAdminCredential**.</span></span> <span data-ttu-id="3f9b2-126">The credential for the cloud administrator, necessary to access the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-126">The credential for the cloud administrator, necessary to access the privileged endpoint.</span></span>
    * <span data-ttu-id="3f9b2-127">**AzCredential**.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-127">**AzCredential**.</span></span> <span data-ttu-id="3f9b2-128">The credential for the Azure Stack service admin account.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-128">The credential for the Azure Stack service admin account.</span></span> <span data-ttu-id="3f9b2-129">Use the same credentials that you used for deploying Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3f9b2-129">Use the same credentials that you used for deploying Azure Stack.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f9b2-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f9b2-130">Next steps</span></span>

[<span data-ttu-id="3f9b2-131">Offer App Services as PaaS</span><span class="sxs-lookup"><span data-stu-id="3f9b2-131">Offer App Services as PaaS</span></span>](azure-stack-app-service-overview.md)
