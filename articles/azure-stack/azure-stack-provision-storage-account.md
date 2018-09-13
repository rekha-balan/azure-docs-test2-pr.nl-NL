---
title: Storage accounts in Azure Stack | Microsoft Docs
description: Learn how to create an Azure Stack storage account.
services: azure-stack
documentationcenter: ''
author: ErikjeMS
manager: byronr
editor: ''
ms.assetid: e1152110-b756-4c1a-9fa2-73fe3ab0ad8e
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 3/1/2017
ms.author: erikje
ms.openlocfilehash: c8aee5595c021cf55dfef3d6b8f9528bc540b198
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554183"
---
# <a name="storage-accounts-in-azure-stack"></a><span data-ttu-id="a846b-103">Storage accounts in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a846b-103">Storage accounts in Azure Stack</span></span>
<span data-ttu-id="a846b-104">Storage accounts include Blob and Table services, and the unique namespace for your storage data objects.</span><span class="sxs-lookup"><span data-stu-id="a846b-104">Storage accounts include Blob and Table services, and the unique namespace for your storage data objects.</span></span> <span data-ttu-id="a846b-105">By default, the data in your account is available only to you, the storage account owner.</span><span class="sxs-lookup"><span data-stu-id="a846b-105">By default, the data in your account is available only to you, the storage account owner.</span></span>

1. <span data-ttu-id="a846b-106">On the Azure Stack POC computer, log in to `https://adminportal.local.azurestack.external` as [an admin](azure-stack-connect-azure-stack.md), and then click **New** > **Data + Storage** > **Storage account**.</span><span class="sxs-lookup"><span data-stu-id="a846b-106">On the Azure Stack POC computer, log in to `https://adminportal.local.azurestack.external` as [an admin](azure-stack-connect-azure-stack.md), and then click **New** > **Data + Storage** > **Storage account**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-provision-storage-account/image01.png)
2. <span data-ttu-id="a846b-107">In the **Create storage account** blade, type a name for your storage account.</span><span class="sxs-lookup"><span data-stu-id="a846b-107">In the **Create storage account** blade, type a name for your storage account.</span></span> <span data-ttu-id="a846b-108">Create a new **Resource Group**, or select an existing one, then click **Create** to create the storage account.</span><span class="sxs-lookup"><span data-stu-id="a846b-108">Create a new **Resource Group**, or select an existing one, then click **Create** to create the storage account.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-provision-storage-account/image02.png)
3. <span data-ttu-id="a846b-109">To see your new storage account, click **All resources**, then search for the storage account and click its name.</span><span class="sxs-lookup"><span data-stu-id="a846b-109">To see your new storage account, click **All resources**, then search for the storage account and click its name.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-provision-storage-account/image03.png)

## <a name="next-steps"></a><span data-ttu-id="a846b-110">Next steps</span><span class="sxs-lookup"><span data-stu-id="a846b-110">Next steps</span></span>
[<span data-ttu-id="a846b-111">Use Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="a846b-111">Use Azure Resource Manager templates</span></span>](azure-stack-arm-templates.md)

[<span data-ttu-id="a846b-112">Learn about Azure storage accounts</span><span class="sxs-lookup"><span data-stu-id="a846b-112">Learn about Azure storage accounts</span></span>](../storage/storage-create-storage-account.md)

[<span data-ttu-id="a846b-113">Download the Azure Stack Azure-consistent Storage Validation Guide</span><span class="sxs-lookup"><span data-stu-id="a846b-113">Download the Azure Stack Azure-consistent Storage Validation Guide</span></span>](http://aka.ms/azurestacktp1doc)



