---
title: Create an Azure DevTest Labs custom image from a VM | Microsoft Docs
description: Learn how to create a custom image in Azure DevTest Labs from a provisioned VM using the Azure portal
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
ms.date: 04/05/2018
ms.author: spelluru
ms.openlocfilehash: 22f1579b2df2acdc736ed4c1d5cee64d096c320a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868665"
---
# <a name="create-a-custom-image-from-a-vm"></a>Create a custom image from a VM

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a>Step-by-step instructions

You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs. The following steps illustrate how to create a custom image from a VM:

1. Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Select **All services**, and then select **DevTest Labs** from the list.

1. From the list of labs, select the desired lab.  

1. On the lab's main pane, select **My virtual machines**.
 
1. On the **My virtual machines** pane, select the VM from which you want to create the custom image.

1. On the VM's management pane, select **Create custom image (VHD)**.

    ![Create custom image menu item](./media/devtest-lab-create-template/create-custom-image.png)

1. On the **Custom image** pane, enter a name and description for your custom image. This information is displayed in the list of bases when you create a VM. The custom image will include the OS disk and all the data disks attached to the virtual machine.

    ![Create custom image pane](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. Select whether sysprep was run on the VM. If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.

1. Select **OK** when finished to create the custom image.

After a few minutes, the custom image is created and is stored inside the lab’s storage account. When a lab user wants to create a new VM, the image is available in the list of base images.

![Custom image available in list of base images](./media/devtest-lab-create-template/custom-image-available-as-base.png)


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Related blog posts

- [Custom images or formulas?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copying Custom Images between Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

## <a name="next-steps"></a>Next steps

- [Add a VM to your lab](devtest-lab-add-vm.md)
