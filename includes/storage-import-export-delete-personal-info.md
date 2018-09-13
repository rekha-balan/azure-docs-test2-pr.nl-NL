---
title: include file
description: include file
services: azure-policy
author: craigshoemaker
ms.service: azure-policy
ms.topic: include
ms.date: 05/18/2018
ms.author: cshoe
ms.custom: include file
ms.openlocfilehash: 84631fee8dd72dc8b730fcd87a8ee3bac089620f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870940"
---
## <a name="deleting-personal-information"></a><span data-ttu-id="e65f6-103">Deleting personal information</span><span class="sxs-lookup"><span data-stu-id="e65f6-103">Deleting personal information</span></span>

[!INCLUDE [gdpr-intro-sentence.md](gdpr-intro-sentence.md)]

<span data-ttu-id="e65f6-104">Personal information is relevant to the import/export service (via the portal and API) during import and export operations.</span><span class="sxs-lookup"><span data-stu-id="e65f6-104">Personal information is relevant to the import/export service (via the portal and API) during import and export operations.</span></span> <span data-ttu-id="e65f6-105">Data used during these processes include:</span><span class="sxs-lookup"><span data-stu-id="e65f6-105">Data used during these processes include:</span></span>

- <span data-ttu-id="e65f6-106">Contact name</span><span class="sxs-lookup"><span data-stu-id="e65f6-106">Contact name</span></span>
- <span data-ttu-id="e65f6-107">Phone number</span><span class="sxs-lookup"><span data-stu-id="e65f6-107">Phone number</span></span>
- <span data-ttu-id="e65f6-108">Email</span><span class="sxs-lookup"><span data-stu-id="e65f6-108">Email</span></span>
- <span data-ttu-id="e65f6-109">Street address</span><span class="sxs-lookup"><span data-stu-id="e65f6-109">Street address</span></span>
- <span data-ttu-id="e65f6-110">City</span><span class="sxs-lookup"><span data-stu-id="e65f6-110">City</span></span>
- <span data-ttu-id="e65f6-111">Zip/postal code</span><span class="sxs-lookup"><span data-stu-id="e65f6-111">Zip/postal code</span></span>
- <span data-ttu-id="e65f6-112">State</span><span class="sxs-lookup"><span data-stu-id="e65f6-112">State</span></span>
- <span data-ttu-id="e65f6-113">Country/Province/Region</span><span class="sxs-lookup"><span data-stu-id="e65f6-113">Country/Province/Region</span></span>
- <span data-ttu-id="e65f6-114">Drive ID</span><span class="sxs-lookup"><span data-stu-id="e65f6-114">Drive ID</span></span>
- <span data-ttu-id="e65f6-115">Carrier account number</span><span class="sxs-lookup"><span data-stu-id="e65f6-115">Carrier account number</span></span>
- <span data-ttu-id="e65f6-116">Shipping tracking number</span><span class="sxs-lookup"><span data-stu-id="e65f6-116">Shipping tracking number</span></span>

<span data-ttu-id="e65f6-117">When an import/export job is created, users provide contact information and a shipping address.</span><span class="sxs-lookup"><span data-stu-id="e65f6-117">When an import/export job is created, users provide contact information and a shipping address.</span></span> <span data-ttu-id="e65f6-118">Personal information is stored in up to two different locations: in the job and optionally in the portal settings.</span><span class="sxs-lookup"><span data-stu-id="e65f6-118">Personal information is stored in up to two different locations: in the job and optionally in the portal settings.</span></span> <span data-ttu-id="e65f6-119">Personal information is only stored in portal settings if you check the checkbox labeled, **Save carrier and return address as default** during the *Return shipping info* section of the export process.</span><span class="sxs-lookup"><span data-stu-id="e65f6-119">Personal information is only stored in portal settings if you check the checkbox labeled, **Save carrier and return address as default** during the *Return shipping info* section of the export process.</span></span>

<span data-ttu-id="e65f6-120">Personal contact information may be deleted in the following ways:</span><span class="sxs-lookup"><span data-stu-id="e65f6-120">Personal contact information may be deleted in the following ways:</span></span>

- <span data-ttu-id="e65f6-121">Data saved with the job is deleted with the job.</span><span class="sxs-lookup"><span data-stu-id="e65f6-121">Data saved with the job is deleted with the job.</span></span> <span data-ttu-id="e65f6-122">Users can delete jobs manually and completed jobs are automatically deleted after 90 days.</span><span class="sxs-lookup"><span data-stu-id="e65f6-122">Users can delete jobs manually and completed jobs are automatically deleted after 90 days.</span></span> <span data-ttu-id="e65f6-123">You can manually delete the jobs via the REST API or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e65f6-123">You can manually delete the jobs via the REST API or the Azure portal.</span></span> <span data-ttu-id="e65f6-124">To delete the job in the Azure portal, go to your import/export job, and click *Delete* from the command bar.</span><span class="sxs-lookup"><span data-stu-id="e65f6-124">To delete the job in the Azure portal, go to your import/export job, and click *Delete* from the command bar.</span></span> <span data-ttu-id="e65f6-125">For details on how to delete an import/export job via REST API, refer to [Delete an import/export job](../articles/storage/common/storage-import-export-cancelling-and-deleting-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="e65f6-125">For details on how to delete an import/export job via REST API, refer to [Delete an import/export job](../articles/storage/common/storage-import-export-cancelling-and-deleting-jobs.md).</span></span>

- <span data-ttu-id="e65f6-126">Contact information saved in the portal settings may be removed by deleting the portal settings.</span><span class="sxs-lookup"><span data-stu-id="e65f6-126">Contact information saved in the portal settings may be removed by deleting the portal settings.</span></span> <span data-ttu-id="e65f6-127">You can delete portal settings by following these steps:</span><span class="sxs-lookup"><span data-stu-id="e65f6-127">You can delete portal settings by following these steps:</span></span>
  - <span data-ttu-id="e65f6-128">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e65f6-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
  - <span data-ttu-id="e65f6-129">Click on the *Settings* icon ![Azure Settings Icon](media/storage-import-export-delete-personal-info/azure-settings-icon.png)</span><span class="sxs-lookup"><span data-stu-id="e65f6-129">Click on the *Settings* icon ![Azure Settings Icon](media/storage-import-export-delete-personal-info/azure-settings-icon.png)</span></span>
  - <span data-ttu-id="e65f6-130">Click *Export all settings* (to save your current settings to a `.json` file).</span><span class="sxs-lookup"><span data-stu-id="e65f6-130">Click *Export all settings* (to save your current settings to a `.json` file).</span></span>
  - <span data-ttu-id="e65f6-131">Click *Delete all settings and private dashboards* to delete all settings including saved contact information.</span><span class="sxs-lookup"><span data-stu-id="e65f6-131">Click *Delete all settings and private dashboards* to delete all settings including saved contact information.</span></span>

<span data-ttu-id="e65f6-132">For more information, review the Microsoft Privacy policy at [Trust Center](https://www.microsoft.com/trustcenter)</span><span class="sxs-lookup"><span data-stu-id="e65f6-132">For more information, review the Microsoft Privacy policy at [Trust Center](https://www.microsoft.com/trustcenter)</span></span>