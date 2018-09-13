---
title: How to assign an MSI access to an Azure resource, using the Azure portal
description: Step-by-step instructions for assigning an MSI on one resource access to another resource, by using the Azure portal.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/14/2017
ms.author: daveba
ms.openlocfilehash: c2048583cde397ac3325fd149982b3a3db475566
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856875"
---
# <a name="assign-a-managed-service-identity-access-to-a-resource-by-using-the-azure-portal"></a><span data-ttu-id="5e11f-103">Assign a Managed Service Identity access to a resource by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="5e11f-103">Assign a Managed Service Identity access to a resource by using the Azure portal</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="5e11f-104">After you've configured an Azure resource with a Managed Service Identity (MSI), you can give the MSI access to another resource, just like any security principal.</span><span class="sxs-lookup"><span data-stu-id="5e11f-104">After you've configured an Azure resource with a Managed Service Identity (MSI), you can give the MSI access to another resource, just like any security principal.</span></span> <span data-ttu-id="5e11f-105">This article shows you how to give an Azure virtual machine or virtual machine scale set's MSI access to an Azure storage account, by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5e11f-105">This article shows you how to give an Azure virtual machine or virtual machine scale set's MSI access to an Azure storage account, by using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e11f-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5e11f-106">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

## <a name="use-rbac-to-assign-the-msi-access-to-another-resource"></a><span data-ttu-id="5e11f-107">Use RBAC to assign the MSI access to another resource</span><span class="sxs-lookup"><span data-stu-id="5e11f-107">Use RBAC to assign the MSI access to another resource</span></span>

<span data-ttu-id="5e11f-108">After you've enabled MSI on an Azure resource, such as an [Azure VM](qs-configure-portal-windows-vm.md) or [Azure VMSS](qs-configure-portal-windows-vmss.md):</span><span class="sxs-lookup"><span data-stu-id="5e11f-108">After you've enabled MSI on an Azure resource, such as an [Azure VM](qs-configure-portal-windows-vm.md) or [Azure VMSS](qs-configure-portal-windows-vmss.md):</span></span>

1. <span data-ttu-id="5e11f-109">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription under which you have configured the MSI.</span><span class="sxs-lookup"><span data-stu-id="5e11f-109">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription under which you have configured the MSI.</span></span>

2. <span data-ttu-id="5e11f-110">Navigate to the desired resource on which you want to modify access control.</span><span class="sxs-lookup"><span data-stu-id="5e11f-110">Navigate to the desired resource on which you want to modify access control.</span></span> <span data-ttu-id="5e11f-111">In this example, we are giving an Azure virtual machine and Azure virtual machine scale set access to a storage account, so we navigate to the storage account.</span><span class="sxs-lookup"><span data-stu-id="5e11f-111">In this example, we are giving an Azure virtual machine and Azure virtual machine scale set access to a storage account, so we navigate to the storage account.</span></span>

3. <span data-ttu-id="5e11f-112">For an Azure virtual machine, select the **Access control (IAM)** page of the resource, and select **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="5e11f-112">For an Azure virtual machine, select the **Access control (IAM)** page of the resource, and select **+ Add**.</span></span> <span data-ttu-id="5e11f-113">Then specify the **Role**, **Assign access to Virtual Machine**, and specify the corresponding **Subscription** and **Resource Group** where the resource resides.</span><span class="sxs-lookup"><span data-stu-id="5e11f-113">Then specify the **Role**, **Assign access to Virtual Machine**, and specify the corresponding **Subscription** and **Resource Group** where the resource resides.</span></span> <span data-ttu-id="5e11f-114">Under the search criteria area, you should see the resource.</span><span class="sxs-lookup"><span data-stu-id="5e11f-114">Under the search criteria area, you should see the resource.</span></span> <span data-ttu-id="5e11f-115">Select the resource, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="5e11f-115">Select the resource, and select **Save**.</span></span> 

   <span data-ttu-id="5e11f-116">![Access control (IAM) screenshot](./media/msi-howto-assign-access-portal/assign-access-control-iam-blade-before.png)</span><span class="sxs-lookup"><span data-stu-id="5e11f-116">![Access control (IAM) screenshot](./media/msi-howto-assign-access-portal/assign-access-control-iam-blade-before.png)</span></span>  
   <span data-ttu-id="5e11f-117">For an Azure virtual machine scale set, select the **Access control (IAM)** page of the resource, and select **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="5e11f-117">For an Azure virtual machine scale set, select the **Access control (IAM)** page of the resource, and select **+ Add**.</span></span> <span data-ttu-id="5e11f-118">Then specify the **Role**, **Assign access to**.</span><span class="sxs-lookup"><span data-stu-id="5e11f-118">Then specify the **Role**, **Assign access to**.</span></span> <span data-ttu-id="5e11f-119">Under the search criteria area, search for  your virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="5e11f-119">Under the search criteria area, search for  your virtual machine scale set.</span></span> <span data-ttu-id="5e11f-120">Select the resource, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="5e11f-120">Select the resource, and select **Save**.</span></span>
   
   ![Access control (IAM) screenshot](./media/msi-howto-assign-access-vmss-portal/assign-access-control-vmss-iam-blade-before.png)  

4. <span data-ttu-id="5e11f-122">You are returned to the main **Access control (IAM)** page, where you see a new entry for the resource's MSI.</span><span class="sxs-lookup"><span data-stu-id="5e11f-122">You are returned to the main **Access control (IAM)** page, where you see a new entry for the resource's MSI.</span></span>

    <span data-ttu-id="5e11f-123">Azure virtual machine:</span><span class="sxs-lookup"><span data-stu-id="5e11f-123">Azure virtual machine:</span></span>

   ![Access control (IAM) screenshot](./media/msi-howto-assign-access-portal/assign-access-control-iam-blade-after.png)

    <span data-ttu-id="5e11f-125">Azure virtual machine scale set:</span><span class="sxs-lookup"><span data-stu-id="5e11f-125">Azure virtual machine scale set:</span></span>

    ![Access control (IAM) screenshot](./media/msi-howto-assign-access-vmss-portal/assign-access-control-vmss-iam-blade-after.png)

## <a name="troubleshooting"></a><span data-ttu-id="5e11f-127">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="5e11f-127">Troubleshooting</span></span>

<span data-ttu-id="5e11f-128">If the MSI for the resource does not show up in the list of available identities, verify that the MSI has been enabled correctly.</span><span class="sxs-lookup"><span data-stu-id="5e11f-128">If the MSI for the resource does not show up in the list of available identities, verify that the MSI has been enabled correctly.</span></span> <span data-ttu-id="5e11f-129">In our case, we can go back to the Azure virtual machine, and check the following:</span><span class="sxs-lookup"><span data-stu-id="5e11f-129">In our case, we can go back to the Azure virtual machine, and check the following:</span></span>

- <span data-ttu-id="5e11f-130">Look at the **Configuration** page and ensure that the value for **MSI enabled** is **Yes**.</span><span class="sxs-lookup"><span data-stu-id="5e11f-130">Look at the **Configuration** page and ensure that the value for **MSI enabled** is **Yes**.</span></span>
- <span data-ttu-id="5e11f-131">Look at the **Extensions** page and ensure that the MSI extension deployed successfully (**Extensions** page is not available for an Azure virtual machine scale set).</span><span class="sxs-lookup"><span data-stu-id="5e11f-131">Look at the **Extensions** page and ensure that the MSI extension deployed successfully (**Extensions** page is not available for an Azure virtual machine scale set).</span></span>

<span data-ttu-id="5e11f-132">If either is incorrect, you might need to redeploy the MSI on your resource again, or troubleshoot the deployment failure.</span><span class="sxs-lookup"><span data-stu-id="5e11f-132">If either is incorrect, you might need to redeploy the MSI on your resource again, or troubleshoot the deployment failure.</span></span>

## <a name="related-content"></a><span data-ttu-id="5e11f-133">Related content</span><span class="sxs-lookup"><span data-stu-id="5e11f-133">Related content</span></span>

- <span data-ttu-id="5e11f-134">For an overview of MSI, see [Managed Service Identity overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e11f-134">For an overview of MSI, see [Managed Service Identity overview](overview.md).</span></span>
- <span data-ttu-id="5e11f-135">To enable MSI on an Azure virtual machine, see [Configure an Azure VM Managed Service Identity (MSI) using the Azure portal](qs-configure-portal-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="5e11f-135">To enable MSI on an Azure virtual machine, see [Configure an Azure VM Managed Service Identity (MSI) using the Azure portal](qs-configure-portal-windows-vm.md).</span></span>
- <span data-ttu-id="5e11f-136">To enable MSI on an Azure virtual machine scale set, see [Configure an Azure Virtual Machine Scale Set Managed Service Identity (MSI) using the Azure portal](qs-configure-portal-windows-vmss.md)</span><span class="sxs-lookup"><span data-stu-id="5e11f-136">To enable MSI on an Azure virtual machine scale set, see [Configure an Azure Virtual Machine Scale Set Managed Service Identity (MSI) using the Azure portal](qs-configure-portal-windows-vmss.md)</span></span>


