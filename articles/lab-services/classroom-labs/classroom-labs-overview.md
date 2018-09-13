---
title: About Azure Lab Services | Microsoft Docs
description: Learn how Lab Services can make it easy to create, manage, and secure labs with virtual machines that can be used by developers, testers, educators, students, and others.
services: lab-services
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 05/21/2018
ms.author: spelluru
ms.openlocfilehash: e9c3cae7c7129cc489ddd38b5b2de18dd6f52e58
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871665"
---
# <a name="introduction-to-classroom-labs"></a><span data-ttu-id="10ae1-103">Introduction to classroom labs</span><span class="sxs-lookup"><span data-stu-id="10ae1-103">Introduction to classroom labs</span></span>
<span data-ttu-id="10ae1-104">Azure Lab Services enables you to quickly set up a classroom lab environment in the cloud.</span><span class="sxs-lookup"><span data-stu-id="10ae1-104">Azure Lab Services enables you to quickly set up a classroom lab environment in the cloud.</span></span> <span data-ttu-id="10ae1-105">An educator creates a classroom lab, provisions Windows, or Linux virtual machines, installs the necessary software and tools labs in the class, and makes them available to students.</span><span class="sxs-lookup"><span data-stu-id="10ae1-105">An educator creates a classroom lab, provisions Windows, or Linux virtual machines, installs the necessary software and tools labs in the class, and makes them available to students.</span></span> <span data-ttu-id="10ae1-106">The students in the class connect to virtual machines (VMs) in the lab, and use them for their projects, assignments, classroom exercises.</span><span class="sxs-lookup"><span data-stu-id="10ae1-106">The students in the class connect to virtual machines (VMs) in the lab, and use them for their projects, assignments, classroom exercises.</span></span> 

<span data-ttu-id="10ae1-107">The classroom labs are managed labs that are managed by Azure.</span><span class="sxs-lookup"><span data-stu-id="10ae1-107">The classroom labs are managed labs that are managed by Azure.</span></span> <span data-ttu-id="10ae1-108">The service itself handles all the infrastructure management for a managed lab, from spinning up virtual machines (VMs) to handling errors, and scaling the infrastructure.</span><span class="sxs-lookup"><span data-stu-id="10ae1-108">The service itself handles all the infrastructure management for a managed lab, from spinning up virtual machines (VMs) to handling errors, and scaling the infrastructure.</span></span> <span data-ttu-id="10ae1-109">You specify what kind of infrastructure you need and install any tools or software that's required for the class.</span><span class="sxs-lookup"><span data-stu-id="10ae1-109">You specify what kind of infrastructure you need and install any tools or software that's required for the class.</span></span> <span data-ttu-id="10ae1-110">The managed labs are currently in preview.</span><span class="sxs-lookup"><span data-stu-id="10ae1-110">The managed labs are currently in preview.</span></span>  

## <a name="scenarios"></a><span data-ttu-id="10ae1-111">Scenarios</span><span class="sxs-lookup"><span data-stu-id="10ae1-111">Scenarios</span></span>
<span data-ttu-id="10ae1-112">Here is the main scenario that classroom labs of Azure Lab Services support:</span><span class="sxs-lookup"><span data-stu-id="10ae1-112">Here is the main scenario that classroom labs of Azure Lab Services support:</span></span> 

### <a name="set-up-a-resizable-computer-lab-in-the-cloud-for-your-classroom"></a><span data-ttu-id="10ae1-113">Set up a resizable computer lab in the cloud for your classroom</span><span class="sxs-lookup"><span data-stu-id="10ae1-113">Set up a resizable computer lab in the cloud for your classroom</span></span>  

- <span data-ttu-id="10ae1-114">Create a managed classroom lab.</span><span class="sxs-lookup"><span data-stu-id="10ae1-114">Create a managed classroom lab.</span></span> <span data-ttu-id="10ae1-115">You just tell the service exactly what you need, and it creates and manages the infrastructure of the lab for you so that you can focus on teaching your class, not technical details of a lab.</span><span class="sxs-lookup"><span data-stu-id="10ae1-115">You just tell the service exactly what you need, and it creates and manages the infrastructure of the lab for you so that you can focus on teaching your class, not technical details of a lab.</span></span> 
- <span data-ttu-id="10ae1-116">Provide students with a lab of virtual machines that are configured with exactly what’s needed for a class.</span><span class="sxs-lookup"><span data-stu-id="10ae1-116">Provide students with a lab of virtual machines that are configured with exactly what’s needed for a class.</span></span> <span data-ttu-id="10ae1-117">Give each student a limited number of hours for using the VMs for class work.</span><span class="sxs-lookup"><span data-stu-id="10ae1-117">Give each student a limited number of hours for using the VMs for class work.</span></span>  
- <span data-ttu-id="10ae1-118">Move your school’s physical computer lab into the cloud.</span><span class="sxs-lookup"><span data-stu-id="10ae1-118">Move your school’s physical computer lab into the cloud.</span></span> <span data-ttu-id="10ae1-119">Automatically scale the number of VMs only to the maximum usage and cost threshold that you set on the lab.</span><span class="sxs-lookup"><span data-stu-id="10ae1-119">Automatically scale the number of VMs only to the maximum usage and cost threshold that you set on the lab.</span></span> 
- <span data-ttu-id="10ae1-120">Delete the lab with a single click once you’re done.</span><span class="sxs-lookup"><span data-stu-id="10ae1-120">Delete the lab with a single click once you’re done.</span></span> 

## <a name="user-profiles"></a><span data-ttu-id="10ae1-121">User profiles</span><span class="sxs-lookup"><span data-stu-id="10ae1-121">User profiles</span></span>
<span data-ttu-id="10ae1-122">This article describes different user profiles in Azure Lab Services.</span><span class="sxs-lookup"><span data-stu-id="10ae1-122">This article describes different user profiles in Azure Lab Services.</span></span> 

### <a name="lab-account-owner"></a><span data-ttu-id="10ae1-123">Lab account owner</span><span class="sxs-lookup"><span data-stu-id="10ae1-123">Lab account owner</span></span>
<span data-ttu-id="10ae1-124">Typically, and IT administrator of organization's cloud resources, who owns the Azure subscription acts as a lab account owner and does the following tasks:</span><span class="sxs-lookup"><span data-stu-id="10ae1-124">Typically, and IT administrator of organization's cloud resources, who owns the Azure subscription acts as a lab account owner and does the following tasks:</span></span>   

- <span data-ttu-id="10ae1-125">Sets up a lab account for your organization.</span><span class="sxs-lookup"><span data-stu-id="10ae1-125">Sets up a lab account for your organization.</span></span>
- <span data-ttu-id="10ae1-126">Manages and configures policies across all labs.</span><span class="sxs-lookup"><span data-stu-id="10ae1-126">Manages and configures policies across all labs.</span></span>
- <span data-ttu-id="10ae1-127">Gives permissions to people in the organization to create a lab under the lab account.</span><span class="sxs-lookup"><span data-stu-id="10ae1-127">Gives permissions to people in the organization to create a lab under the lab account.</span></span>

### <a name="educator"></a><span data-ttu-id="10ae1-128">Educator</span><span class="sxs-lookup"><span data-stu-id="10ae1-128">Educator</span></span>
<span data-ttu-id="10ae1-129">Typically, users such as a teacher or an online trainer creates classroom labs under a lab account.</span><span class="sxs-lookup"><span data-stu-id="10ae1-129">Typically, users such as a teacher or an online trainer creates classroom labs under a lab account.</span></span> <span data-ttu-id="10ae1-130">An educator does the following tasks:</span><span class="sxs-lookup"><span data-stu-id="10ae1-130">An educator does the following tasks:</span></span> 

- <span data-ttu-id="10ae1-131">Creates a classroom lab.</span><span class="sxs-lookup"><span data-stu-id="10ae1-131">Creates a classroom lab.</span></span>
- <span data-ttu-id="10ae1-132">Creates virtual machines in the lab.</span><span class="sxs-lookup"><span data-stu-id="10ae1-132">Creates virtual machines in the lab.</span></span> 
- <span data-ttu-id="10ae1-133">Installs the appropriate software on virtual machines.</span><span class="sxs-lookup"><span data-stu-id="10ae1-133">Installs the appropriate software on virtual machines.</span></span>
- <span data-ttu-id="10ae1-134">Specifies who can access the lab.</span><span class="sxs-lookup"><span data-stu-id="10ae1-134">Specifies who can access the lab.</span></span>
- <span data-ttu-id="10ae1-135">Provides registration link to the lab to students.</span><span class="sxs-lookup"><span data-stu-id="10ae1-135">Provides registration link to the lab to students.</span></span>

### <a name="student"></a><span data-ttu-id="10ae1-136">Student</span><span class="sxs-lookup"><span data-stu-id="10ae1-136">Student</span></span>
<span data-ttu-id="10ae1-137">A student does the following tasks:</span><span class="sxs-lookup"><span data-stu-id="10ae1-137">A student does the following tasks:</span></span>

- <span data-ttu-id="10ae1-138">Uses the registration link that the lab user receives from a lab creator to register with the lab.</span><span class="sxs-lookup"><span data-stu-id="10ae1-138">Uses the registration link that the lab user receives from a lab creator to register with the lab.</span></span> 
- <span data-ttu-id="10ae1-139">Connects to a virtual machine in the lab and use it for doing class work, assignments, and projects.</span><span class="sxs-lookup"><span data-stu-id="10ae1-139">Connects to a virtual machine in the lab and use it for doing class work, assignments, and projects.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="10ae1-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="10ae1-140">Next steps</span></span>
<span data-ttu-id="10ae1-141">Get started with setting up a lab account that's required to create a classroom lab using Azure Lab Services:</span><span class="sxs-lookup"><span data-stu-id="10ae1-141">Get started with setting up a lab account that's required to create a classroom lab using Azure Lab Services:</span></span>

- [<span data-ttu-id="10ae1-142">Set up a lab account</span><span class="sxs-lookup"><span data-stu-id="10ae1-142">Set up a lab account</span></span>](tutorial-setup-lab-account.md)
