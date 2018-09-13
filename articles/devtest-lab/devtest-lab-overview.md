---
title: About Azure DevTest Labs | Microsoft Docs
description: Learn how DevTest Labs can make it easy to create, manage, and monitor Azure virtual machines
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: 1b9eed3b-c69a-4c49-a36e-f388efea6f39
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 62e2d214d6d685c7f27c8c45cae161eb25ed1cbd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555792"
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="4125a-103">About Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4125a-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="4125a-104">Overview</span><span class="sxs-lookup"><span data-stu-id="4125a-104">Overview</span></span>
<span data-ttu-id="4125a-105">Developers and testers are looking to solve the delays in creating and managing their environments by going to the cloud.</span><span class="sxs-lookup"><span data-stu-id="4125a-105">Developers and testers are looking to solve the delays in creating and managing their environments by going to the cloud.</span></span>  <span data-ttu-id="4125a-106">Azure solves the problem of environment delays and allows self-service within a new cost efficient structure.</span><span class="sxs-lookup"><span data-stu-id="4125a-106">Azure solves the problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="4125a-107">However, developers and testers still need to spend considerable time configuring their self-served environments.</span><span class="sxs-lookup"><span data-stu-id="4125a-107">However, developers and testers still need to spend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="4125a-108">Also, decision makers are uncertain about how to leverage the cloud to maximize their cost savings without adding too much process overhead.</span><span class="sxs-lookup"><span data-stu-id="4125a-108">Also, decision makers are uncertain about how to leverage the cloud to maximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="4125a-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span><span class="sxs-lookup"><span data-stu-id="4125a-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="4125a-110">You can test the latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span><span class="sxs-lookup"><span data-stu-id="4125a-110">You can test the latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="4125a-111">Easily integrate your deployment pipeline with DevTest Labs to provision on-demand environments.</span><span class="sxs-lookup"><span data-stu-id="4125a-111">Easily integrate your deployment pipeline with DevTest Labs to provision on-demand environments.</span></span> <span data-ttu-id="4125a-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span><span class="sxs-lookup"><span data-stu-id="4125a-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="4125a-113">DevTest Labs provides the following benefits in creating, configuring, and managing developer and test environments in the cloud</span><span class="sxs-lookup"><span data-stu-id="4125a-113">DevTest Labs provides the following benefits in creating, configuring, and managing developer and test environments in the cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="4125a-114">Worry-free self-service</span><span class="sxs-lookup"><span data-stu-id="4125a-114">Worry-free self-service</span></span>
<span data-ttu-id="4125a-115">DevTest Labs makes it easier to control costs by allowing you to set policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span><span class="sxs-lookup"><span data-stu-id="4125a-115">DevTest Labs makes it easier to control costs by allowing you to set policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="4125a-116">DevTest Labs also enables you to create policies to automatically shut down and start VMs.</span><span class="sxs-lookup"><span data-stu-id="4125a-116">DevTest Labs also enables you to create policies to automatically shut down and start VMs.</span></span>

## <a name="quickly-get-to-ready-to-test"></a><span data-ttu-id="4125a-117">Quickly get to ready-to-test</span><span class="sxs-lookup"><span data-stu-id="4125a-117">Quickly get to ready-to-test</span></span>
<span data-ttu-id="4125a-118">DevTest Labs enables you to create pre-provisioned environments with everything your team needs to start developing and testing applications.</span><span class="sxs-lookup"><span data-stu-id="4125a-118">DevTest Labs enables you to create pre-provisioned environments with everything your team needs to start developing and testing applications.</span></span> <span data-ttu-id="4125a-119">Simply claim the environments where the last good build of your application is installed and get working right away.</span><span class="sxs-lookup"><span data-stu-id="4125a-119">Simply claim the environments where the last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="4125a-120">Or, use containers for even faster and leaner environment creation.</span><span class="sxs-lookup"><span data-stu-id="4125a-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="4125a-121">Create once, use everywhere</span><span class="sxs-lookup"><span data-stu-id="4125a-121">Create once, use everywhere</span></span>
<span data-ttu-id="4125a-122">Capture and share environment templates and artifacts within your team or organization - all in source control - to create developer and test environments easily.</span><span class="sxs-lookup"><span data-stu-id="4125a-122">Capture and share environment templates and artifacts within your team or organization - all in source control - to create developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="4125a-123">Integrates with your existing toolchain</span><span class="sxs-lookup"><span data-stu-id="4125a-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="4125a-124">Leverage pre-made plug-ins or our API to provision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span><span class="sxs-lookup"><span data-stu-id="4125a-124">Leverage pre-made plug-ins or our API to provision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="4125a-125">You can also use our comprehensive command-line tool.</span><span class="sxs-lookup"><span data-stu-id="4125a-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="4125a-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="4125a-126">Next steps</span></span>
[<span data-ttu-id="4125a-127">DevTest Labs concepts</span><span class="sxs-lookup"><span data-stu-id="4125a-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)

