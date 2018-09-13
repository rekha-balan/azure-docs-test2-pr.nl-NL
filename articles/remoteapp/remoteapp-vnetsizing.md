---
title: Sizing information for a VNET in Azure RemoteApp | Microsoft Docs
description: Learn about the IP address requirements for Azure RemoteApp running with a VNET
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9375981db64ec4a1ae523e958423b5f5787cec33
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540830"
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a>Sizing information for a VNET in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp is being discontinued on August 31, 2017. Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.
> 
> 

When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within the subnet. Based on the scale of your RemoteApp service, you need to ensure that your subnet has enough IP addresses available for RemoteApp virtual machines. While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range. This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase the subnet size without removing RemoteApp.

For each RemoteApp collection that you want to run at maximum capacity, you should have 100 IP addresses available. For example, if you have one RemoteApp collection in the Standard plan and you want to have the maximum 500 users, you should have 100 IP addresses for that collection. Similarly, you need 100 IP addresses for a RemoteApp collection in the Basic plan that has 800 users. If you plan to have fewer users (less than the maximum), you can reduce the IP addresses needed per collection. The minimum subnet size requirement is 30 IP addresses (/27).

Check out the following information to make sure your VNET is configured and working propertly:

* [Migrate from a personal VNET to an Azure VNET](remoteapp-migratevnet.md)
* [Validate the Azure VNET to use with Azure RemoteApp](remoteapp-vnet.md)

