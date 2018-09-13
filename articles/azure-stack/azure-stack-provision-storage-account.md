---
title: Storage accounts in Azure Stack | Microsoft Docs
description: Learn how to create an Azure Stack storage account.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.assetid: e1152110-b756-4c1a-9fa2-73fe3ab0ad8e
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/08/2018
ms.author: mabrigg
ms.openlocfilehash: c3629dd252b7275d983042ed03bc6d0d9c258e38
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800831"
---
# <a name="storage-accounts-in-azure-stack"></a><span data-ttu-id="f9587-103">Storage accounts in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f9587-103">Storage accounts in Azure Stack</span></span>
<span data-ttu-id="f9587-104">Storage accounts include Blob and Table services, and the unique namespace for your storage data objects.</span><span class="sxs-lookup"><span data-stu-id="f9587-104">Storage accounts include Blob and Table services, and the unique namespace for your storage data objects.</span></span> <span data-ttu-id="f9587-105">By default, the data in your account is available only to you, the storage account owner.</span><span class="sxs-lookup"><span data-stu-id="f9587-105">By default, the data in your account is available only to you, the storage account owner.</span></span>

1. <span data-ttu-id="f9587-106">On the Azure Stack POC computer, sign in to `https://adminportal.local.azurestack.external` as [an admin](azure-stack-connect-azure-stack.md), and then click **New** > **Data + Storage** > **Storage account**.</span><span class="sxs-lookup"><span data-stu-id="f9587-106">On the Azure Stack POC computer, sign in to `https://adminportal.local.azurestack.external` as [an admin](azure-stack-connect-azure-stack.md), and then click **New** > **Data + Storage** > **Storage account**.</span></span>

   ![](media/azure-stack-provision-storage-account/image01.png)
2. <span data-ttu-id="f9587-107">In the **Create storage account** blade, type a name for your storage account.</span><span class="sxs-lookup"><span data-stu-id="f9587-107">In the **Create storage account** blade, type a name for your storage account.</span></span> <span data-ttu-id="f9587-108">Create a new **Resource Group**, or select an existing one, then click **Create** to create the storage account.</span><span class="sxs-lookup"><span data-stu-id="f9587-108">Create a new **Resource Group**, or select an existing one, then click **Create** to create the storage account.</span></span>

   ![](media/azure-stack-provision-storage-account/image02.png)
3. <span data-ttu-id="f9587-109">To see your new storage account, click **All resources**, then search for the storage account and click its name.</span><span class="sxs-lookup"><span data-stu-id="f9587-109">To see your new storage account, click **All resources**, then search for the storage account and click its name.</span></span>

    ![](media/azure-stack-provision-storage-account/image03.png)

### <a name="next-steps"></a><span data-ttu-id="f9587-110">Next steps</span><span class="sxs-lookup"><span data-stu-id="f9587-110">Next steps</span></span>
[<span data-ttu-id="f9587-111">Use Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="f9587-111">Use Azure Resource Manager templates</span></span>](user/azure-stack-arm-templates.md)

[<span data-ttu-id="f9587-112">Learn about Azure storage accounts</span><span class="sxs-lookup"><span data-stu-id="f9587-112">Learn about Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)

[<span data-ttu-id="f9587-113">Download the Azure Stack Azure-consistent Storage Validation Guide</span><span class="sxs-lookup"><span data-stu-id="f9587-113">Download the Azure Stack Azure-consistent Storage Validation Guide</span></span>](http://aka.ms/azurestacktp1doc)
