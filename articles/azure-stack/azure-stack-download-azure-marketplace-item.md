---
title: Download marketplace items from Azure | Microsoft Docs
description: I can download marketplace items from Azure to my Azure Stack deployment.
services: azure-stack
documentationcenter: ''
author: ErikjeMS
manager: byronr
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: erikje
ms.openlocfilehash: 37cbfd23e9678dcd2684c3be30099d1ff354ec34
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662454"
---
# <a name="download-marketplace-items-from-azure-to-azure-stack"></a><span data-ttu-id="d77c2-103">Download marketplace items from Azure to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d77c2-103">Download marketplace items from Azure to Azure Stack</span></span>

<span data-ttu-id="d77c2-104">As you decide what content to include in your Azure Stack marketplace, you should consider the content available from the Azure marketplace.</span><span class="sxs-lookup"><span data-stu-id="d77c2-104">As you decide what content to include in your Azure Stack marketplace, you should consider the content available from the Azure marketplace.</span></span> <span data-ttu-id="d77c2-105">You can download from a curated list of Azure marketplace items that have been pre-tested to run on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d77c2-105">You can download from a curated list of Azure marketplace items that have been pre-tested to run on Azure Stack.</span></span> <span data-ttu-id="d77c2-106">New items are frequently added to this list, so make sure check back for new content.</span><span class="sxs-lookup"><span data-stu-id="d77c2-106">New items are frequently added to this list, so make sure check back for new content.</span></span>

<span data-ttu-id="d77c2-107">To download marketplace items, you must first [register Azure Stack with Azure](azure-stack-register.md).</span><span class="sxs-lookup"><span data-stu-id="d77c2-107">To download marketplace items, you must first [register Azure Stack with Azure](azure-stack-register.md).</span></span> 

## <a name="download"></a><span data-ttu-id="d77c2-108">Download</span><span class="sxs-lookup"><span data-stu-id="d77c2-108">Download</span></span>
1. <span data-ttu-id="d77c2-109">Sign in to the Azure Stack portal (https://portal.local.azurestack.external) as a service administrator.</span><span class="sxs-lookup"><span data-stu-id="d77c2-109">Sign in to the Azure Stack portal (https://portal.local.azurestack.external) as a service administrator.</span></span>
2. <span data-ttu-id="d77c2-110">Some marketplace items can be very large.</span><span class="sxs-lookup"><span data-stu-id="d77c2-110">Some marketplace items can be very large.</span></span>  <span data-ttu-id="d77c2-111">Check to make sure you have enough space on your system by clicking **Resource Providers** > **Storage**.</span><span class="sxs-lookup"><span data-stu-id="d77c2-111">Check to make sure you have enough space on your system by clicking **Resource Providers** > **Storage**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-download-azure-marketplace-item/image01.PNG)

3. <span data-ttu-id="d77c2-112">Click **More Services** > **Marketplace Management**.</span><span class="sxs-lookup"><span data-stu-id="d77c2-112">Click **More Services** > **Marketplace Management**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-download-azure-marketplace-item/image02.PNG)

4. <span data-ttu-id="d77c2-113">Click **Add from Azure** to see a list of items available for download.</span><span class="sxs-lookup"><span data-stu-id="d77c2-113">Click **Add from Azure** to see a list of items available for download.</span></span> <span data-ttu-id="d77c2-114">You can click on each item in the list to view its description and download size.</span><span class="sxs-lookup"><span data-stu-id="d77c2-114">You can click on each item in the list to view its description and download size.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-download-azure-marketplace-item/image03.PNG)

5. <span data-ttu-id="d77c2-115">Select the item you want in the list and then click **Download**.</span><span class="sxs-lookup"><span data-stu-id="d77c2-115">Select the item you want in the list and then click **Download**.</span></span> <span data-ttu-id="d77c2-116">This starts downloading the VM image for the item you selected.</span><span class="sxs-lookup"><span data-stu-id="d77c2-116">This starts downloading the VM image for the item you selected.</span></span> <span data-ttu-id="d77c2-117">Download times vary.</span><span class="sxs-lookup"><span data-stu-id="d77c2-117">Download times vary.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-download-azure-marketplace-item/image04.png)

6. <span data-ttu-id="d77c2-118">After the download completes, you can deploy your new marketplace item as either a service administrator or tenant user.</span><span class="sxs-lookup"><span data-stu-id="d77c2-118">After the download completes, you can deploy your new marketplace item as either a service administrator or tenant user.</span></span> <span data-ttu-id="d77c2-119">Click **+New**, search among the categories for the new marketplace item, and then select the item.</span><span class="sxs-lookup"><span data-stu-id="d77c2-119">Click **+New**, search among the categories for the new marketplace item, and then select the item.</span></span>
7. <span data-ttu-id="d77c2-120">Click **Create** to open up the creation experience for the newly downloaded item.</span><span class="sxs-lookup"><span data-stu-id="d77c2-120">Click **Create** to open up the creation experience for the newly downloaded item.</span></span> <span data-ttu-id="d77c2-121">Follow the step-by-step instructions to deploy your item.</span><span class="sxs-lookup"><span data-stu-id="d77c2-121">Follow the step-by-step instructions to deploy your item.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d77c2-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="d77c2-122">Next steps</span></span>

[<span data-ttu-id="d77c2-123">Create and publish a Marketplace item</span><span class="sxs-lookup"><span data-stu-id="d77c2-123">Create and publish a Marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)




