---
title: GPUs on Azure Government | Microsoft Docs
description: Getting Started with GPUs on Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: yujhongmicrosoft
manager: zakramer
ms.assetid: 47e5e535-baa0-457e-8c41-f9fd65478b38
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 10/31/2017
ms.author: yujhongmicrosoft
ms.openlocfilehash: 286d89affc46d417d99f666c4f4be9a3b07efc61
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968607"
---
# <a name="gpus-on-azure-government"></a><span data-ttu-id="cdbfe-103">GPUs on Azure Government</span><span class="sxs-lookup"><span data-stu-id="cdbfe-103">GPUs on Azure Government</span></span>
<span data-ttu-id="cdbfe-104">This page will help you get started using GPUs on Azure Government.</span><span class="sxs-lookup"><span data-stu-id="cdbfe-104">This page will help you get started using GPUs on Azure Government.</span></span> 
## <a name="prerequisites"></a><span data-ttu-id="cdbfe-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cdbfe-105">Prerequisites</span></span>
<span data-ttu-id="cdbfe-106">To get started with GPUs and Data Science VMs on Azure Government, you must have an active Azure Government subscription.</span><span class="sxs-lookup"><span data-stu-id="cdbfe-106">To get started with GPUs and Data Science VMs on Azure Government, you must have an active Azure Government subscription.</span></span>
<span data-ttu-id="cdbfe-107">If you don't have an Azure Government subscription, create a [free account](https://azure.microsoft.com/overview/clouds/government/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="cdbfe-107">If you don't have an Azure Government subscription, create a [free account](https://azure.microsoft.com/overview/clouds/government/) before you begin.</span></span>

## <a name="variations"></a><span data-ttu-id="cdbfe-108">Variations</span><span class="sxs-lookup"><span data-stu-id="cdbfe-108">Variations</span></span>
<span data-ttu-id="cdbfe-109">NC-Virtual Machines powered by NVIDIA Tesla® K80 GPUs are available in the following regions:</span><span class="sxs-lookup"><span data-stu-id="cdbfe-109">NC-Virtual Machines powered by NVIDIA Tesla® K80 GPUs are available in the following regions:</span></span>
- <span data-ttu-id="cdbfe-110">US Gov Arizona</span><span class="sxs-lookup"><span data-stu-id="cdbfe-110">US Gov Arizona</span></span>
- <span data-ttu-id="cdbfe-111">US Gov Texas</span><span class="sxs-lookup"><span data-stu-id="cdbfe-111">US Gov Texas</span></span>

<span data-ttu-id="cdbfe-112">If you want to start deploying GPUs, navigate to the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cdbfe-112">If you want to start deploying GPUs, navigate to the Marketplace.</span></span>

<span data-ttu-id="cdbfe-113">**Windows offerings**: The following are supported in Azure Government:</span><span class="sxs-lookup"><span data-stu-id="cdbfe-113">**Windows offerings**: The following are supported in Azure Government:</span></span>
- <span data-ttu-id="cdbfe-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="cdbfe-114">Windows Server 2016</span></span>
- <span data-ttu-id="cdbfe-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cdbfe-115">Windows Server 2012 R2</span></span>

    <span data-ttu-id="cdbfe-116">Once the VM has been created, connect to the VM and install the [NVIDIA Tesla drivers](../virtual-machines/windows/n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="cdbfe-116">Once the VM has been created, connect to the VM and install the [NVIDIA Tesla drivers](../virtual-machines/windows/n-series-driver-setup.md).</span></span> 

<span data-ttu-id="cdbfe-117">**Linux offerings**: The following are supported in Azure Government:</span><span class="sxs-lookup"><span data-stu-id="cdbfe-117">**Linux offerings**: The following are supported in Azure Government:</span></span>
- <span data-ttu-id="cdbfe-118">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="cdbfe-118">Ubuntu 16.04 LTS</span></span>
- <span data-ttu-id="cdbfe-119">Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="cdbfe-119">Red Hat Enterprise Linux 7.3</span></span>
- <span data-ttu-id="cdbfe-120">CentOS-based 7.3</span><span class="sxs-lookup"><span data-stu-id="cdbfe-120">CentOS-based 7.3</span></span>

    <span data-ttu-id="cdbfe-121">Once the VM has been created, connect to the VM and install the [NVIDIA Tesla drivers](../virtual-machines/linux/n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="cdbfe-121">Once the VM has been created, connect to the VM and install the [NVIDIA Tesla drivers](../virtual-machines/linux/n-series-driver-setup.md).</span></span>

## <a name="data-science-vms"></a><span data-ttu-id="cdbfe-122">Data Science VMs</span><span class="sxs-lookup"><span data-stu-id="cdbfe-122">Data Science VMs</span></span>
<span data-ttu-id="cdbfe-123">For those new to Azure we recommend using the Data Science Virtual Machines which support Ubuntu and Windows Server 2016 DSVM solutions.</span><span class="sxs-lookup"><span data-stu-id="cdbfe-123">For those new to Azure we recommend using the Data Science Virtual Machines which support Ubuntu and Windows Server 2016 DSVM solutions.</span></span> 

>[!Note]
><span data-ttu-id="cdbfe-124">A DSVM has many VM sizes, but you will need to select “HDD” and an NC\* size.</span><span class="sxs-lookup"><span data-stu-id="cdbfe-124">A DSVM has many VM sizes, but you will need to select “HDD” and an NC\* size.</span></span>
>
> 

<span data-ttu-id="cdbfe-125">The Data Science Virtual Machine(DSVM) has many popular data science and deep learning tools already installed and configured.</span><span class="sxs-lookup"><span data-stu-id="cdbfe-125">The Data Science Virtual Machine(DSVM) has many popular data science and deep learning tools already installed and configured.</span></span> <span data-ttu-id="cdbfe-126">A list of tools available is located [here](../machine-learning/data-science-virtual-machine/overview.md).</span><span class="sxs-lookup"><span data-stu-id="cdbfe-126">A list of tools available is located [here](../machine-learning/data-science-virtual-machine/overview.md).</span></span>

### <a name="create-a-data-science-vm"></a><span data-ttu-id="cdbfe-127">Create a Data Science VM</span><span class="sxs-lookup"><span data-stu-id="cdbfe-127">Create a Data Science VM</span></span>
<span data-ttu-id="cdbfe-128">In order to create the Data Science VMs navigate to the [Azure Government Portal](https://portal.azure.us) and click "New" to access the Azure Government Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cdbfe-128">In order to create the Data Science VMs navigate to the [Azure Government Portal](https://portal.azure.us) and click "New" to access the Azure Government Marketplace.</span></span>

- [<span data-ttu-id="cdbfe-129">Provision a Windows Data Science VM</span><span class="sxs-lookup"><span data-stu-id="cdbfe-129">Provision a Windows Data Science VM</span></span>](../machine-learning/data-science-virtual-machine/provision-vm.md)
- [<span data-ttu-id="cdbfe-130">Provision a Linux Data Science VM</span><span class="sxs-lookup"><span data-stu-id="cdbfe-130">Provision a Linux Data Science VM</span></span>](../machine-learning/data-science-virtual-machine/dsvm-ubuntu-intro.md)

### <a name="using-a-data-science-vm"></a><span data-ttu-id="cdbfe-131">Using a Data Science VM</span><span class="sxs-lookup"><span data-stu-id="cdbfe-131">Using a Data Science VM</span></span>
- [<span data-ttu-id="cdbfe-132">Ten things you can do on the Windows Data Science VM</span><span class="sxs-lookup"><span data-stu-id="cdbfe-132">Ten things you can do on the Windows Data Science VM</span></span>](../machine-learning/data-science-virtual-machine/vm-do-ten-things.md)
- [<span data-ttu-id="cdbfe-133">Ten things you can do on the Linux Data Science VM</span><span class="sxs-lookup"><span data-stu-id="cdbfe-133">Ten things you can do on the Linux Data Science VM</span></span>](../machine-learning/data-science-virtual-machine/linux-dsvm-walkthrough.md)

## <a name="next-steps"></a><span data-ttu-id="cdbfe-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="cdbfe-134">Next steps</span></span>
<span data-ttu-id="cdbfe-135">For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov/).</span><span class="sxs-lookup"><span data-stu-id="cdbfe-135">For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov/).</span></span>
