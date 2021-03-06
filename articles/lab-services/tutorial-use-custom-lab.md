---
title: Access a lab in Azure DevTest Labs | Microsoft Docs
description: In this tutorial, you access the lab that's created by using Azure DevTest Labs, claim virtual machines, use them, and then unclaim them.
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
ms.date: 05/17/2018
ms.author: spelluru
ms.openlocfilehash: cd623767c9627810afb64ca9185c991c5c9f3858
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856150"
---
# <a name="tutorial-access-a-lab-in-azure-devtest-labs"></a>Tutorial: Access a lab in Azure DevTest Labs
In this tutorial, you use the lab that was created in the [Tutorial: Create a lab in Azure DevTest Labs](tutorial-create-custom-lab.md) .

In this tutorial, you do the following actions:

> [!div class="checklist"]
> * Claim a virtual machine (VM) in the lab
> * Connect to the VM
> * Unclaim the VM

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.

## <a name="access-the-lab"></a>Access the lab

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Select **All resources** on the left menu. 
3. Select **DevTest Labs** for resource type. 
4. Select the lab. 

    ![Select the lab](./media/tutorial-use-custom-lab/search-for-select-custom-lab.png)

## <a name="claim-a-vm"></a>Claim a VM

1. In the list of **Claimable virtual machines**, select **...** (ellipsis), and select **Claim machine**.

    ![Claim virtual machine](./media/tutorial-use-custom-lab/claim-virtual-machine.png)
1. Confirm that you see the VM in the list **My virtual machines**.

    ![My virtual machine](./media/tutorial-use-custom-lab/my-virtual-machines.png)

## <a name="connect-to-the-vm"></a>Connect to the VM

1. Select your VM in the list. You see the **Virtual Machine page** for your VM. Select **Connect** on the toolbar.

    ![Connect to virtual machine](./media/tutorial-use-custom-lab/connect-button.png)
2. Save the downloaded **RDP** file your hard disk and use it to connect to the virtual machine. Specify the user name and password you mentioned when the VM was created in the previous section. 

## <a name="unclaim-the-vm"></a>Unclaim the VM
After you are done with using the VM, unclaim the VM by following these steps: 

1. On the virtual machine page, and select **Unclaim** on the toolbar. 

    ![Unclaim VM](./media/tutorial-use-custom-lab/unclaim-vm-menu.png)
1. The VM is shut down before it's unclaimed. 

    ![Unclaim status](./media/tutorial-use-custom-lab/unclaim-status.png) 
1. After the unclaim operation is done, you see the VM in the list of **Claimable virtual machines** list at the bottom. 
    
## <a name="next-steps"></a>Next steps
This tutorial showed you how to access and use a lab that was created by using Azure DevTest Labs. For more information about accessing and using VMs in a lab, see 

> [!div class="nextstepaction"]
> [How to: Use VMs in a lab](devtest-lab-add-vm.md)

