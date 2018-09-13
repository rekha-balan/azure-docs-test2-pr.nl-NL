---
title: Removing the MySQL resource provider on Azure Stack | Microsoft Docs
description: Learn how you can remove the MySQL resource provider from your Azure Stack deployment.
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
ms.openlocfilehash: d3a615e3b92a62709a787d0463dfa3148f14d07e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871484"
---
# <a name="remove-the-mysql-resource-provider"></a><span data-ttu-id="59ad8-103">Remove the MySQL resource provider</span><span class="sxs-lookup"><span data-stu-id="59ad8-103">Remove the MySQL resource provider</span></span>

<span data-ttu-id="59ad8-104">Before you remove the MySQL resource provider, you must remove all the provider dependencies.</span><span class="sxs-lookup"><span data-stu-id="59ad8-104">Before you remove the MySQL resource provider, you must remove all the provider dependencies.</span></span> <span data-ttu-id="59ad8-105">You'll also need a copy of the deployment package that was used to install the resource provider.</span><span class="sxs-lookup"><span data-stu-id="59ad8-105">You'll also need a copy of the deployment package that was used to install the resource provider.</span></span>

## <a name="dependency-cleanup"></a><span data-ttu-id="59ad8-106">Dependency cleanup</span><span class="sxs-lookup"><span data-stu-id="59ad8-106">Dependency cleanup</span></span>

<span data-ttu-id="59ad8-107">There are several cleanup tasks to do before you run the DeployMySqlProvider.ps1 script to remove the resource provider.</span><span class="sxs-lookup"><span data-stu-id="59ad8-107">There are several cleanup tasks to do before you run the DeployMySqlProvider.ps1 script to remove the resource provider.</span></span>

<span data-ttu-id="59ad8-108">The tenants are responsible for the following cleanup tasks:</span><span class="sxs-lookup"><span data-stu-id="59ad8-108">The tenants are responsible for the following cleanup tasks:</span></span>

* <span data-ttu-id="59ad8-109">Delete all their databases from the resource provider.</span><span class="sxs-lookup"><span data-stu-id="59ad8-109">Delete all their databases from the resource provider.</span></span> <span data-ttu-id="59ad8-110">(Deleting the tenant databases doesn't delete the data.)</span><span class="sxs-lookup"><span data-stu-id="59ad8-110">(Deleting the tenant databases doesn't delete the data.)</span></span>
* <span data-ttu-id="59ad8-111">Unregister from the provider namespace.</span><span class="sxs-lookup"><span data-stu-id="59ad8-111">Unregister from the provider namespace.</span></span>

<span data-ttu-id="59ad8-112">The administrator is responsible for the following cleanup tasks:</span><span class="sxs-lookup"><span data-stu-id="59ad8-112">The administrator is responsible for the following cleanup tasks:</span></span>

* <span data-ttu-id="59ad8-113">Deletes the hosting servers from the MySQL Adapter.</span><span class="sxs-lookup"><span data-stu-id="59ad8-113">Deletes the hosting servers from the MySQL Adapter.</span></span>
* <span data-ttu-id="59ad8-114">Deletes any plans that reference the MySQL Adapter.</span><span class="sxs-lookup"><span data-stu-id="59ad8-114">Deletes any plans that reference the MySQL Adapter.</span></span>
* <span data-ttu-id="59ad8-115">Deletes any quotas that are associated with the MySQL Adapter.</span><span class="sxs-lookup"><span data-stu-id="59ad8-115">Deletes any quotas that are associated with the MySQL Adapter.</span></span>

## <a name="to-remove-the-mysql-resource-provider"></a><span data-ttu-id="59ad8-116">To remove the MySQL resource provider</span><span class="sxs-lookup"><span data-stu-id="59ad8-116">To remove the MySQL resource provider</span></span>

1. <span data-ttu-id="59ad8-117">Verify that you've removed all the existing MySQL resource provider dependencies.</span><span class="sxs-lookup"><span data-stu-id="59ad8-117">Verify that you've removed all the existing MySQL resource provider dependencies.</span></span>

   >[!NOTE]
   ><span data-ttu-id="59ad8-118">Uninstalling the MySQL resource provider will proceed even if dependent resources are currently using the resource provider.</span><span class="sxs-lookup"><span data-stu-id="59ad8-118">Uninstalling the MySQL resource provider will proceed even if dependent resources are currently using the resource provider.</span></span>
  
2. <span data-ttu-id="59ad8-119">Get a copy of the MySQL resource provider binary and then run the self-extractor to extract the contents to a temporary directory.</span><span class="sxs-lookup"><span data-stu-id="59ad8-119">Get a copy of the MySQL resource provider binary and then run the self-extractor to extract the contents to a temporary directory.</span></span>
3. <span data-ttu-id="59ad8-120">Get a copy of the SQL resource provider binary and then run the self-extractor to extract the contents to a temporary directory.</span><span class="sxs-lookup"><span data-stu-id="59ad8-120">Get a copy of the SQL resource provider binary and then run the self-extractor to extract the contents to a temporary directory.</span></span>
4. <span data-ttu-id="59ad8-121">Open a new elevated PowerShell console window and change to the directory where you extracted the MySQL resource provider binary files.</span><span class="sxs-lookup"><span data-stu-id="59ad8-121">Open a new elevated PowerShell console window and change to the directory where you extracted the MySQL resource provider binary files.</span></span>
5. <span data-ttu-id="59ad8-122">Run the DeployMySqlProvider.ps1 script using the following parameters:</span><span class="sxs-lookup"><span data-stu-id="59ad8-122">Run the DeployMySqlProvider.ps1 script using the following parameters:</span></span>
    - <span data-ttu-id="59ad8-123">**Uninstall**.</span><span class="sxs-lookup"><span data-stu-id="59ad8-123">**Uninstall**.</span></span> <span data-ttu-id="59ad8-124">Removes the resource provider and all associated resources.</span><span class="sxs-lookup"><span data-stu-id="59ad8-124">Removes the resource provider and all associated resources.</span></span>
    - <span data-ttu-id="59ad8-125">**PrivilegedEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="59ad8-125">**PrivilegedEndpoint**.</span></span> <span data-ttu-id="59ad8-126">The IP address or DNS name of the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="59ad8-126">The IP address or DNS name of the privileged endpoint.</span></span>
    - <span data-ttu-id="59ad8-127">**CloudAdminCredential**.</span><span class="sxs-lookup"><span data-stu-id="59ad8-127">**CloudAdminCredential**.</span></span> <span data-ttu-id="59ad8-128">The credential for the cloud administrator, necessary to access the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="59ad8-128">The credential for the cloud administrator, necessary to access the privileged endpoint.</span></span>
    - <span data-ttu-id="59ad8-129">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="59ad8-129">**DirectoryTenantID**</span></span>
    - <span data-ttu-id="59ad8-130">**AzCredential**.</span><span class="sxs-lookup"><span data-stu-id="59ad8-130">**AzCredential**.</span></span> <span data-ttu-id="59ad8-131">The credential for the Azure Stack service admin account.</span><span class="sxs-lookup"><span data-stu-id="59ad8-131">The credential for the Azure Stack service admin account.</span></span> <span data-ttu-id="59ad8-132">Use the same credentials that you used for deploying Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="59ad8-132">Use the same credentials that you used for deploying Azure Stack.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59ad8-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="59ad8-133">Next steps</span></span>

[<span data-ttu-id="59ad8-134">Offer App Services as PaaS</span><span class="sxs-lookup"><span data-stu-id="59ad8-134">Offer App Services as PaaS</span></span>](azure-stack-app-service-overview.md)
