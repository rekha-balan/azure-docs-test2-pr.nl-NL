---
title: Set up a classroom lab using Azure Lab Services | Microsoft Docs
description: In this tutorial, you set up a lab to use in a classroom.
services: devtest-lab, lab-services, virtual-machines
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.custom: mvc
ms.date: 07/23/2018
ms.author: spelluru
ms.openlocfilehash: fe41728b6f08ba767dbcb40d0595b9f7cdc79615
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865500"
---
# <a name="tutorial-set-up-a-classroom-lab"></a><span data-ttu-id="c7c47-103">Tutorial: Set up a classroom lab</span><span class="sxs-lookup"><span data-stu-id="c7c47-103">Tutorial: Set up a classroom lab</span></span> 
<span data-ttu-id="c7c47-104">In this tutorial, you set up a classroom lab with virtual machines that are used by students in the classroom.</span><span class="sxs-lookup"><span data-stu-id="c7c47-104">In this tutorial, you set up a classroom lab with virtual machines that are used by students in the classroom.</span></span>  

<span data-ttu-id="c7c47-105">In this tutorial, you do the following actions:</span><span class="sxs-lookup"><span data-stu-id="c7c47-105">In this tutorial, you do the following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c7c47-106">Create a classroom lab</span><span class="sxs-lookup"><span data-stu-id="c7c47-106">Create a classroom lab</span></span>
> * <span data-ttu-id="c7c47-107">Configure the classroom lab</span><span class="sxs-lookup"><span data-stu-id="c7c47-107">Configure the classroom lab</span></span>
> * <span data-ttu-id="c7c47-108">Send registration link to students</span><span class="sxs-lookup"><span data-stu-id="c7c47-108">Send registration link to students</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7c47-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c7c47-109">Prerequisites</span></span>
<span data-ttu-id="c7c47-110">To set up a classroom lab in a lab account, you must be a member of the **Lab Creator** role in the lab account.</span><span class="sxs-lookup"><span data-stu-id="c7c47-110">To set up a classroom lab in a lab account, you must be a member of the **Lab Creator** role in the lab account.</span></span> <span data-ttu-id="c7c47-111">The account you used to create a lab account is automatically added to this role.</span><span class="sxs-lookup"><span data-stu-id="c7c47-111">The account you used to create a lab account is automatically added to this role.</span></span> <span data-ttu-id="c7c47-112">A lab owner can add other users to the Lab Creator role by using steps in the following article: [Add a user to the Lab Creator role](tutorial-setup-lab-account.md#add-a-user-to-the-lab-creator-role).</span><span class="sxs-lookup"><span data-stu-id="c7c47-112">A lab owner can add other users to the Lab Creator role by using steps in the following article: [Add a user to the Lab Creator role](tutorial-setup-lab-account.md#add-a-user-to-the-lab-creator-role).</span></span>


## <a name="create-a-classroom-lab"></a><span data-ttu-id="c7c47-113">Create a classroom lab</span><span class="sxs-lookup"><span data-stu-id="c7c47-113">Create a classroom lab</span></span>

1. <span data-ttu-id="c7c47-114">Navigate to [Azure Lab Services website](https://labs.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c7c47-114">Navigate to [Azure Lab Services website](https://labs.azure.com).</span></span> 
2. <span data-ttu-id="c7c47-115">Select **Sign in** and enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="c7c47-115">Select **Sign in** and enter your credentials.</span></span> <span data-ttu-id="c7c47-116">Azure Lab Services supports organizational accounts and Microsoft accounts.</span><span class="sxs-lookup"><span data-stu-id="c7c47-116">Azure Lab Services supports organizational accounts and Microsoft accounts.</span></span> 
3. <span data-ttu-id="c7c47-117">In the **New Lab** window, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="c7c47-117">In the **New Lab** window, do the following actions:</span></span> 
    1. <span data-ttu-id="c7c47-118">Specify a **name** for the classroom lab.</span><span class="sxs-lookup"><span data-stu-id="c7c47-118">Specify a **name** for the classroom lab.</span></span> 
    2. <span data-ttu-id="c7c47-119">Select the **size** of the virtual machine that you plan to use in the classroom.</span><span class="sxs-lookup"><span data-stu-id="c7c47-119">Select the **size** of the virtual machine that you plan to use in the classroom.</span></span>
    3. <span data-ttu-id="c7c47-120">Select the **image** to use to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c7c47-120">Select the **image** to use to create the virtual machine.</span></span>
    4. <span data-ttu-id="c7c47-121">Specify **default credentials** for logging into virtual machines in the lab.</span><span class="sxs-lookup"><span data-stu-id="c7c47-121">Specify **default credentials** for logging into virtual machines in the lab.</span></span> 
    7. <span data-ttu-id="c7c47-122">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="c7c47-122">Select **Save**.</span></span>

        ![Create a classroom lab](../media/tutorial-setup-classroom-lab/new-lab-window.png)
1. <span data-ttu-id="c7c47-124">Once the lab is created, select **Go to my lab**.</span><span class="sxs-lookup"><span data-stu-id="c7c47-124">Once the lab is created, select **Go to my lab**.</span></span> 

    ![Go to my lab](../media/tutorial-setup-classroom-lab/go-to-my-lab.png)
1. <span data-ttu-id="c7c47-126">You see the **dashboard** for the lab.</span><span class="sxs-lookup"><span data-stu-id="c7c47-126">You see the **dashboard** for the lab.</span></span> 
    
    ![Classroom lab dashboard](../media/tutorial-setup-classroom-lab/classroom-lab-home-page.png)

## <a name="configure-usage-policy"></a><span data-ttu-id="c7c47-128">Configure usage policy</span><span class="sxs-lookup"><span data-stu-id="c7c47-128">Configure usage policy</span></span>

1. <span data-ttu-id="c7c47-129">Select **Usage policy**.</span><span class="sxs-lookup"><span data-stu-id="c7c47-129">Select **Usage policy**.</span></span> 
2. <span data-ttu-id="c7c47-130">In the **Usage policy**, settings, enter the **number of users** allowed to use the lab.</span><span class="sxs-lookup"><span data-stu-id="c7c47-130">In the **Usage policy**, settings, enter the **number of users** allowed to use the lab.</span></span>
3. <span data-ttu-id="c7c47-131">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="c7c47-131">Select **Save**.</span></span> 

    ![Usage policy](../media/tutorial-setup-classroom-lab/usage-policy-settings.png)


## <a name="set-up-the-template"></a><span data-ttu-id="c7c47-133">Set up the template</span><span class="sxs-lookup"><span data-stu-id="c7c47-133">Set up the template</span></span> 
<span data-ttu-id="c7c47-134">A template in a lab is a base virtual machine image from which all users’ virtual machines are created.</span><span class="sxs-lookup"><span data-stu-id="c7c47-134">A template in a lab is a base virtual machine image from which all users’ virtual machines are created.</span></span> <span data-ttu-id="c7c47-135">Set up the template virtual machine so that it is configured with exactly what you want to provide to the lab users.</span><span class="sxs-lookup"><span data-stu-id="c7c47-135">Set up the template virtual machine so that it is configured with exactly what you want to provide to the lab users.</span></span> <span data-ttu-id="c7c47-136">You can provide a name and description of the template that the lab users see.</span><span class="sxs-lookup"><span data-stu-id="c7c47-136">You can provide a name and description of the template that the lab users see.</span></span> <span data-ttu-id="c7c47-137">Publish the template to make instances of the template VM available to your lab users.</span><span class="sxs-lookup"><span data-stu-id="c7c47-137">Publish the template to make instances of the template VM available to your lab users.</span></span> 

### <a name="set-title-and-description"></a><span data-ttu-id="c7c47-138">Set title and description</span><span class="sxs-lookup"><span data-stu-id="c7c47-138">Set title and description</span></span>
1. <span data-ttu-id="c7c47-139">In the **Template** section, select **Edit** (pencil icon) for the template.</span><span class="sxs-lookup"><span data-stu-id="c7c47-139">In the **Template** section, select **Edit** (pencil icon) for the template.</span></span> 
2. <span data-ttu-id="c7c47-140">In the **User view** window, Enter a **title** for the template.</span><span class="sxs-lookup"><span data-stu-id="c7c47-140">In the **User view** window, Enter a **title** for the template.</span></span>
3. <span data-ttu-id="c7c47-141">Enter **description** for the template.</span><span class="sxs-lookup"><span data-stu-id="c7c47-141">Enter **description** for the template.</span></span>
4. <span data-ttu-id="c7c47-142">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="c7c47-142">Select **Save**.</span></span>

    ![Classroom lab description](../media/tutorial-setup-classroom-lab/lab-description.png)

### <a name="set-up-the-template-vm"></a><span data-ttu-id="c7c47-144">Set up the template VM</span><span class="sxs-lookup"><span data-stu-id="c7c47-144">Set up the template VM</span></span>
 <span data-ttu-id="c7c47-145">You connect to the template VM and install any required software on it before making it available to your students.</span><span class="sxs-lookup"><span data-stu-id="c7c47-145">You connect to the template VM and install any required software on it before making it available to your students.</span></span> 

1. <span data-ttu-id="c7c47-146">Wait until the template virtual machine is ready.</span><span class="sxs-lookup"><span data-stu-id="c7c47-146">Wait until the template virtual machine is ready.</span></span> <span data-ttu-id="c7c47-147">Once it is ready, the **Start** button should be enabled.</span><span class="sxs-lookup"><span data-stu-id="c7c47-147">Once it is ready, the **Start** button should be enabled.</span></span> <span data-ttu-id="c7c47-148">To start the VM, select **Start**.</span><span class="sxs-lookup"><span data-stu-id="c7c47-148">To start the VM, select **Start**.</span></span>

    ![Start the template VM](../media/tutorial-setup-classroom-lab/start-template-vm.png)
1. <span data-ttu-id="c7c47-150">To connect to the VM, select **Connect**, and follow instructions.</span><span class="sxs-lookup"><span data-stu-id="c7c47-150">To connect to the VM, select **Connect**, and follow instructions.</span></span> 

    ![Connect to the template VM](../media/tutorial-setup-classroom-lab/connect-template-vm.png)
1. <span data-ttu-id="c7c47-152">Install any software that's required for students to do the lab (for example, Visual Studio, Azure Storage Explorer, etc.).</span><span class="sxs-lookup"><span data-stu-id="c7c47-152">Install any software that's required for students to do the lab (for example, Visual Studio, Azure Storage Explorer, etc.).</span></span> 
2. <span data-ttu-id="c7c47-153">Disconnect (close your remote desktop session) from the template VM.</span><span class="sxs-lookup"><span data-stu-id="c7c47-153">Disconnect (close your remote desktop session) from the template VM.</span></span> 
3. <span data-ttu-id="c7c47-154">**Stop** the template VM by selecting **Stop**.</span><span class="sxs-lookup"><span data-stu-id="c7c47-154">**Stop** the template VM by selecting **Stop**.</span></span> 

    ![Stop the template VM](../media/tutorial-setup-classroom-lab/stop-template-vm.png)

### <a name="publish-the-template"></a><span data-ttu-id="c7c47-156">Publish the template</span><span class="sxs-lookup"><span data-stu-id="c7c47-156">Publish the template</span></span> 
<span data-ttu-id="c7c47-157">When you publish a template, Azure Lab Services creates VMs in the lab by using the template.</span><span class="sxs-lookup"><span data-stu-id="c7c47-157">When you publish a template, Azure Lab Services creates VMs in the lab by using the template.</span></span> <span data-ttu-id="c7c47-158">The number of VMs created in this process is same as the maximum number of users allowed into the lab, which you can set in the usage policy of the lab.</span><span class="sxs-lookup"><span data-stu-id="c7c47-158">The number of VMs created in this process is same as the maximum number of users allowed into the lab, which you can set in the usage policy of the lab.</span></span> <span data-ttu-id="c7c47-159">All virtual machines have the same configuration as the template.</span><span class="sxs-lookup"><span data-stu-id="c7c47-159">All virtual machines have the same configuration as the template.</span></span> 

1. <span data-ttu-id="c7c47-160">Select **Publish** in the **Template** section.</span><span class="sxs-lookup"><span data-stu-id="c7c47-160">Select **Publish** in the **Template** section.</span></span> 

    ![Publish the template VM](../media/tutorial-setup-classroom-lab/public-access.png)
1. <span data-ttu-id="c7c47-162">In the **Publish** window, select the **Published** option.</span><span class="sxs-lookup"><span data-stu-id="c7c47-162">In the **Publish** window, select the **Published** option.</span></span> 
2. <span data-ttu-id="c7c47-163">Now, select the **Publish** button.</span><span class="sxs-lookup"><span data-stu-id="c7c47-163">Now, select the **Publish** button.</span></span> <span data-ttu-id="c7c47-164">This process may take some time depending on how many VMs are being created, which is same as the number of users allowed into the lab.</span><span class="sxs-lookup"><span data-stu-id="c7c47-164">This process may take some time depending on how many VMs are being created, which is same as the number of users allowed into the lab.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="c7c47-165">Once a template is published, it can't be unpublished.</span><span class="sxs-lookup"><span data-stu-id="c7c47-165">Once a template is published, it can't be unpublished.</span></span> 
4. <span data-ttu-id="c7c47-166">Switch to the **Virtual machines** page, and confirm that you see virtual machines that are in **Unassigned** state.</span><span class="sxs-lookup"><span data-stu-id="c7c47-166">Switch to the **Virtual machines** page, and confirm that you see virtual machines that are in **Unassigned** state.</span></span> <span data-ttu-id="c7c47-167">These VMs are not assigned to students yet.</span><span class="sxs-lookup"><span data-stu-id="c7c47-167">These VMs are not assigned to students yet.</span></span> 

    ![Virtual machines](../media/tutorial-setup-classroom-lab/virtual-machines.png)
5. <span data-ttu-id="c7c47-169">Wait until the VMs are created.</span><span class="sxs-lookup"><span data-stu-id="c7c47-169">Wait until the VMs are created.</span></span> <span data-ttu-id="c7c47-170">They should be in **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="c7c47-170">They should be in **Stopped** state.</span></span> <span data-ttu-id="c7c47-171">You can start a student VM, connect to the VM, stop the VM, and delete the VM on this page.</span><span class="sxs-lookup"><span data-stu-id="c7c47-171">You can start a student VM, connect to the VM, stop the VM, and delete the VM on this page.</span></span> <span data-ttu-id="c7c47-172">You can start them in this page or let your students start the VMs.</span><span class="sxs-lookup"><span data-stu-id="c7c47-172">You can start them in this page or let your students start the VMs.</span></span> 

    ![Virtual machines in stopped state](../media/tutorial-setup-classroom-lab/virtual-machines-stopped.png)

## <a name="send-registration-link-to-students"></a><span data-ttu-id="c7c47-174">Send registration link to students</span><span class="sxs-lookup"><span data-stu-id="c7c47-174">Send registration link to students</span></span>

1. <span data-ttu-id="c7c47-175">Switch to the **Dashboard** view.</span><span class="sxs-lookup"><span data-stu-id="c7c47-175">Switch to the **Dashboard** view.</span></span> 
2. <span data-ttu-id="c7c47-176">Select **User registration** tile.</span><span class="sxs-lookup"><span data-stu-id="c7c47-176">Select **User registration** tile.</span></span>

    ![Student registration link](../media/tutorial-setup-classroom-lab/dashboard-user-registration-link.png)
1. <span data-ttu-id="c7c47-178">In the **User registration** dialog box, select the **Copy** button.</span><span class="sxs-lookup"><span data-stu-id="c7c47-178">In the **User registration** dialog box, select the **Copy** button.</span></span> <span data-ttu-id="c7c47-179">The link is copied to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="c7c47-179">The link is copied to the clipboard.</span></span> <span data-ttu-id="c7c47-180">Paste it in an email editor, and send an email to the student.</span><span class="sxs-lookup"><span data-stu-id="c7c47-180">Paste it in an email editor, and send an email to the student.</span></span> 

    ![Student registration link](../media/tutorial-setup-classroom-lab/registration-link.png)
2. <span data-ttu-id="c7c47-182">On the **User registration** dialog box, select **Close**.</span><span class="sxs-lookup"><span data-stu-id="c7c47-182">On the **User registration** dialog box, select **Close**.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="c7c47-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7c47-183">Next steps</span></span>
<span data-ttu-id="c7c47-184">In this tutorial, you created a classroom lab, and configured the lab.</span><span class="sxs-lookup"><span data-stu-id="c7c47-184">In this tutorial, you created a classroom lab, and configured the lab.</span></span> <span data-ttu-id="c7c47-185">To learn how a student can access a VM in the lab using the registration link, advance to the next tutorial:</span><span class="sxs-lookup"><span data-stu-id="c7c47-185">To learn how a student can access a VM in the lab using the registration link, advance to the next tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7c47-186">Connect to a VM in the classroom lab</span><span class="sxs-lookup"><span data-stu-id="c7c47-186">Connect to a VM in the classroom lab</span></span>](tutorial-connect-virtual-machine-classroom-lab.md)

