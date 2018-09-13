---
title: Understand shared IP addresses in Azure DevTest Labs | Microsoft Docs
description: Learn how Azure DevTest Labs uses shared IP addresses to minimize the public IP addresses required to access your lab VMs.
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: ''
ms.assetid: ''
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: f20f1d9370480b13ba1331d95c16345317eba27c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552573"
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a>Understand shared IP addresses in Azure DevTest Labs

Azure DevTest Labs uses shared IP addresses to minimize the number of public IP addresses required to access your individual lab VMs.  This article describes how shared IPs work and their related configuration options.

## <a name="shared-ip-setting"></a>Shared IP setting

When you create a lab, it resides in a subnet of a virtual network.  By default, this subnet is created with **Enable shared public IP** set to *Yes*.  This configuration creates one public IP address for the entire subnet.  For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).

![New lab subnet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-shared-ip/lab-subnet.png)

Any VMs created in this lab default to using a shared IP.  When creating the VM, this setting can be observed in the **Advanced settings** blade under **IP address configuration**.

![New VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-shared-ip/new-vm.png)

Whenever a VM with shared IP enabled is added to the subnet, a TCP port is assigned on the public IP address forwarding to the RDP port on the VM.  

## <a name="using-the-shared-ip"></a>Using the shared IP

You connect to Remote Desktop on the VM in an RDP client using the IP address or fully qualified domain name, followed by a colon, followed by the port.  For example, in the image below, the RDP address to connect to the VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.  Alternatively, from the Azure portal, select the **Connect** button to download a pre-configured RDP file.

![VM example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-shared-ip/vm-info.png)

## <a name="next-steps"></a>Next steps

* [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md)
* [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md)








