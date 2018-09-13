---
title: Comparing custom images and formulas in DevTest Labs | Microsoft Docs
description: Learn about the differences between custom images and formulas as VM bases so you can decide which one best suits your environment.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/05/2018
ms.author: spelluru
ms.openlocfilehash: 37288fd4a9c7558d05728b8ce03df505117e0232
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864970"
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="b3567-103">Comparing custom images and formulas in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b3567-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="b3567-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="b3567-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="b3567-105">However, the key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span><span class="sxs-lookup"><span data-stu-id="b3567-105">However, the key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="b3567-106">These preconfigured settings are set up with default values that can be overridden at the time of VM creation.</span><span class="sxs-lookup"><span data-stu-id="b3567-106">These preconfigured settings are set up with default values that can be overridden at the time of VM creation.</span></span> <span data-ttu-id="b3567-107">This article explains some of the advantages (pros) and disadvantages (cons) to using custom images versus using formulas.</span><span class="sxs-lookup"><span data-stu-id="b3567-107">This article explains some of the advantages (pros) and disadvantages (cons) to using custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="b3567-108">Custom image pros and cons</span><span class="sxs-lookup"><span data-stu-id="b3567-108">Custom image pros and cons</span></span>
<span data-ttu-id="b3567-109">Custom images provide a static, immutable way to create VMs from a desired environment.</span><span class="sxs-lookup"><span data-stu-id="b3567-109">Custom images provide a static, immutable way to create VMs from a desired environment.</span></span> 

<span data-ttu-id="b3567-110">**Pros**</span><span class="sxs-lookup"><span data-stu-id="b3567-110">**Pros**</span></span>

* <span data-ttu-id="b3567-111">VM provisioning from a custom image is fast as nothing changes after the VM is spun up from the image.</span><span class="sxs-lookup"><span data-stu-id="b3567-111">VM provisioning from a custom image is fast as nothing changes after the VM is spun up from the image.</span></span> <span data-ttu-id="b3567-112">In other words, there are no settings to apply as the custom image is just an image without settings.</span><span class="sxs-lookup"><span data-stu-id="b3567-112">In other words, there are no settings to apply as the custom image is just an image without settings.</span></span> 
* <span data-ttu-id="b3567-113">VMs created from a single custom image are identical.</span><span class="sxs-lookup"><span data-stu-id="b3567-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="b3567-114">**Cons**</span><span class="sxs-lookup"><span data-stu-id="b3567-114">**Cons**</span></span>

* <span data-ttu-id="b3567-115">If you need to update some aspect of the custom image, the image must be recreated.</span><span class="sxs-lookup"><span data-stu-id="b3567-115">If you need to update some aspect of the custom image, the image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="b3567-116">Formula pros and cons</span><span class="sxs-lookup"><span data-stu-id="b3567-116">Formula pros and cons</span></span>
<span data-ttu-id="b3567-117">Formulas provide a dynamic way to create VMs from the desired configuration/settings.</span><span class="sxs-lookup"><span data-stu-id="b3567-117">Formulas provide a dynamic way to create VMs from the desired configuration/settings.</span></span>

<span data-ttu-id="b3567-118">**Pros**</span><span class="sxs-lookup"><span data-stu-id="b3567-118">**Pros**</span></span>

* <span data-ttu-id="b3567-119">Changes in the environment can be captured on the fly via artifacts.</span><span class="sxs-lookup"><span data-stu-id="b3567-119">Changes in the environment can be captured on the fly via artifacts.</span></span> <span data-ttu-id="b3567-120">For example, if you want a VM installed with the latest bits from your release pipeline or enlist the latest code from your repository, you can simply specify an artifact that deploys the latest bits or enlists the latest code in the formula together with a target base image.</span><span class="sxs-lookup"><span data-stu-id="b3567-120">For example, if you want a VM installed with the latest bits from your release pipeline or enlist the latest code from your repository, you can simply specify an artifact that deploys the latest bits or enlists the latest code in the formula together with a target base image.</span></span> <span data-ttu-id="b3567-121">Whenever this formula is used to create VMs, the latest bits/code are deployed/enlisted to the VM.</span><span class="sxs-lookup"><span data-stu-id="b3567-121">Whenever this formula is used to create VMs, the latest bits/code are deployed/enlisted to the VM.</span></span> 
* <span data-ttu-id="b3567-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span><span class="sxs-lookup"><span data-stu-id="b3567-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="b3567-123">The settings saved in a formula are shown as default values, but can be modified when the VM is created.</span><span class="sxs-lookup"><span data-stu-id="b3567-123">The settings saved in a formula are shown as default values, but can be modified when the VM is created.</span></span> 

<span data-ttu-id="b3567-124">**Cons**</span><span class="sxs-lookup"><span data-stu-id="b3567-124">**Cons**</span></span>

* <span data-ttu-id="b3567-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span><span class="sxs-lookup"><span data-stu-id="b3567-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="b3567-126">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="b3567-126">Related blog posts</span></span>
* [<span data-ttu-id="b3567-127">Custom images or formulas?</span><span class="sxs-lookup"><span data-stu-id="b3567-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="b3567-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="b3567-128">Next steps</span></span>
- [<span data-ttu-id="b3567-129">DevTest Labs FAQ</span><span class="sxs-lookup"><span data-stu-id="b3567-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)