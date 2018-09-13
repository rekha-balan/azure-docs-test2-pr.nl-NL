---
title: Specify mandatory artifacts for your Azure DevTest Labs | Microsoft Docs
description: Learn how to specify mandatory artifacts that need to installed prior to installing any user-selected artifacts on virtual machines (VMs) in the lab.
services: devtest-lab,virtual-machines
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2018
ms.author: spelluru
ms.openlocfilehash: a739b958ad60e39c38e81ce887edf68349340bb0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857582"
---
# <a name="specify-mandatory-artifacts-for-your-lab-in-azure-devtest-labs"></a><span data-ttu-id="a6747-103">Specify mandatory artifacts for your lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a6747-103">Specify mandatory artifacts for your lab in Azure DevTest Labs</span></span>
<span data-ttu-id="a6747-104">As a owner of a lab, you can specify mandatory artifacts that are applied to every machine created in the lab.</span><span class="sxs-lookup"><span data-stu-id="a6747-104">As a owner of a lab, you can specify mandatory artifacts that are applied to every machine created in the lab.</span></span> <span data-ttu-id="a6747-105">Imagine a scenario where you want each machine in your lab to be connected to your corporate network.</span><span class="sxs-lookup"><span data-stu-id="a6747-105">Imagine a scenario where you want each machine in your lab to be connected to your corporate network.</span></span> <span data-ttu-id="a6747-106">In this case, each lab user would have to add a domain join artifact during virtual machine creation to make sure their machine is connected to the corporate domain.</span><span class="sxs-lookup"><span data-stu-id="a6747-106">In this case, each lab user would have to add a domain join artifact during virtual machine creation to make sure their machine is connected to the corporate domain.</span></span> <span data-ttu-id="a6747-107">In other words, lab users would essentially have to re-create a machine in case they forget to apply mandatory artifacts on their machine.</span><span class="sxs-lookup"><span data-stu-id="a6747-107">In other words, lab users would essentially have to re-create a machine in case they forget to apply mandatory artifacts on their machine.</span></span> <span data-ttu-id="a6747-108">As a lab owner, you make the domain join artifact as a mandatory artifact in your lab.</span><span class="sxs-lookup"><span data-stu-id="a6747-108">As a lab owner, you make the domain join artifact as a mandatory artifact in your lab.</span></span> <span data-ttu-id="a6747-109">This step makes sure that each machine is connected to the corporate network and saving the time and effort for your lab users.</span><span class="sxs-lookup"><span data-stu-id="a6747-109">This step makes sure that each machine is connected to the corporate network and saving the time and effort for your lab users.</span></span>
 
<span data-ttu-id="a6747-110">Other mandatory artifacts could include a common tool that your team uses, or a platform-related security pack that each machine needs to have by default etc. In short, any common software that every machine in your lab must have becomes a mandatory artifact.</span><span class="sxs-lookup"><span data-stu-id="a6747-110">Other mandatory artifacts could include a common tool that your team uses, or a platform-related security pack that each machine needs to have by default etc. In short, any common software that every machine in your lab must have becomes a mandatory artifact.</span></span> <span data-ttu-id="a6747-111">If you create a custom image from a machine that has mandatory artifacts applied to it and then create a fresh machine from that image, the mandatory artifacts are reapplied on the machine during creation.</span><span class="sxs-lookup"><span data-stu-id="a6747-111">If you create a custom image from a machine that has mandatory artifacts applied to it and then create a fresh machine from that image, the mandatory artifacts are reapplied on the machine during creation.</span></span> <span data-ttu-id="a6747-112">This behavior also means that even though the custom image is old, every time you create a machine from it the most updated version of mandatory artifacts are applied to it during the creation flow.</span><span class="sxs-lookup"><span data-stu-id="a6747-112">This behavior also means that even though the custom image is old, every time you create a machine from it the most updated version of mandatory artifacts are applied to it during the creation flow.</span></span> 
 
<span data-ttu-id="a6747-113">Only artifacts that have no parameters are supported as mandatory ones.</span><span class="sxs-lookup"><span data-stu-id="a6747-113">Only artifacts that have no parameters are supported as mandatory ones.</span></span> <span data-ttu-id="a6747-114">Your lab user doesn't need to enter additional parameters during lab creation and thus making the process of VM creation simple.</span><span class="sxs-lookup"><span data-stu-id="a6747-114">Your lab user doesn't need to enter additional parameters during lab creation and thus making the process of VM creation simple.</span></span> 

## <a name="specify-mandatory-artifacts"></a><span data-ttu-id="a6747-115">Specify mandatory artifacts</span><span class="sxs-lookup"><span data-stu-id="a6747-115">Specify mandatory artifacts</span></span>
<span data-ttu-id="a6747-116">You can select mandatory artifacts for Windows and Linux machines separately.</span><span class="sxs-lookup"><span data-stu-id="a6747-116">You can select mandatory artifacts for Windows and Linux machines separately.</span></span> <span data-ttu-id="a6747-117">You can also reorder these artifacts depending on the order in which you would like them to applied.</span><span class="sxs-lookup"><span data-stu-id="a6747-117">You can also reorder these artifacts depending on the order in which you would like them to applied.</span></span> 

1. <span data-ttu-id="a6747-118">On the home page of your lab, select **Configuration and policies** under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="a6747-118">On the home page of your lab, select **Configuration and policies** under **SETTINGS**.</span></span> 
3. <span data-ttu-id="a6747-119">Select **Mandatory artifacts** under **EXTERNAL RESOURCES**.</span><span class="sxs-lookup"><span data-stu-id="a6747-119">Select **Mandatory artifacts** under **EXTERNAL RESOURCES**.</span></span> 
4. <span data-ttu-id="a6747-120">Select **Edit** in the **Windows** section or the **Linux** section.</span><span class="sxs-lookup"><span data-stu-id="a6747-120">Select **Edit** in the **Windows** section or the **Linux** section.</span></span> <span data-ttu-id="a6747-121">This example uses the **Windows** option.</span><span class="sxs-lookup"><span data-stu-id="a6747-121">This example uses the **Windows** option.</span></span> 

    ![Mandatory artifacts page - Edit button](media/devtest-lab-mandatory-artifacts/mandatory-artifacts-edit-button.png)
4. <span data-ttu-id="a6747-123">Select an artifact.</span><span class="sxs-lookup"><span data-stu-id="a6747-123">Select an artifact.</span></span> <span data-ttu-id="a6747-124">This example uses **7-Zip** option.</span><span class="sxs-lookup"><span data-stu-id="a6747-124">This example uses **7-Zip** option.</span></span> 
5. <span data-ttu-id="a6747-125">On the **Add artifact** page, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="a6747-125">On the **Add artifact** page, select **Add**.</span></span> 

    ![Mandatory artifacts page - Add 7-zip](media/devtest-lab-mandatory-artifacts/add-seven-zip.png)
6. <span data-ttu-id="a6747-127">To add another artifact, select the article, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="a6747-127">To add another artifact, select the article, and select **Add**.</span></span> <span data-ttu-id="a6747-128">This example adds **Chrome** as the second mandatory artifact.</span><span class="sxs-lookup"><span data-stu-id="a6747-128">This example adds **Chrome** as the second mandatory artifact.</span></span>

    ![Mandatory artifacts page - Add Chrome](media/devtest-lab-mandatory-artifacts/add-chrome.png)
7. <span data-ttu-id="a6747-130">On the **Mandatory artifacts** page, you see a message that specifies the number of artifacts selected.</span><span class="sxs-lookup"><span data-stu-id="a6747-130">On the **Mandatory artifacts** page, you see a message that specifies the number of artifacts selected.</span></span> <span data-ttu-id="a6747-131">If you click the message, you see the artifacts that you selected.</span><span class="sxs-lookup"><span data-stu-id="a6747-131">If you click the message, you see the artifacts that you selected.</span></span> <span data-ttu-id="a6747-132">Select **Save** to save.</span><span class="sxs-lookup"><span data-stu-id="a6747-132">Select **Save** to save.</span></span> 

    ![Mandatory artifacts page - Save artifacts](media/devtest-lab-mandatory-artifacts/save-artifacts.png)
8. <span data-ttu-id="a6747-134">Repeat the steps to specify mandatory artifacts for Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="a6747-134">Repeat the steps to specify mandatory artifacts for Linux VMs.</span></span> 
    
    ![Mandatory artifacts page - Windows and Linux artifacts](media/devtest-lab-mandatory-artifacts/windows-linux-artifacts.png)
9. <span data-ttu-id="a6747-136">To **delete** an artifact from the list, select **...(ellipsis)** at the end of the row, and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="a6747-136">To **delete** an artifact from the list, select **...(ellipsis)** at the end of the row, and select **Delete**.</span></span> 
10. <span data-ttu-id="a6747-137">To **reorder** artifacts in the list, hover mouse over the artifact, select **...(ellipsis)** that shows up at the beginning of the row, and drag the item to the new position.</span><span class="sxs-lookup"><span data-stu-id="a6747-137">To **reorder** artifacts in the list, hover mouse over the artifact, select **...(ellipsis)** that shows up at the beginning of the row, and drag the item to the new position.</span></span> 
11. <span data-ttu-id="a6747-138">To save mandatory artifacts in the lab, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="a6747-138">To save mandatory artifacts in the lab, select **Save**.</span></span> 

    ![Mandatory artifacts page - Save artifacts in lab](media/devtest-lab-mandatory-artifacts/save-to-lab.png)
12. <span data-ttu-id="a6747-140">Close the **Configuration and policies** page (select **X** in the upper-right corner) to get back to the home page for your lab.</span><span class="sxs-lookup"><span data-stu-id="a6747-140">Close the **Configuration and policies** page (select **X** in the upper-right corner) to get back to the home page for your lab.</span></span>  

## <a name="delete-a-mandatory-artifact"></a><span data-ttu-id="a6747-141">Delete a mandatory artifact</span><span class="sxs-lookup"><span data-stu-id="a6747-141">Delete a mandatory artifact</span></span>
<span data-ttu-id="a6747-142">To delete a mandatory artifact from a lab, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="a6747-142">To delete a mandatory artifact from a lab, do the following actions:</span></span> 

1. <span data-ttu-id="a6747-143">Select **Configuration and policies** under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="a6747-143">Select **Configuration and policies** under **SETTINGS**.</span></span> 
2. <span data-ttu-id="a6747-144">Select **Mandatory artifacts** under **EXTERNAL RESOURCES**.</span><span class="sxs-lookup"><span data-stu-id="a6747-144">Select **Mandatory artifacts** under **EXTERNAL RESOURCES**.</span></span> 
3. <span data-ttu-id="a6747-145">Select **Edit** in the **Windows** section or the **Linux** section.</span><span class="sxs-lookup"><span data-stu-id="a6747-145">Select **Edit** in the **Windows** section or the **Linux** section.</span></span> <span data-ttu-id="a6747-146">This example uses the **Windows** option.</span><span class="sxs-lookup"><span data-stu-id="a6747-146">This example uses the **Windows** option.</span></span> 
4. <span data-ttu-id="a6747-147">Select the message with the number of mandatory artifacts at the top.</span><span class="sxs-lookup"><span data-stu-id="a6747-147">Select the message with the number of mandatory artifacts at the top.</span></span> 

    ![Mandatory artifacts page - Select the message](media/devtest-lab-mandatory-artifacts/select-message-artifacts.png)
5. <span data-ttu-id="a6747-149">On the **Selected artifacts** page, select **...(ellipsis)** for the artifact to be deleted, and select **Remove**.</span><span class="sxs-lookup"><span data-stu-id="a6747-149">On the **Selected artifacts** page, select **...(ellipsis)** for the artifact to be deleted, and select **Remove**.</span></span> 
    
    ![Mandatory artifacts page - Remove artifact](media/devtest-lab-mandatory-artifacts/remove-artifact.png)
6. <span data-ttu-id="a6747-151">Select **OK** to close the **Selected artifacts** page.</span><span class="sxs-lookup"><span data-stu-id="a6747-151">Select **OK** to close the **Selected artifacts** page.</span></span> 
7. <span data-ttu-id="a6747-152">Select **Save** on the **Mandatory artifacts** page.</span><span class="sxs-lookup"><span data-stu-id="a6747-152">Select **Save** on the **Mandatory artifacts** page.</span></span>
8. <span data-ttu-id="a6747-153">Repeat steps for **Linux** images if needed.</span><span class="sxs-lookup"><span data-stu-id="a6747-153">Repeat steps for **Linux** images if needed.</span></span> 
9. <span data-ttu-id="a6747-154">Select **Save** to save all the changes to the lab.</span><span class="sxs-lookup"><span data-stu-id="a6747-154">Select **Save** to save all the changes to the lab.</span></span> 

## <a name="view-mandatory-artifacts-when-creating-a-vm"></a><span data-ttu-id="a6747-155">View mandatory artifacts when creating a VM</span><span class="sxs-lookup"><span data-stu-id="a6747-155">View mandatory artifacts when creating a VM</span></span>
<span data-ttu-id="a6747-156">Now, as a lab user you can view the list of mandatory artifacts while creating a VM in the lab.</span><span class="sxs-lookup"><span data-stu-id="a6747-156">Now, as a lab user you can view the list of mandatory artifacts while creating a VM in the lab.</span></span> <span data-ttu-id="a6747-157">You can't edit or delete mandatory artifacts set in the lab by your lab owner.</span><span class="sxs-lookup"><span data-stu-id="a6747-157">You can't edit or delete mandatory artifacts set in the lab by your lab owner.</span></span>

1. <span data-ttu-id="a6747-158">On the home page for your lab, select **Overview** from the menu.</span><span class="sxs-lookup"><span data-stu-id="a6747-158">On the home page for your lab, select **Overview** from the menu.</span></span>
2. <span data-ttu-id="a6747-159">To add a VM to the lab, select **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="a6747-159">To add a VM to the lab, select **+ Add**.</span></span> 
3. <span data-ttu-id="a6747-160">Select a **base image**.</span><span class="sxs-lookup"><span data-stu-id="a6747-160">Select a **base image**.</span></span> <span data-ttu-id="a6747-161">This example uses **Windows Server, version 1709**.</span><span class="sxs-lookup"><span data-stu-id="a6747-161">This example uses **Windows Server, version 1709**.</span></span>
4. <span data-ttu-id="a6747-162">Notice that you see a message for **Artifacts** with the number of mandatory artifacts selected.</span><span class="sxs-lookup"><span data-stu-id="a6747-162">Notice that you see a message for **Artifacts** with the number of mandatory artifacts selected.</span></span> 
5. <span data-ttu-id="a6747-163">Select **Artifacts**.</span><span class="sxs-lookup"><span data-stu-id="a6747-163">Select **Artifacts**.</span></span> 
6. <span data-ttu-id="a6747-164">Confirm that you see the **mandatory artifacts** you specified in the lab's configuration and policies.</span><span class="sxs-lookup"><span data-stu-id="a6747-164">Confirm that you see the **mandatory artifacts** you specified in the lab's configuration and policies.</span></span> 

    ![Create a VM - mandatory artifacts](media/devtest-lab-mandatory-artifacts/create-vm-artifacts.png)

## <a name="next-steps"></a><span data-ttu-id="a6747-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6747-166">Next steps</span></span>
* <span data-ttu-id="a6747-167">Learn how to [add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="a6747-167">Learn how to [add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>

