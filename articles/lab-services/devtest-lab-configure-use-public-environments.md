---
title: Configure and use public environments in Azure DevTest Labs | Microsoft Docs
description: Learn how to configure and use public environments in Azure DevTest Labs.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/13/2018
ms.author: spelluru
ms.openlocfilehash: d93818cd875c4050b1b35f21ce580933776c5bc5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866341"
---
# <a name="configure-and-use-public-environments-in-azure-devtest-labs"></a><span data-ttu-id="18ca5-103">Configure and use public environments in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="18ca5-103">Configure and use public environments in Azure DevTest Labs</span></span>
<span data-ttu-id="18ca5-104">Azure DevTest Labs has a [public repository of Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/Environments) that you can use to create environments without having to connect to an external GitHub source by yourself.</span><span class="sxs-lookup"><span data-stu-id="18ca5-104">Azure DevTest Labs has a [public repository of Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/Environments) that you can use to create environments without having to connect to an external GitHub source by yourself.</span></span> <span data-ttu-id="18ca5-105">This repository includes frequently used templates such as Azure Web Apps, Service Fabric Cluster, and development SharePoint Farm environment.</span><span class="sxs-lookup"><span data-stu-id="18ca5-105">This repository includes frequently used templates such as Azure Web Apps, Service Fabric Cluster, and development SharePoint Farm environment.</span></span> <span data-ttu-id="18ca5-106">This feature is similar to the public repository of artifacts that is included for every lab that you create.</span><span class="sxs-lookup"><span data-stu-id="18ca5-106">This feature is similar to the public repository of artifacts that is included for every lab that you create.</span></span> <span data-ttu-id="18ca5-107">The environment repository allows you to quickly get started with pre-authored environment templates with minimum input parameters to provide you with a smooth getting started experience for PaaS resources within labs.</span><span class="sxs-lookup"><span data-stu-id="18ca5-107">The environment repository allows you to quickly get started with pre-authored environment templates with minimum input parameters to provide you with a smooth getting started experience for PaaS resources within labs.</span></span> 

## <a name="configuring-public-environments"></a><span data-ttu-id="18ca5-108">Configuring public environments</span><span class="sxs-lookup"><span data-stu-id="18ca5-108">Configuring public environments</span></span>
<span data-ttu-id="18ca5-109">As a lab owner, you can enable the public environment repository for your lab during the lab creation.</span><span class="sxs-lookup"><span data-stu-id="18ca5-109">As a lab owner, you can enable the public environment repository for your lab during the lab creation.</span></span> <span data-ttu-id="18ca5-110">To enable public environments for your lab, select **On** for the **Public environments** field while creating a lab.</span><span class="sxs-lookup"><span data-stu-id="18ca5-110">To enable public environments for your lab, select **On** for the **Public environments** field while creating a lab.</span></span> 

![Enable public environment for a new lab](media/devtest-lab-configure-use-public-environments/enable-public-environment-new-lab.png)


<span data-ttu-id="18ca5-112">For existing labs, the public environment repository is not enabled.</span><span class="sxs-lookup"><span data-stu-id="18ca5-112">For existing labs, the public environment repository is not enabled.</span></span> <span data-ttu-id="18ca5-113">Manually enable it to use templates in the repository.</span><span class="sxs-lookup"><span data-stu-id="18ca5-113">Manually enable it to use templates in the repository.</span></span> <span data-ttu-id="18ca5-114">For labs created using Resource Manager templates, the repository is disabled by default as well.</span><span class="sxs-lookup"><span data-stu-id="18ca5-114">For labs created using Resource Manager templates, the repository is disabled by default as well.</span></span>

<span data-ttu-id="18ca5-115">You can enable/disable public environments for your lab, and also make only specific environments available to lab users by using the following steps:</span><span class="sxs-lookup"><span data-stu-id="18ca5-115">You can enable/disable public environments for your lab, and also make only specific environments available to lab users by using the following steps:</span></span> 

1. <span data-ttu-id="18ca5-116">Select **Configuration and policies** for your lab.</span><span class="sxs-lookup"><span data-stu-id="18ca5-116">Select **Configuration and policies** for your lab.</span></span> 
2. <span data-ttu-id="18ca5-117">In the **VIRTUAL MACHINE BASES** section, select **Public environments**.</span><span class="sxs-lookup"><span data-stu-id="18ca5-117">In the **VIRTUAL MACHINE BASES** section, select **Public environments**.</span></span>
3. <span data-ttu-id="18ca5-118">To enable public environments for the lab, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="18ca5-118">To enable public environments for the lab, select **Yes**.</span></span> <span data-ttu-id="18ca5-119">Otherwise, select **No**.</span><span class="sxs-lookup"><span data-stu-id="18ca5-119">Otherwise, select **No**.</span></span> 
4. <span data-ttu-id="18ca5-120">If you enabled public environments, all the environments in the repository are enabled by defaults.</span><span class="sxs-lookup"><span data-stu-id="18ca5-120">If you enabled public environments, all the environments in the repository are enabled by defaults.</span></span> <span data-ttu-id="18ca5-121">You can de-select an environment to make it not available to your lab users.</span><span class="sxs-lookup"><span data-stu-id="18ca5-121">You can de-select an environment to make it not available to your lab users.</span></span> 

![Public environments page](media/devtest-lab-configure-use-public-environments/public-environments-page.png)

## <a name="use-environment-templates-as-a-lab-user"></a><span data-ttu-id="18ca5-123">Use environment templates as a lab user</span><span class="sxs-lookup"><span data-stu-id="18ca5-123">Use environment templates as a lab user</span></span>
<span data-ttu-id="18ca5-124">As a lab user, you can create a new environment from the enabled list of environment templates by simply selecting **+Add** from the tool bar in the lab page.</span><span class="sxs-lookup"><span data-stu-id="18ca5-124">As a lab user, you can create a new environment from the enabled list of environment templates by simply selecting **+Add** from the tool bar in the lab page.</span></span> <span data-ttu-id="18ca5-125">The list of bases includes the public environments templates enabled by your lab admin at the top of the list.</span><span class="sxs-lookup"><span data-stu-id="18ca5-125">The list of bases includes the public environments templates enabled by your lab admin at the top of the list.</span></span>

![Public environment templates](media/devtest-lab-configure-use-public-environments/public-environment-templates.png)

## <a name="next-steps"></a><span data-ttu-id="18ca5-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="18ca5-127">Next steps</span></span>
<span data-ttu-id="18ca5-128">This repository is an open-source repository that you can contribute to add frequently used and helpful Resource Manager templates of your own.</span><span class="sxs-lookup"><span data-stu-id="18ca5-128">This repository is an open-source repository that you can contribute to add frequently used and helpful Resource Manager templates of your own.</span></span> <span data-ttu-id="18ca5-129">To contribute, simply submit a pull request against the repository.</span><span class="sxs-lookup"><span data-stu-id="18ca5-129">To contribute, simply submit a pull request against the repository.</span></span>  
