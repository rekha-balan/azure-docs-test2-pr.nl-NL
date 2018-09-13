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
# <a name="introduction-to-classroom-labs"></a>Introduction to classroom labs
Azure Lab Services enables you to quickly set up a classroom lab environment in the cloud. An educator creates a classroom lab, provisions Windows, or Linux virtual machines, installs the necessary software and tools labs in the class, and makes them available to students. The students in the class connect to virtual machines (VMs) in the lab, and use them for their projects, assignments, classroom exercises. 

The classroom labs are managed labs that are managed by Azure. The service itself handles all the infrastructure management for a managed lab, from spinning up virtual machines (VMs) to handling errors, and scaling the infrastructure. You specify what kind of infrastructure you need and install any tools or software that's required for the class. The managed labs are currently in preview.  

## <a name="scenarios"></a>Scenarios
Here is the main scenario that classroom labs of Azure Lab Services support: 

### <a name="set-up-a-resizable-computer-lab-in-the-cloud-for-your-classroom"></a>Set up a resizable computer lab in the cloud for your classroom  

- Create a managed classroom lab. You just tell the service exactly what you need, and it creates and manages the infrastructure of the lab for you so that you can focus on teaching your class, not technical details of a lab. 
- Provide students with a lab of virtual machines that are configured with exactly what’s needed for a class. Give each student a limited number of hours for using the VMs for class work.  
- Move your school’s physical computer lab into the cloud. Automatically scale the number of VMs only to the maximum usage and cost threshold that you set on the lab. 
- Delete the lab with a single click once you’re done. 

## <a name="user-profiles"></a>User profiles
This article describes different user profiles in Azure Lab Services. 

### <a name="lab-account-owner"></a>Lab account owner
Typically, and IT administrator of organization's cloud resources, who owns the Azure subscription acts as a lab account owner and does the following tasks:   

- Sets up a lab account for your organization.
- Manages and configures policies across all labs.
- Gives permissions to people in the organization to create a lab under the lab account.

### <a name="educator"></a>Educator
Typically, users such as a teacher or an online trainer creates classroom labs under a lab account. An educator does the following tasks: 

- Creates a classroom lab.
- Creates virtual machines in the lab. 
- Installs the appropriate software on virtual machines.
- Specifies who can access the lab.
- Provides registration link to the lab to students.

### <a name="student"></a>Student
A student does the following tasks:

- Uses the registration link that the lab user receives from a lab creator to register with the lab. 
- Connects to a virtual machine in the lab and use it for doing class work, assignments, and projects. 

## <a name="next-steps"></a>Next steps
Get started with setting up a lab account that's required to create a classroom lab using Azure Lab Services:

- [Set up a lab account](tutorial-setup-lab-account.md)
