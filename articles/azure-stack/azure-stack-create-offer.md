---
title: Create an offer in Azure Stack | Microsoft Docs
description: As a service administrator, learn how to create an offer for your tenants in Azure Stack.
services: azure-stack
documentationcenter: ''
author: ErikjeMS
manager: byronr
editor: ''
ms.assetid: 96b080a4-a9a5-407c-ba54-111de2413d59
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: erikje
ms.openlocfilehash: 0826c66d29be42b039fd21b431e2d33917acf0e1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660941"
---
# <a name="create-an-offer-in-azure-stack"></a>Create an offer in Azure Stack
[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present to tenants to purchase or subscribe to. This document shows you how to create an offer that includes the [plan that you created](azure-stack-create-plan.md) in the last step. This offer gives subscribers the ability to provision virtual machines.

1. [Sign in](azure-stack-connect-azure-stack.md) to the portal as a service administrator and then click **New** > **Tenant Offers + Plans** > **Offer**.
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-offer/image01.png)
2. In the **New Offer** blade, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**. The Display Name is the offer's friendly name. Only the admin can see the Resource Name. It's the name that admins use to work with the offer as an Azure Resource Manager resource.

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-offer/image01a.png)
3. Click **Base plans** and, in the **Plan** blade, select the plans you want to include in the offer, and then click **Select**. Click **Create** to create the offer.

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-offer/image02.png)
4. Click **Offers** and then click the offer you just created.

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-offer/image03.png)
5. Click **Change State**, and then click **Public**.

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-offer/image04.png)

Offers must be made public for tenants to get the full view when subscribing. Offers can be:

* **Public**: Visible to tenants.
* **Private**: Only visible to the service administrators. Useful while drafting the plan or offer, or if the service administrator wants to approve every subscription.
* **Decommissioned**: Closed to new subscribers. The service administrator can use decommissioned to prevent future subscriptions, but leave current subscribers untouched.

Changes to the offer are not immediately visible to the tenant. To see the changes, you might have to logout/login to see the new subscription in the “Subscription picker” when creating resources/resource groups.

## <a name="next-steps"></a>Next steps
[Subscribe to an offer and then provision a VM](azure-stack-subscribe-plan-provision-vm.md)





