---
title: Manage classroom labs in Azure Lab Services | Microsoft Docs
description: Learn how to create and configure a classroom lab, view all the classroom labs, shre the registration link with a lab user, or delete a lab.
services: lab-services
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2018
ms.author: spelluru
ms.openlocfilehash: 48056d6e2988dd674351aca83526032175c355b6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864541"
---
# <a name="manage-classroom-labs-in-azure-lab-services"></a><span data-ttu-id="ff28a-103">Manage classroom labs in Azure Lab Services</span><span class="sxs-lookup"><span data-stu-id="ff28a-103">Manage classroom labs in Azure Lab Services</span></span> 
<span data-ttu-id="ff28a-104">This article describes how to create and configure a classroom lab, view all classroom labs, or delete a classroom lab.</span><span class="sxs-lookup"><span data-stu-id="ff28a-104">This article describes how to create and configure a classroom lab, view all classroom labs, or delete a classroom lab.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff28a-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ff28a-105">Prerequisites</span></span>
<span data-ttu-id="ff28a-106">To set up a classroom lab in a lab account, you must be a member of the **Lab Creator** role in the lab account.</span><span class="sxs-lookup"><span data-stu-id="ff28a-106">To set up a classroom lab in a lab account, you must be a member of the **Lab Creator** role in the lab account.</span></span> <span data-ttu-id="ff28a-107">The account you used to create a lab account is automatically added to this role.</span><span class="sxs-lookup"><span data-stu-id="ff28a-107">The account you used to create a lab account is automatically added to this role.</span></span> <span data-ttu-id="ff28a-108">A lab owner can add other users to the Lab Creator role by using steps in the following article: [Add a user to the Lab Creator role](tutorial-setup-lab-account.md#add-a-user-to-the-lab-creator-role).</span><span class="sxs-lookup"><span data-stu-id="ff28a-108">A lab owner can add other users to the Lab Creator role by using steps in the following article: [Add a user to the Lab Creator role](tutorial-setup-lab-account.md#add-a-user-to-the-lab-creator-role).</span></span>

## <a name="create-a-classroom-lab"></a><span data-ttu-id="ff28a-109">Create a classroom lab</span><span class="sxs-lookup"><span data-stu-id="ff28a-109">Create a classroom lab</span></span>

1. <span data-ttu-id="ff28a-110">Navigate to [Azure Lab Services website](https://labs.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff28a-110">Navigate to [Azure Lab Services website](https://labs.azure.com).</span></span>
2. <span data-ttu-id="ff28a-111">Select **Sign in** and enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="ff28a-111">Select **Sign in** and enter your credentials.</span></span> <span data-ttu-id="ff28a-112">Azure Lab Services supports organizational accounts and Microsoft accounts.</span><span class="sxs-lookup"><span data-stu-id="ff28a-112">Azure Lab Services supports organizational accounts and Microsoft accounts.</span></span>
3. <span data-ttu-id="ff28a-113">In the **New Lab** window, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="ff28a-113">In the **New Lab** window, do the following actions:</span></span> 
    1. <span data-ttu-id="ff28a-114">Specify a **name** for the classroom lab.</span><span class="sxs-lookup"><span data-stu-id="ff28a-114">Specify a **name** for the classroom lab.</span></span> 
    2. <span data-ttu-id="ff28a-115">Select the **size** of the virtual machine that you plan to use in the classroom.</span><span class="sxs-lookup"><span data-stu-id="ff28a-115">Select the **size** of the virtual machine that you plan to use in the classroom.</span></span>
    3. <span data-ttu-id="ff28a-116">Select the **image** to use to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ff28a-116">Select the **image** to use to create the virtual machine.</span></span>
    4. <span data-ttu-id="ff28a-117">Specify the **default credentials** to use for logging into the virtual machines in the lab.</span><span class="sxs-lookup"><span data-stu-id="ff28a-117">Specify the **default credentials** to use for logging into the virtual machines in the lab.</span></span>
    7. <span data-ttu-id="ff28a-118">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="ff28a-118">Select **Save**.</span></span>

        ![Create a classroom lab](../media/how-to-manage-classroom-labs/new-lab-window.png)
1. <span data-ttu-id="ff28a-120">You see the **dashboard** for the lab.</span><span class="sxs-lookup"><span data-stu-id="ff28a-120">You see the **dashboard** for the lab.</span></span> 
    
    ![Classroom lab dashboard](../media/how-to-manage-classroom-labs/classroom-lab-home-page.png)

## <a name="configure-usage-policy"></a><span data-ttu-id="ff28a-122">Configure usage policy</span><span class="sxs-lookup"><span data-stu-id="ff28a-122">Configure usage policy</span></span>

1. <span data-ttu-id="ff28a-123">Select **Usage policy**.</span><span class="sxs-lookup"><span data-stu-id="ff28a-123">Select **Usage policy**.</span></span> 
2. <span data-ttu-id="ff28a-124">In the **Usage policy**, settings, enter the **number of users** allowed to use the lab.</span><span class="sxs-lookup"><span data-stu-id="ff28a-124">In the **Usage policy**, settings, enter the **number of users** allowed to use the lab.</span></span>
3. <span data-ttu-id="ff28a-125">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="ff28a-125">Select **Save**.</span></span> 

    ![Usage policy](../media/how-to-manage-classroom-labs/usage-policy-settings.png)

## <a name="set-up-the-template"></a><span data-ttu-id="ff28a-127">Set up the template</span><span class="sxs-lookup"><span data-stu-id="ff28a-127">Set up the template</span></span>
<span data-ttu-id="ff28a-128">A template in a lab is a base virtual machine image from which all users’ virtual machines are created.</span><span class="sxs-lookup"><span data-stu-id="ff28a-128">A template in a lab is a base virtual machine image from which all users’ virtual machines are created.</span></span> <span data-ttu-id="ff28a-129">Set up the template virtual machine so that it is configured with exactly what you want to provide to the lab users.</span><span class="sxs-lookup"><span data-stu-id="ff28a-129">Set up the template virtual machine so that it is configured with exactly what you want to provide to the lab users.</span></span> <span data-ttu-id="ff28a-130">You can provide a name and description of the template that the lab users see.</span><span class="sxs-lookup"><span data-stu-id="ff28a-130">You can provide a name and description of the template that the lab users see.</span></span> <span data-ttu-id="ff28a-131">Publish the template to make instances of the template VM available to your lab users.</span><span class="sxs-lookup"><span data-stu-id="ff28a-131">Publish the template to make instances of the template VM available to your lab users.</span></span>  

### <a name="set-template-title-and-description"></a><span data-ttu-id="ff28a-132">Set template title and description</span><span class="sxs-lookup"><span data-stu-id="ff28a-132">Set template title and description</span></span>
1. <span data-ttu-id="ff28a-133">In the **Template** section, select **Edit** (pencil icon) for the template.</span><span class="sxs-lookup"><span data-stu-id="ff28a-133">In the **Template** section, select **Edit** (pencil icon) for the template.</span></span> 
2. <span data-ttu-id="ff28a-134">In the **User view** window, Enter a **title** for the template.</span><span class="sxs-lookup"><span data-stu-id="ff28a-134">In the **User view** window, Enter a **title** for the template.</span></span>
3. <span data-ttu-id="ff28a-135">Enter **description** for the template.</span><span class="sxs-lookup"><span data-stu-id="ff28a-135">Enter **description** for the template.</span></span>
4. <span data-ttu-id="ff28a-136">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="ff28a-136">Select **Save**.</span></span>

    ![Classroom lab description](../media/how-to-manage-classroom-labs/lab-description.png)

### <a name="set-up-the-template-vm"></a><span data-ttu-id="ff28a-138">Set up the template VM</span><span class="sxs-lookup"><span data-stu-id="ff28a-138">Set up the template VM</span></span>
 <span data-ttu-id="ff28a-139">You connect to the template VM and install any required software on it before making it available to your students.</span><span class="sxs-lookup"><span data-stu-id="ff28a-139">You connect to the template VM and install any required software on it before making it available to your students.</span></span> 

1. <span data-ttu-id="ff28a-140">Wait until the template virtual machine is ready.</span><span class="sxs-lookup"><span data-stu-id="ff28a-140">Wait until the template virtual machine is ready.</span></span> <span data-ttu-id="ff28a-141">Once it is ready, the **Start** button should be enabled.</span><span class="sxs-lookup"><span data-stu-id="ff28a-141">Once it is ready, the **Start** button should be enabled.</span></span> <span data-ttu-id="ff28a-142">To start the VM, select **Start**.</span><span class="sxs-lookup"><span data-stu-id="ff28a-142">To start the VM, select **Start**.</span></span>

    ![Start the template VM](../media/tutorial-setup-classroom-lab/start-template-vm.png)
1. <span data-ttu-id="ff28a-144">To connect to the VM, select **Connect**, and follow instructions.</span><span class="sxs-lookup"><span data-stu-id="ff28a-144">To connect to the VM, select **Connect**, and follow instructions.</span></span> 

    ![Connect to the template VM](../media/tutorial-setup-classroom-lab/connect-template-vm.png)
1. <span data-ttu-id="ff28a-146">Install any software that's required for students to do the lab (for example, Visual Studio, Azure Storage Explorer, etc.).</span><span class="sxs-lookup"><span data-stu-id="ff28a-146">Install any software that's required for students to do the lab (for example, Visual Studio, Azure Storage Explorer, etc.).</span></span> 
2. <span data-ttu-id="ff28a-147">Disconnect (close your remote desktop session) from the template VM.</span><span class="sxs-lookup"><span data-stu-id="ff28a-147">Disconnect (close your remote desktop session) from the template VM.</span></span> 
3. <span data-ttu-id="ff28a-148">**Stop** the template VM by selecting **Stop**.</span><span class="sxs-lookup"><span data-stu-id="ff28a-148">**Stop** the template VM by selecting **Stop**.</span></span> 

    ![Stop the template VM](../media/tutorial-setup-classroom-lab/stop-template-vm.png)


### <a name="publish-the-template"></a><span data-ttu-id="ff28a-150">Publish the template</span><span class="sxs-lookup"><span data-stu-id="ff28a-150">Publish the template</span></span> 
<span data-ttu-id="ff28a-151">When you publish a template, Azure Lab Services creates VMs in the lab by using the template.</span><span class="sxs-lookup"><span data-stu-id="ff28a-151">When you publish a template, Azure Lab Services creates VMs in the lab by using the template.</span></span> <span data-ttu-id="ff28a-152">The number of VMs created in this process is same as the maximum number of users allowed into the lab, which you can set in the usage policy of the lab.</span><span class="sxs-lookup"><span data-stu-id="ff28a-152">The number of VMs created in this process is same as the maximum number of users allowed into the lab, which you can set in the usage policy of the lab.</span></span> <span data-ttu-id="ff28a-153">All virtual machines have the same configuration as the template.</span><span class="sxs-lookup"><span data-stu-id="ff28a-153">All virtual machines have the same configuration as the template.</span></span> 

1. <span data-ttu-id="ff28a-154">Select **Publish** in the **Template** section.</span><span class="sxs-lookup"><span data-stu-id="ff28a-154">Select **Publish** in the **Template** section.</span></span> 

    ![Publish the template VM](../media/tutorial-setup-classroom-lab/public-access.png)
1. <span data-ttu-id="ff28a-156">In the **Publish** window, select the **Published** option.</span><span class="sxs-lookup"><span data-stu-id="ff28a-156">In the **Publish** window, select the **Published** option.</span></span> 
2. <span data-ttu-id="ff28a-157">Now, select the **Publish** button.</span><span class="sxs-lookup"><span data-stu-id="ff28a-157">Now, select the **Publish** button.</span></span> <span data-ttu-id="ff28a-158">This process may take some time depending on how many VMs are being created, which is same as the number of users allowed into the lab.</span><span class="sxs-lookup"><span data-stu-id="ff28a-158">This process may take some time depending on how many VMs are being created, which is same as the number of users allowed into the lab.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="ff28a-159">Once a template is published, it can't be unpublished.</span><span class="sxs-lookup"><span data-stu-id="ff28a-159">Once a template is published, it can't be unpublished.</span></span> 
4. <span data-ttu-id="ff28a-160">Switch to the **Virtual machines** page, and confirm that you see virtual machines that are in **Unassigned** state.</span><span class="sxs-lookup"><span data-stu-id="ff28a-160">Switch to the **Virtual machines** page, and confirm that you see virtual machines that are in **Unassigned** state.</span></span> <span data-ttu-id="ff28a-161">These VMs are not assigned to students yet.</span><span class="sxs-lookup"><span data-stu-id="ff28a-161">These VMs are not assigned to students yet.</span></span> 

    ![Virtual machines](../media/tutorial-setup-classroom-lab/virtual-machines.png)
5. <span data-ttu-id="ff28a-163">Wait until the VMs are created.</span><span class="sxs-lookup"><span data-stu-id="ff28a-163">Wait until the VMs are created.</span></span> <span data-ttu-id="ff28a-164">They should be in **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="ff28a-164">They should be in **Stopped** state.</span></span> <span data-ttu-id="ff28a-165">You can start a student VM, connect to the VM, stop the VM, and delete the VM on this page.</span><span class="sxs-lookup"><span data-stu-id="ff28a-165">You can start a student VM, connect to the VM, stop the VM, and delete the VM on this page.</span></span> <span data-ttu-id="ff28a-166">You can start them in this page or let your students start the VMs.</span><span class="sxs-lookup"><span data-stu-id="ff28a-166">You can start them in this page or let your students start the VMs.</span></span> 

    ![Virtual machines in stopped state](../media/tutorial-setup-classroom-lab/virtual-machines-stopped.png)


## <a name="send-registration-link-to-students"></a><span data-ttu-id="ff28a-168">Send registration link to students</span><span class="sxs-lookup"><span data-stu-id="ff28a-168">Send registration link to students</span></span>

1. <span data-ttu-id="ff28a-169">Switch to the **Dashboard** view.</span><span class="sxs-lookup"><span data-stu-id="ff28a-169">Switch to the **Dashboard** view.</span></span> 
2. <span data-ttu-id="ff28a-170">Select **User registration** tile.</span><span class="sxs-lookup"><span data-stu-id="ff28a-170">Select **User registration** tile.</span></span>

    ![Student registration link](../media/tutorial-setup-classroom-lab/dashboard-user-registration-link.png)
1. <span data-ttu-id="ff28a-172">In the **User registration** dialog box, select the **Copy** button.</span><span class="sxs-lookup"><span data-stu-id="ff28a-172">In the **User registration** dialog box, select the **Copy** button.</span></span> <span data-ttu-id="ff28a-173">The link is copied to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="ff28a-173">The link is copied to the clipboard.</span></span> <span data-ttu-id="ff28a-174">Paste it in an email editor, and send an email to the student.</span><span class="sxs-lookup"><span data-stu-id="ff28a-174">Paste it in an email editor, and send an email to the student.</span></span> 

    ![Student registration link](../media/tutorial-setup-classroom-lab/registration-link.png)
2. <span data-ttu-id="ff28a-176">On the **User registration** dialog box, select **Close**.</span><span class="sxs-lookup"><span data-stu-id="ff28a-176">On the **User registration** dialog box, select **Close**.</span></span> 

## <a name="view-all-classroom-labs"></a><span data-ttu-id="ff28a-177">View all classroom labs</span><span class="sxs-lookup"><span data-stu-id="ff28a-177">View all classroom labs</span></span>
1. <span data-ttu-id="ff28a-178">Navigate to [Azure Lab Services portal](https://labs.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff28a-178">Navigate to [Azure Lab Services portal](https://labs.azure.com).</span></span>
2. <span data-ttu-id="ff28a-179">Confirm that you see all the labs in the selected lab account.</span><span class="sxs-lookup"><span data-stu-id="ff28a-179">Confirm that you see all the labs in the selected lab account.</span></span> 

    ![All labs](../media/how-to-manage-classroom-labs/all-labs.png)
3. <span data-ttu-id="ff28a-181">Use the drop-down list at the top to select a different lab account.</span><span class="sxs-lookup"><span data-stu-id="ff28a-181">Use the drop-down list at the top to select a different lab account.</span></span> <span data-ttu-id="ff28a-182">You see labs in the selected lab account.</span><span class="sxs-lookup"><span data-stu-id="ff28a-182">You see labs in the selected lab account.</span></span> 

## <a name="delete-a-classroom-lab"></a><span data-ttu-id="ff28a-183">Delete a classroom lab</span><span class="sxs-lookup"><span data-stu-id="ff28a-183">Delete a classroom lab</span></span>
1. <span data-ttu-id="ff28a-184">On the tile for the lab, select three dots (...) in the corner.</span><span class="sxs-lookup"><span data-stu-id="ff28a-184">On the tile for the lab, select three dots (...) in the corner.</span></span> 

    ![Select the lab](../media/how-to-manage-classroom-labs/select-three-dots.png)
2. <span data-ttu-id="ff28a-186">Select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="ff28a-186">Select **Delete**.</span></span> 

    ![Delete button](../media/how-to-manage-classroom-labs/delete-button.png)
3. <span data-ttu-id="ff28a-188">On the **Delete lab** dialog box, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="ff28a-188">On the **Delete lab** dialog box, select **Delete**.</span></span> 

    ![Delete dialog box](../media/how-to-manage-classroom-labs/delete-lab-dialog-box.png)
 
## <a name="manage-student-vms"></a><span data-ttu-id="ff28a-190">Manage student VMs</span><span class="sxs-lookup"><span data-stu-id="ff28a-190">Manage student VMs</span></span>
<span data-ttu-id="ff28a-191">Once students register with Azure Lab Services using the registration link you provided to them, you see the VMs assigned to students on the **Virtual machines** tab.</span><span class="sxs-lookup"><span data-stu-id="ff28a-191">Once students register with Azure Lab Services using the registration link you provided to them, you see the VMs assigned to students on the **Virtual machines** tab.</span></span> 

![Virtual machines assigned to students](../media/how-to-manage-classroom-labs/virtual-machines-students.png)

<span data-ttu-id="ff28a-193">You can do the following tasks on a student VM:</span><span class="sxs-lookup"><span data-stu-id="ff28a-193">You can do the following tasks on a student VM:</span></span> 

- <span data-ttu-id="ff28a-194">Stop a VM if the VM is running.</span><span class="sxs-lookup"><span data-stu-id="ff28a-194">Stop a VM if the VM is running.</span></span> 
- <span data-ttu-id="ff28a-195">Start a VM if the VM is stopped.</span><span class="sxs-lookup"><span data-stu-id="ff28a-195">Start a VM if the VM is stopped.</span></span> 
- <span data-ttu-id="ff28a-196">Connect to the VM.</span><span class="sxs-lookup"><span data-stu-id="ff28a-196">Connect to the VM.</span></span> 
- <span data-ttu-id="ff28a-197">Delete the VM.</span><span class="sxs-lookup"><span data-stu-id="ff28a-197">Delete the VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ff28a-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff28a-198">Next steps</span></span>
<span data-ttu-id="ff28a-199">Get started with setting up a lab using Azure Lab Services:</span><span class="sxs-lookup"><span data-stu-id="ff28a-199">Get started with setting up a lab using Azure Lab Services:</span></span>

- [<span data-ttu-id="ff28a-200">Set up a classroom lab</span><span class="sxs-lookup"><span data-stu-id="ff28a-200">Set up a classroom lab</span></span>](how-to-manage-classroom-labs.md)
- [<span data-ttu-id="ff28a-201">Set up a lab</span><span class="sxs-lookup"><span data-stu-id="ff28a-201">Set up a lab</span></span>](../tutorial-create-custom-lab.md)
