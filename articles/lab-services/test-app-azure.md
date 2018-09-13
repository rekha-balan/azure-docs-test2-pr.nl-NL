---
title: How to test your app in Azure | Microsoft Docs
description: Learn how to create a file share in a lab and mount it on your local machine and a virtual machine in the lab, and then deploy desktop/web applications to the file share and test them.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/04/2018
ms.author: spelluru
ms.openlocfilehash: 099bdc25c27e264c3c7732243068307856840409
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866228"
---
# <a name="test-your-app-in-azure"></a><span data-ttu-id="5eaa5-103">Test your app in Azure</span><span class="sxs-lookup"><span data-stu-id="5eaa5-103">Test your app in Azure</span></span> 
<span data-ttu-id="5eaa5-104">This article provides steps for testing your application in Azure using DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-104">This article provides steps for testing your application in Azure using DevTest Labs.</span></span> <span data-ttu-id="5eaa5-105">First, you set up a file share within a lab and mount it as a drive on your local development machine and a VM inside a lab.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-105">First, you set up a file share within a lab and mount it as a drive on your local development machine and a VM inside a lab.</span></span> <span data-ttu-id="5eaa5-106">Then, you use Visual Studio 2017 to deploy your app to the file share so that you can run the app on the VM in the lab.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-106">Then, you use Visual Studio 2017 to deploy your app to the file share so that you can run the app on the VM in the lab.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="5eaa5-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5eaa5-107">Prerequisites</span></span> 
1. <span data-ttu-id="5eaa5-108">[Create an Azure subscription](https://azure.microsoft.com/free/) if you don't already have one, and sign into [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5eaa5-108">[Create an Azure subscription](https://azure.microsoft.com/free/) if you don't already have one, and sign into [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5eaa5-109">Follow instructions in [this article](devtest-lab-create-lab.md) to create a lab using Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-109">Follow instructions in [this article](devtest-lab-create-lab.md) to create a lab using Azure DevTest Labs.</span></span> <span data-ttu-id="5eaa5-110">Pin the lab to your dashboard so that you can easily find it next time you sign in.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-110">Pin the lab to your dashboard so that you can easily find it next time you sign in.</span></span> <span data-ttu-id="5eaa5-111">Azure DevTest Labs enables you to create resources within Azure quickly by minimizing waste and controlling cost.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-111">Azure DevTest Labs enables you to create resources within Azure quickly by minimizing waste and controlling cost.</span></span> <span data-ttu-id="5eaa5-112">To learn more about DevTest Labs, see [overview](devtest-lab-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5eaa5-112">To learn more about DevTest Labs, see [overview](devtest-lab-overview.md).</span></span> 
3. <span data-ttu-id="5eaa5-113">Create an Azure Storage account in the lab's resource group by following instructions in the [Create a storage account](../storage/common/storage-create-storage-account.md) article.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-113">Create an Azure Storage account in the lab's resource group by following instructions in the [Create a storage account](../storage/common/storage-create-storage-account.md) article.</span></span> <span data-ttu-id="5eaa5-114">On the **Create storage account** page, select **Use existing** for **Resource group**, and select the **lab's resource group**.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-114">On the **Create storage account** page, select **Use existing** for **Resource group**, and select the **lab's resource group**.</span></span> 
4. <span data-ttu-id="5eaa5-115">Create a file share in your Azure storage by following instructions in the [Create a file share in Azure Files](../storage/files/storage-how-to-create-file-share.md) article.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-115">Create a file share in your Azure storage by following instructions in the [Create a file share in Azure Files](../storage/files/storage-how-to-create-file-share.md) article.</span></span> 

## <a name="mount-the-file-share-on-your-local-machine"></a><span data-ttu-id="5eaa5-116">Mount the file share on your local machine</span><span class="sxs-lookup"><span data-stu-id="5eaa5-116">Mount the file share on your local machine</span></span>
1. <span data-ttu-id="5eaa5-117">On your local machine, use the script from [Persisting Azure file share credentials in Windows](../storage/files/storage-how-to-use-files-windows.md#persisting-azure-file-share-credentials-in-windows) section of [Use an Azure file share with Windows](../storage/files/storage-how-to-use-files-windows.md) article.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-117">On your local machine, use the script from [Persisting Azure file share credentials in Windows](../storage/files/storage-how-to-use-files-windows.md#persisting-azure-file-share-credentials-in-windows) section of [Use an Azure file share with Windows](../storage/files/storage-how-to-use-files-windows.md) article.</span></span> 
2. <span data-ttu-id="5eaa5-118">Then, use `net use` command to mount the file share on your machine.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-118">Then, use `net use` command to mount the file share on your machine.</span></span> <span data-ttu-id="5eaa5-119">Here is the sample command: Specify your Azure storage name and file share name before running the command.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-119">Here is the sample command: Specify your Azure storage name and file share name before running the command.</span></span> 

    `net use Z: \\<YOUR AZURE STORAGE NAME>.file.core.windows.net\<YOUR FILE SHARE NAME> /persistent:yes`

## <a name="create-a-vm-in-the-lab"></a><span data-ttu-id="5eaa5-120">Create a VM in the lab</span><span class="sxs-lookup"><span data-stu-id="5eaa5-120">Create a VM in the lab</span></span>
1. <span data-ttu-id="5eaa5-121">On the **File share** page, select the **resource group** in the breadcrumb menu at the top.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-121">On the **File share** page, select the **resource group** in the breadcrumb menu at the top.</span></span> <span data-ttu-id="5eaa5-122">You see the **Resource group** page.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-122">You see the **Resource group** page.</span></span> 
    
    ![Select resource group from breadcrumb menu](media/test-app-in-azure/select-resource-group-bread-crump.png)
2. <span data-ttu-id="5eaa5-124">On the **Resource group** page, select the **lab** you created in DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-124">On the **Resource group** page, select the **lab** you created in DevTest Labs.</span></span>

    ![Select the lab](media/test-app-in-azure/select-devtest-lab-in-resource-group.png)
3. <span data-ttu-id="5eaa5-126">On the **DevTest Lab** page for your lab, select **+ Add** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-126">On the **DevTest Lab** page for your lab, select **+ Add** on the toolbar.</span></span> 

    ![Add button for the lab](media/test-app-in-azure/add-button-in-lab.png)
4. <span data-ttu-id="5eaa5-128">On the **Choose a base** page, search for **smalldisk**, and select **[smalldisk] Windows Server 2016 Data Center**.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-128">On the **Choose a base** page, search for **smalldisk**, and select **[smalldisk] Windows Server 2016 Data Center**.</span></span> 

    ![Choose small disk Windows server](media/test-app-in-azure/choose-small-disk-windows-server.png)
5. <span data-ttu-id="5eaa5-130">On the **Virtual machine** page, specify **virtual machine name**, **user name**, **password**, and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-130">On the **Virtual machine** page, specify **virtual machine name**, **user name**, **password**, and select **Create**.</span></span>    
    
    ![Create virtual machine page](media/test-app-in-azure/create-virtual-machine-page.png)    

## <a name="mount-the-file-share-on-your-vm"></a><span data-ttu-id="5eaa5-132">Mount the file share on your VM</span><span class="sxs-lookup"><span data-stu-id="5eaa5-132">Mount the file share on your VM</span></span>
1. <span data-ttu-id="5eaa5-133">After the virtual machine is created successfully, select the **virtual machine** from the list.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-133">After the virtual machine is created successfully, select the **virtual machine** from the list.</span></span>    

    ![Select the lab VM](media/test-app-in-azure/select-lab-vm.png)
2. <span data-ttu-id="5eaa5-135">Select **Connect** on the toolbar to connect to the VM.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-135">Select **Connect** on the toolbar to connect to the VM.</span></span> 
3. <span data-ttu-id="5eaa5-136">[Install Azure PowerShell](https://azure.microsoft.com/downloads/) by using the **Windows install** link in the **Command-line tools** section.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-136">[Install Azure PowerShell](https://azure.microsoft.com/downloads/) by using the **Windows install** link in the **Command-line tools** section.</span></span> <span data-ttu-id="5eaa5-137">For other ways of installing Azure PowerShell, see [this article](/powershell/azure/install-azurerm-ps?view=azurermps-6.8.1).</span><span class="sxs-lookup"><span data-stu-id="5eaa5-137">For other ways of installing Azure PowerShell, see [this article](/powershell/azure/install-azurerm-ps?view=azurermps-6.8.1).</span></span>
4. <span data-ttu-id="5eaa5-138">Follow instructions in the [Mount the file share](#mount-the-file-share) section.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-138">Follow instructions in the [Mount the file share](#mount-the-file-share) section.</span></span> 

## <a name="publish-your-app-from-visual-studio"></a><span data-ttu-id="5eaa5-139">Publish your app from Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5eaa5-139">Publish your app from Visual Studio</span></span>
<span data-ttu-id="5eaa5-140">In this section, you publish your app from Visual Studio to a test VM in the cloud.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-140">In this section, you publish your app from Visual Studio to a test VM in the cloud.</span></span>

1. <span data-ttu-id="5eaa5-141">Create a desktop/web application by using Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-141">Create a desktop/web application by using Visual Studio 2017.</span></span>
2. <span data-ttu-id="5eaa5-142">Build your app.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-142">Build your app.</span></span>
3. <span data-ttu-id="5eaa5-143">To publish your app, right-click your project in the **Solution Explorer**, and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-143">To publish your app, right-click your project in the **Solution Explorer**, and select **Publish**.</span></span> 
4. <span data-ttu-id="5eaa5-144">In the **Publish wizard**, enter the **drive** that's mapped to your file share.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-144">In the **Publish wizard**, enter the **drive** that's mapped to your file share.</span></span>

    <span data-ttu-id="5eaa5-145">**Desktop app:**</span><span class="sxs-lookup"><span data-stu-id="5eaa5-145">**Desktop app:**</span></span>

    ![Desktop app](media/test-app-in-azure/desktop-app.png)

    <span data-ttu-id="5eaa5-147">**Web app:**</span><span class="sxs-lookup"><span data-stu-id="5eaa5-147">**Web app:**</span></span>

    ![Web app](media/test-app-in-azure/web-app.png)

1. <span data-ttu-id="5eaa5-149">Select **Next** to complete the publish workflow, and select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-149">Select **Next** to complete the publish workflow, and select **Finish**.</span></span> <span data-ttu-id="5eaa5-150">When you finish the wizard steps, Visual Studio builds your application and publishes it to your file share.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-150">When you finish the wizard steps, Visual Studio builds your application and publishes it to your file share.</span></span> 


## <a name="test-the-app-on-your-test-vm-in-the-lab"></a><span data-ttu-id="5eaa5-151">Test the app on your test VM in the lab</span><span class="sxs-lookup"><span data-stu-id="5eaa5-151">Test the app on your test VM in the lab</span></span>

1. <span data-ttu-id="5eaa5-152">Navigate to the virtual machine page for your VM in the lab.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-152">Navigate to the virtual machine page for your VM in the lab.</span></span> 
2. <span data-ttu-id="5eaa5-153">Select **Start** on the toolbar to start the VM if it's in stopped state.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-153">Select **Start** on the toolbar to start the VM if it's in stopped state.</span></span> <span data-ttu-id="5eaa5-154">You can set up auto-start and auto-shutdown policies for your VM to avoid starting and stopping each time.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-154">You can set up auto-start and auto-shutdown policies for your VM to avoid starting and stopping each time.</span></span> 
3. <span data-ttu-id="5eaa5-155">Select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-155">Select **Connect**.</span></span>

    ![Virtual machine page](media/test-app-in-azure/virtual-machine-page.png)
4. <span data-ttu-id="5eaa5-157">Within the virtual machine, launch **File Explorer**, and select **This PC** to find your file share.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-157">Within the virtual machine, launch **File Explorer**, and select **This PC** to find your file share.</span></span>

    ![Find share on VM](media/test-app-in-azure/find-share-on-vm.png)

    > [!NOTE]
    > <span data-ttu-id="5eaa5-159">For any reason, if you are unable to find your file share on your virtual machine or on your local machine, you can remount it by running the `net use` command.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-159">For any reason, if you are unable to find your file share on your virtual machine or on your local machine, you can remount it by running the `net use` command.</span></span> <span data-ttu-id="5eaa5-160">You can find the `net use` command on the **Connect** Wizard of your **File Share** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-160">You can find the `net use` command on the **Connect** Wizard of your **File Share** in the Azure portal.</span></span>
1. <span data-ttu-id="5eaa5-161">Open the file share and confirm that you see the app you deployed from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-161">Open the file share and confirm that you see the app you deployed from Visual Studio.</span></span> 

    ![Open share on VM](media/test-app-in-azure/open-file-share.png)

    <span data-ttu-id="5eaa5-163">You can now access and test your app within the test VM you created in Azure.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-163">You can now access and test your app within the test VM you created in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5eaa5-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="5eaa5-164">Next steps</span></span>
<span data-ttu-id="5eaa5-165">See the following articles to learn how to use VMs in a lab.</span><span class="sxs-lookup"><span data-stu-id="5eaa5-165">See the following articles to learn how to use VMs in a lab.</span></span> 

- [<span data-ttu-id="5eaa5-166">Add a VM to a lab</span><span class="sxs-lookup"><span data-stu-id="5eaa5-166">Add a VM to a lab</span></span>](devtest-lab-add-vm.md)
- [<span data-ttu-id="5eaa5-167">Restart a lab VM</span><span class="sxs-lookup"><span data-stu-id="5eaa5-167">Restart a lab VM</span></span>](devtest-lab-restart-vm.md)
- [<span data-ttu-id="5eaa5-168">Resize a lab VM</span><span class="sxs-lookup"><span data-stu-id="5eaa5-168">Resize a lab VM</span></span>](devtest-lab-resize-vm.md)
