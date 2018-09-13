---
title: Configure private IP addresses for VMs - Azure portal | Microsoft Docs
description: Learn how to configure private IP addresses for virtual machines using the Azure portal.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7400d51ea193b3a50ddbbef7cf9e7ad25ad71744
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555970"
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-portal"></a>Configure private IP addresses for a virtual machine using the Azure portal

> [!div class="op_single_selector"]
> * [Azure portal](virtual-networks-static-private-ip-arm-pportal.md)
> * [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
> * [Azure CLI](virtual-networks-static-private-ip-arm-cli.md)
> * [Azure portal (Classic)](virtual-networks-static-private-ip-classic-pportal.md)
> * [PowerShell (Classic)](virtual-networks-static-private-ip-classic-ps.md)
> * [Azure CLI (Classic)](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

This article covers the Resource Manager deployment model. You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

The sample steps below expect a simple environment already created. If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).

## <a name="how-to-create-a-vm-for-testing-static-private-ip-addresses"></a>How to create a VM for testing static private IP addresses
You cannot set a static private IP address during the creation of a VM in the Resource Manager deployment mode by using the Azure portal. You must create the VM first, tehn set its private IP to be static.

To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet*, follow the steps below.

1. From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.
2. Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in the figure below.
   
    ![Create VM in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. In the **Basics** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password, as seen in the figure below.
   
    ![Basics blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. Make sure the **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.
   
    ![Basics blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. In the **Choose a size** blade, select **A1 Standard**, and then click **Select**.
   
    ![Choose a size blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. In teh **Settings** blade, make sure the following properties are set are set with the values below, and then click **OK**.
   
    -**Storage account**: *vnetstorage*
   
   * **Network**: *TestVNet*
   * **Subnet**: *FrontEnd*
     
     ![Choose a size blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. In the **Summary** blade, click **OK**. Notice the tile below displayed in your dashboard.
   
    ![Create VM in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a>How to retrieve static private IP address information for a VM
To view the static private IP address information for the VM created with the steps above, execute the steps below.

1. From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on the only network interface listed.
   
    ![Deploying VM tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. In the **Network interface** blade, click **All settings** > **IP addresses** and notice the **Assignment** and **IP address** values.
   
    ![Deploying VM tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a>How to add a static private IP address to an existing VM
To add a static private IP address to the VM created using the steps above, follow the steps below:

1. From the **IP addresses** blade shown above, click **Static** under **Assignment**.
2. Type *192.168.1.101* for **IP address**, and then click **Save**.
   
    ![Create VM in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> If after clicking **Save** you notice that the assignment is still set to **Dynamic**, it means that the IP address you typed is already in use. Try a different IP address.
> 
> 

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a>How to remove a static private IP address from a VM
To remove the static private IP address from the VM created above, complete the following step:

From the **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.

## <a name="next-steps"></a>Next steps
* Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.
* Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.
* Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).










