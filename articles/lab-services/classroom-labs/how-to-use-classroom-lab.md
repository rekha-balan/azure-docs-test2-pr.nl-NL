---
title: How to access a classroom lab in Azure Lab Services | Microsoft Docs
description: In this tutorial, you access virtual machines in a classroom lab that's set up by a professor.
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
ms.openlocfilehash: 85da6989740446c980bcb9f2c89a6c31afe488fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865941"
---
# <a name="how-to-access-a-classroom-lab-in-azure-lab-services"></a>How to access a classroom lab in Azure Lab Services
This article describes how to access a classroom lab, connect to the VM in the lab, and stop the VM. 

## <a name="view-all-the-classroom-labs"></a>View all the classroom labs

1. Navigate to the **registration URL** that you received from the professor/educator. 
2. Sign in to the service using your school account to complete the registration. 
3. Once registered, confirm that you see the virtual machines for the labs you have access to. 

    ![View all labs](../media/how-to-use-classroom-lab/all-labs.png)

## <a name="connect-to-the-virtual-machine-in-a-classroom-lab"></a>Connect to the virtual machine in a classroom lab

1. Select **Connect** on the tile that represents the virtual machine of the lab that you want to access.

    ![View all labs](../media/how-to-use-classroom-lab/connect-button.png)
2. It takes a few minutes for the virtual machine to be ready.

    ![Getting the virtual machine to be ready](../media/how-to-use-classroom-lab/getting-virtual-machine-ready.png)
3. Save the RDP file to the hard disk and open it. 
    
    ![Save the RDP file](../media/how-to-use-classroom-lab/save-rdp-file.png)
4. Use the **user name** and **password** you get from your educator/professor for logging in to the machine. 

## <a name="stop-the-virtual-machine-in-a-classroom-lab"></a>Stop the virtual machine in a classroom lab

Select **Stop** on the tile that represents the classroom lab. When the VM is stopped, the **Start** button on the tile is enabled. 

## <a name="next-steps"></a>Next steps
Get started with setting up a lab using Azure Lab Services:

- [Set up a classroom lab](how-to-manage-classroom-labs.md)
- [Set up a lab](../tutorial-create-custom-lab.md)

 