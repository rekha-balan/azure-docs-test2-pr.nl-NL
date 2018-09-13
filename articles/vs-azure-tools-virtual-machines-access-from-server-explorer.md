---
title: Accessing Azure Virtual Machines from Server Explorer | Microsoft Docs
description: Get an overview of how to view create and manage Azure virtual machines (VMs) in Server Explorer in Visual Studio.
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: tarcher
ms.openlocfilehash: 3a35bba4b5b694f9dd555d15fce934ff29d0ab70
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550425"
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>Accessing Azure Virtual Machines from Server Explorer
By using Server Explorer in Visual Studio, you can display information about your virtual machines hosted by Azure.

## <a name="accessing-virtual-machines-in-server-explorer"></a>Accessing virtual machines in Server Explorer
If you have virtual machines hosted by Azure, you can access them in Server Explorer. You must first sign in to your Azure subscription to view your mobile services. To sign in, open the shortcut menu for the Azure node in Server Explorer, and choose **Connect to Microsoft Azure**.

### <a name="to-get-information-about-your-virtual-machines"></a>To get information about your virtual machines
1. In Server Explorer, choose a virtual machine, and then choose the F4 key to show its properties window.
   
    The following table shows what properties are available, but they are all read-only. To change them, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).
   
   | Property | Description |
   | --- | --- |
   | DNS Name |The URL with the Internet address of the virtual machine. |
   | Environment |For a virtual machine, the value of this property is always Production. |
   | Name |The name of the virtual machine. |
   | Size |The size of the virtual machine, which reflects the amount of memory and disk space that’s available. For more information, see How To: Configure Virtual Machine Sizes. |
   | Status |Values include Starting, Started, Stopping, Stopped, and Retrieving Status. If Retrieving Status appears, the current status is unknown. The values for this property differ from the values that are used on the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885). |
   | SubscriptionID |The subscription ID for your Azure account. You can show this information on the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) by viewing the properties for a subscription. |
2. Choose an endpoint node, and then view the **Properties** window.
3. The following table describes the available properties of endpoints, but they are read-only. To add or edit the endpoints for a virtual machine, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885). 
   
   | Property | Description |
   | --- | --- |
   | Name |An identifier for the endpoint. |
   | Private Port |The port for network access internal to your application. |
   | Protocol |The protocol that the transport layer for this endpoint uses, either TCP or UDP. |
   | Public Port |The port that’s used for public access to your application. |

## <a name="next-steps"></a>Next steps
To learn more about using Azure roles in Visual Studio, see [Using Remote Desktop with Azure Roles](vs-azure-tools-remote-desktop-roles.md).

