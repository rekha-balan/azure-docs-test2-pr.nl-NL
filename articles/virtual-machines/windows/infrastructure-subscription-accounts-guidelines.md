---
title: Subscription and accounts for Windows VMs in Azure | Microsoft Docs
description: Learn about the key design and implementation guidelines for subscriptions and accounts on Azure.
documentationcenter: ''
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 761fa847-78b0-4078-a33a-d95d198d1029
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2f245ad9d5cad59531466c2183b565a96e7d53ce
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555559"
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a>Azure subscription and accounts guidelines for Windows VMs

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

This article focuses on understanding how to approach subscription and account management as your environment and user base grows.

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>Implementation guidelines for subscriptions and accounts
Decisions:

* What set of subscriptions and accounts do you need to host your IT workload or infrastructure?
* How to break down the hierarchy to fit your organization?

Tasks:

* Define your logical organization hierarchy as you would like to manage it from a subscription level.
* To match this logical hierarchy, define the accounts required and subscriptions under each account.
* Create the set of subscriptions and accounts using your naming convention.

## <a name="subscriptions-and-accounts"></a>Subscriptions and accounts
To work with Azure, you need one or more Azure subscriptions. Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.

* Enterprise customers typically have an Enterprise Enrollment, which is the top-most resource in the hierarchy, and is associated to one or more accounts.
* For consumers and customers without an Enterprise Enrollment, the top-most resource is the account.
* Subscriptions are associated to accounts, and there can be one or more subscriptions per account. Azure records billing information at the subscription level.

Due to the limit of two hierarchy levels on the Account/Subscription relationship, it is important to align the naming convention of accounts and subscriptions to the billing needs. For instance, if a global company uses Azure, they might choose to have one account per region, and have subscriptions managed at the region level:

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

For instance, you might use the following structure:

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

If a region decides to have more than one subscription associated to a particular group, the naming convention should incorporate a way to encode the extra data on either the account or the subscription name. This organization allows massaging billing data to generate the new levels of hierarchy during billing reports:

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

The organization could look like the following example:

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.

## <a name="next-steps"></a>Next steps
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]





