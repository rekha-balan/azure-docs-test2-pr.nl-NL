---
title: Comparing custom images and formulas in DevTest Labs | Microsoft Docs
description: Learn about the differences between custom images and formulas as VM bases so you can decide which one best suits your environment.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: ff771abc26c08f0adb977c29739d2f5c91924b21
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556421"
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="7b278-103">Comparing custom images and formulas in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="7b278-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="7b278-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="7b278-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="7b278-105">However, the key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span><span class="sxs-lookup"><span data-stu-id="7b278-105">However, the key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="7b278-106">These preconfigured settings are set up with default values that can be overridden at the time of VM creation.</span><span class="sxs-lookup"><span data-stu-id="7b278-106">These preconfigured settings are set up with default values that can be overridden at the time of VM creation.</span></span> <span data-ttu-id="7b278-107">This article explains some of the advantages (pros) and disadvantages (cons) to using custom images versus using formulas.</span><span class="sxs-lookup"><span data-stu-id="7b278-107">This article explains some of the advantages (pros) and disadvantages (cons) to using custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="7b278-108">Custom image pros and cons</span><span class="sxs-lookup"><span data-stu-id="7b278-108">Custom image pros and cons</span></span>
<span data-ttu-id="7b278-109">Custom images provide a static, immutable way to create VMs from a desired environment.</span><span class="sxs-lookup"><span data-stu-id="7b278-109">Custom images provide a static, immutable way to create VMs from a desired environment.</span></span> 

<span data-ttu-id="7b278-110">**Pros**</span><span class="sxs-lookup"><span data-stu-id="7b278-110">**Pros**</span></span>

* <span data-ttu-id="7b278-111">VM provisioning from a custom image is fast as nothing changes after the VM is spun up from the image.</span><span class="sxs-lookup"><span data-stu-id="7b278-111">VM provisioning from a custom image is fast as nothing changes after the VM is spun up from the image.</span></span> <span data-ttu-id="7b278-112">In other words, there are no settings to apply as the custom image is just an image without settings.</span><span class="sxs-lookup"><span data-stu-id="7b278-112">In other words, there are no settings to apply as the custom image is just an image without settings.</span></span> 
* <span data-ttu-id="7b278-113">VMs created from a single custom image are identical.</span><span class="sxs-lookup"><span data-stu-id="7b278-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="7b278-114">**Cons**</span><span class="sxs-lookup"><span data-stu-id="7b278-114">**Cons**</span></span>

* <span data-ttu-id="7b278-115">If you need to update some aspect of the custom image, the image must be recreated.</span><span class="sxs-lookup"><span data-stu-id="7b278-115">If you need to update some aspect of the custom image, the image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="7b278-116">Formula pros and cons</span><span class="sxs-lookup"><span data-stu-id="7b278-116">Formula pros and cons</span></span>
<span data-ttu-id="7b278-117">Formulas provide a dynamic way to create VMs from the desired configuration/settings.</span><span class="sxs-lookup"><span data-stu-id="7b278-117">Formulas provide a dynamic way to create VMs from the desired configuration/settings.</span></span>

<span data-ttu-id="7b278-118">**Pros**</span><span class="sxs-lookup"><span data-stu-id="7b278-118">**Pros**</span></span>

* <span data-ttu-id="7b278-119">Changes in the environment can be captured on the fly via artifacts.</span><span class="sxs-lookup"><span data-stu-id="7b278-119">Changes in the environment can be captured on the fly via artifacts.</span></span> <span data-ttu-id="7b278-120">For example, if you want a VM installed with the latest bits from your release pipeline or enlist the latest code from your repository, you can simply specify an artifact that deploys the latest bits or enlists the latest code in the formula together with a target base image.</span><span class="sxs-lookup"><span data-stu-id="7b278-120">For example, if you want a VM installed with the latest bits from your release pipeline or enlist the latest code from your repository, you can simply specify an artifact that deploys the latest bits or enlists the latest code in the formula together with a target base image.</span></span> <span data-ttu-id="7b278-121">Whenever this formula is used to create VMs, the latest bits/code are deployed/enlisted to the VM.</span><span class="sxs-lookup"><span data-stu-id="7b278-121">Whenever this formula is used to create VMs, the latest bits/code are deployed/enlisted to the VM.</span></span> 
* <span data-ttu-id="7b278-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span><span class="sxs-lookup"><span data-stu-id="7b278-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="7b278-123">The settings saved in a formula are shown as default values, but can be modified when the VM is created.</span><span class="sxs-lookup"><span data-stu-id="7b278-123">The settings saved in a formula are shown as default values, but can be modified when the VM is created.</span></span> 

<span data-ttu-id="7b278-124">**Cons**</span><span class="sxs-lookup"><span data-stu-id="7b278-124">**Cons**</span></span>

* <span data-ttu-id="7b278-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span><span class="sxs-lookup"><span data-stu-id="7b278-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="7b278-126">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="7b278-126">Related blog posts</span></span>
* [<span data-ttu-id="7b278-127">Custom images or formulas?</span><span class="sxs-lookup"><span data-stu-id="7b278-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="7b278-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="7b278-128">Next steps</span></span>
- [<span data-ttu-id="7b278-129">DevTest Labs FAQ</span><span class="sxs-lookup"><span data-stu-id="7b278-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)