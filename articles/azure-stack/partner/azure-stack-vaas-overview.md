---
title: An overview of validation as a service for Azure Stack | Microsoft Docs
description: An overview of Azure Stack validation as a service known issues.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2018
ms.author: mabrigg
ms.reviewer: johnhas
ms.openlocfilehash: 56251245a23df031f3bc8fe3d36de43e194fbcc7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870709"
---
# <a name="what-is-validation-as-a-service-for-azure-stack"></a><span data-ttu-id="ba30d-103">What is validation as a service for Azure Stack?</span><span class="sxs-lookup"><span data-stu-id="ba30d-103">What is validation as a service for Azure Stack?</span></span>

[!INCLUDE [Azure_Stack_Partner](./includes/azure-stack-partner-appliesto.md)]

<span data-ttu-id="ba30d-104">Validation as a service (VaaS) is a native Azure service designed for solution partners who are co-engineering Azure Stack offerings with Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ba30d-104">Validation as a service (VaaS) is a native Azure service designed for solution partners who are co-engineering Azure Stack offerings with Microsoft.</span></span> <span data-ttu-id="ba30d-105">Solution partners can use the service to check that their solutions meet Microsoft's requirements and work as expected with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ba30d-105">Solution partners can use the service to check that their solutions meet Microsoft's requirements and work as expected with Azure Stack.</span></span>

<span data-ttu-id="ba30d-106">The primary use for VaaS is:</span><span class="sxs-lookup"><span data-stu-id="ba30d-106">The primary use for VaaS is:</span></span>

- <span data-ttu-id="ba30d-107">Validate new Azure Stack solutions</span><span class="sxs-lookup"><span data-stu-id="ba30d-107">Validate new Azure Stack solutions</span></span>
- <span data-ttu-id="ba30d-108">Validate changes to the Azure Stack software</span><span class="sxs-lookup"><span data-stu-id="ba30d-108">Validate changes to the Azure Stack software</span></span>
- <span data-ttu-id="ba30d-109">Get digitally signed solution partner packages used during deployment</span><span class="sxs-lookup"><span data-stu-id="ba30d-109">Get digitally signed solution partner packages used during deployment</span></span>
- <span data-ttu-id="ba30d-110">Preview Azure Stack validation collateral</span><span class="sxs-lookup"><span data-stu-id="ba30d-110">Preview Azure Stack validation collateral</span></span>

## <a name="validate-new-azure-stack-solution"></a><span data-ttu-id="ba30d-111">Validate new Azure Stack solution</span><span class="sxs-lookup"><span data-stu-id="ba30d-111">Validate new Azure Stack solution</span></span>

<span data-ttu-id="ba30d-112">Partners use the solution validation workflow to check new Azure Stack solutions.</span><span class="sxs-lookup"><span data-stu-id="ba30d-112">Partners use the solution validation workflow to check new Azure Stack solutions.</span></span> <span data-ttu-id="ba30d-113">The solution must pass the required Hardware Lab Kit (HKL) Azure Stack tests component tests.</span><span class="sxs-lookup"><span data-stu-id="ba30d-113">The solution must pass the required Hardware Lab Kit (HKL) Azure Stack tests component tests.</span></span> <span data-ttu-id="ba30d-114">You only need to run the workflow twice for each new solution: once for the minimum and maximum configuration.</span><span class="sxs-lookup"><span data-stu-id="ba30d-114">You only need to run the workflow twice for each new solution: once for the minimum and maximum configuration.</span></span>

<span data-ttu-id="ba30d-115">For more information, see [Validate a new Azure Stack solution](azure-stack-vaas-validate-solution-new.md).</span><span class="sxs-lookup"><span data-stu-id="ba30d-115">For more information, see [Validate a new Azure Stack solution](azure-stack-vaas-validate-solution-new.md).</span></span>

## <a name="validate-changes-to-the-azure-stack-software"></a><span data-ttu-id="ba30d-116">Validate changes to the Azure Stack software</span><span class="sxs-lookup"><span data-stu-id="ba30d-116">Validate changes to the Azure Stack software</span></span>

<span data-ttu-id="ba30d-117">Partners use the  package validation workflow to check that their solution works with the recent Azure Stack software update.</span><span class="sxs-lookup"><span data-stu-id="ba30d-117">Partners use the  package validation workflow to check that their solution works with the recent Azure Stack software update.</span></span> <span data-ttu-id="ba30d-118">At a minimum, the package validation workflow must be run on the hardware environment recommended by Microsoft, and on a solution where the patch and update (P&U) were used to apply the update.</span><span class="sxs-lookup"><span data-stu-id="ba30d-118">At a minimum, the package validation workflow must be run on the hardware environment recommended by Microsoft, and on a solution where the patch and update (P&U) were used to apply the update.</span></span> <span data-ttu-id="ba30d-119">You should run the package validation on the baseline build.</span><span class="sxs-lookup"><span data-stu-id="ba30d-119">You should run the package validation on the baseline build.</span></span>

<span data-ttu-id="ba30d-120">For more information, see [Validate software updates from Microsoft](azure-stack-vaas-validate-microsoft-updates.md).</span><span class="sxs-lookup"><span data-stu-id="ba30d-120">For more information, see [Validate software updates from Microsoft](azure-stack-vaas-validate-microsoft-updates.md).</span></span>

## <a name="get-digitally-signed-solution-partner-packages"></a><span data-ttu-id="ba30d-121">Get digitally signed solution partner packages</span><span class="sxs-lookup"><span data-stu-id="ba30d-121">Get digitally signed solution partner packages</span></span>

<span data-ttu-id="ba30d-122">In addition to validating Azure Stack updates, you can use the package validation workflow to check updates to OEM customization packages, which include Azure Stack partner-specific drivers, firmware, and other software used during deployment of the Azure Stack software.</span><span class="sxs-lookup"><span data-stu-id="ba30d-122">In addition to validating Azure Stack updates, you can use the package validation workflow to check updates to OEM customization packages, which include Azure Stack partner-specific drivers, firmware, and other software used during deployment of the Azure Stack software.</span></span> <span data-ttu-id="ba30d-123">Deploy the package you are checking on the current version of the Azure Stack software using at a least the minimum sized solution that will be supported.</span><span class="sxs-lookup"><span data-stu-id="ba30d-123">Deploy the package you are checking on the current version of the Azure Stack software using at a least the minimum sized solution that will be supported.</span></span> <span data-ttu-id="ba30d-124">The updated package must be uploaded to the service before to starting the test.</span><span class="sxs-lookup"><span data-stu-id="ba30d-124">The updated package must be uploaded to the service before to starting the test.</span></span> <span data-ttu-id="ba30d-125">If the tests succeed, notify vaashelp@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="ba30d-125">If the tests succeed, notify vaashelp@microsoft.com.</span></span> <span data-ttu-id="ba30d-126">Tell the Azure Stack partner that the package has completed testing and should be digitally signed with the Azure Stack digital signature.</span><span class="sxs-lookup"><span data-stu-id="ba30d-126">Tell the Azure Stack partner that the package has completed testing and should be digitally signed with the Azure Stack digital signature.</span></span> <span data-ttu-id="ba30d-127">Microsoft signs the package and notifies the Azure Stack partner that the package is available for download in the portal.</span><span class="sxs-lookup"><span data-stu-id="ba30d-127">Microsoft signs the package and notifies the Azure Stack partner that the package is available for download in the portal.</span></span>

<span data-ttu-id="ba30d-128">For more information, see [Validate OEM packages](azure-stack-vaas-validate-oem-package.md).</span><span class="sxs-lookup"><span data-stu-id="ba30d-128">For more information, see [Validate OEM packages](azure-stack-vaas-validate-oem-package.md).</span></span>

## <a name="preview-azure-stack-validation-collateral"></a><span data-ttu-id="ba30d-129">Preview Azure Stack validation collateral</span><span class="sxs-lookup"><span data-stu-id="ba30d-129">Preview Azure Stack validation collateral</span></span>

<span data-ttu-id="ba30d-130">Microsoft regularly makes new features available in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ba30d-130">Microsoft regularly makes new features available in Azure Stack.</span></span> <span data-ttu-id="ba30d-131">As part of the development process for delivering these features to market, new test collateral is made available in the test-pass workflow.</span><span class="sxs-lookup"><span data-stu-id="ba30d-131">As part of the development process for delivering these features to market, new test collateral is made available in the test-pass workflow.</span></span> <span data-ttu-id="ba30d-132">The test-pass workflow includes test collateral from the other workflows to allow for unofficial test execution.</span><span class="sxs-lookup"><span data-stu-id="ba30d-132">The test-pass workflow includes test collateral from the other workflows to allow for unofficial test execution.</span></span> <span data-ttu-id="ba30d-133">Do not use the test-pass workflow to submit results for approval.</span><span class="sxs-lookup"><span data-stu-id="ba30d-133">Do not use the test-pass workflow to submit results for approval.</span></span> <span data-ttu-id="ba30d-134">Use the solution validation and package validations workflow to get official approval for your solution.</span><span class="sxs-lookup"><span data-stu-id="ba30d-134">Use the solution validation and package validations workflow to get official approval for your solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba30d-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="ba30d-135">Next steps</span></span>

- <span data-ttu-id="ba30d-136">Get started, and [Set up your validation as a service account](azure-stack-vaas-validate-solution-new.md)</span><span class="sxs-lookup"><span data-stu-id="ba30d-136">Get started, and [Set up your validation as a service account](azure-stack-vaas-validate-solution-new.md)</span></span>
