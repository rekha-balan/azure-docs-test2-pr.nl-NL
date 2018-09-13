---
title: Create a lab in Azure DevTest Labs | Microsoft Docs
description: Create a lab in Azure DevTest Labs for virtual machines
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: a1e52a8ff7a2018c54c7b88b80bab3c2897b1fb4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870657"
---
# <a name="create-a-lab-in-azure-devtest-labs"></a>Create a lab in Azure DevTest Labs
A lab in Azure DevTest Labs is the infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas. This article walks you through the process of creating a lab using the Azure portal.

## <a name="prerequisites"></a>Prerequisites
To create a lab, you need:

* An Azure subscription. To learn about Azure purchase options, see [How to buy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/). You must be the owner of the subscription to create the lab.

## <a name="steps-to-create-a-lab-in-azure-devtest-labs"></a>Steps to create a lab in Azure DevTest Labs
The following steps illustrate how to use the Azure portal to create a lab in Azure DevTest Labs. 

1. Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. From the main menu on the left side, select **All Services** (at the top of the list).

    ![All services menu option](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. From the list of available services, **DevTest Labs**.
1. In the **DevTest Labs** area, select **Add**.
   
    ![Add a lab](./media/devtest-lab-create-lab/add-lab-button.png)

1. Under **Create a DevTest Lab**:
   
    1. Enter a **Lab Name** for the new lab.
    2. Select the **Subscription** to associate with the lab.
    3. Select a **Location** in which to store the lab.
    4. Select **Auto-shutdown** to specify if you want to enable - and define the parameters for - the automatic shutting down of all the lab's VMs. The auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want the VM to automatically be shut down. You can change auto-shutdown settings after creating the lab by following the steps outlined in the article [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).
    1. Enter **NAME** and **VALUE** information for **Tags** if you want to create custom tagging that is added to every resource you will create in the lab. Tags are useful to help you manage and organize lab resources by category. For more information about tags, including how to add tags after creating the lab, see [Add tags to a lab](devtest-lab-add-tag.md).
    5. Select **Pin to Dashboard** if you want a shortcut of the lab to appear on the portal dashboard.
    6. Select **Automation options** to get Azure Resource Manager templates for configuration automation. 
    7. Select **Create**. You can monitor the status of the lab creation process by watching the **Notifications** area. Once completed, refresh the page to see the newly created lab in the list of labs.  
    
    ![Create a lab section of DevTest Labs](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Next steps
Once you've created your lab, here are some next steps to consider:

* [Secure access to a lab](devtest-lab-add-devtest-user.md)
* [Set lab policies](devtest-lab-set-lab-policy.md)
* [Create a lab template](devtest-lab-create-template.md)
* [Create custom artifacts for your VMs](devtest-lab-artifact-author.md)
* [Add a VM to a lab](devtest-lab-add-vm.md)

