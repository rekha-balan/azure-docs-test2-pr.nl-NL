---
title: Manage Azure Reservations | Microsoft Docs
description: Learn how you can change subscription scope and manage access for Azure Reservations.
services: billing
documentationcenter: ''
author: yashesvi
manager: yashesvi
editor: ''
ms.service: billing
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2018
ms.author: yashesvi
ms.openlocfilehash: 3e5316ac0ca20c58a0960818d3151c238927df0d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866173"
---
# <a name="manage-reservations-for-azure-resources"></a>Manage Reservations for Azure resources

After you buy an Azure Reservation, you may need to apply the reservation to a different subscription, change who can manage the reservation, or change the scope of the reservation. You can also split a reservation into two reservations to apply some of the instances you bought to another subscription.

If you bought Azure Reserved Virtual Machine Instances, you can change the optimize setting for the reservation. The reservation discount can apply to VMs in the same series or you can reserve data center capacity for a specific VM size.

## <a name="change-the-scope-for-a-reservation"></a>Change the scope for a reservation

 Your reservation discount applies to virtual machines, SQL databases, or other resources that match your reservation and run within the reservation scope. The scope of a reservation can be single subscription or all subscriptions in your billing context. If you set the scope to single subscription, the reservation is matched to running resources in the selected subscription. If you set the scope to shared, Azure matches the reservation to resources that run in all the subscriptions within the billing context. The billing context is dependent on the subscription used to buy the reservation.

To update the scope of a reservation:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Select **All services** > **Reservations**.
3. Select the reservation.
4. Select **Settings** > **Configuration**.
5. Change the scope. 

If you change from shared to single scope, you can only select subscriptions where you are the owner. Only subscriptions within the same billing context as the reservation, can be selected.

The scope only applies to Pay-As-You-Go offer MS-AZR-0003P, Enterprise offer MS-AZR-0017P, or CSP subscription types. For enterprise agreements, dev/test subscriptions are not eligible to get the reservation discount.

## <a name="add-or-change-users-who-can-manage-a-reservation"></a>Add or change users who can manage a reservation

You can delegate management of a reservation by adding people to roles on the reservation. By default, the person that bought the reservation and the account administrator have the Owner role on the reservation.

You can manage access to reservations independently from the subscriptions that get the reservation discount. When you give someone permissions to manage a reservation, that doesn't give them rights to manage the subscription. And if you give someone permissions to manage a subscription within the reservation's scope, that doesn't give them rights to manage the reservation.

To delegate access management for a reservation:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Select **All Services** > **Reservation** to list reservations that you have access to.
3. Select the reservation that you want to delegate access to other users.
4. Select **Access Control (IAM)**.
5. Select **Add** > **Role** > **Owner**. Or, if you want to give limited access, select a different role.
6. Type the email address of the user you want to add as owner.
7. Select the user, and then select **Save**.

## <a name="split-a-single-reservation-into-two-reservations"></a>Split a single reservation into two reservations

 After you buy more than one resource instance within a reservation, you may want to assign instances within that reservation to different subscriptions. By default, all instances have one scope - either single subscription or shared. For example, you bought 10 reservation instances and specified the scope to be subscription A. You may now want to change the scope for 7 reservations to subscription A and the remaining 3 to subscription B. Splitting a reservation allows you to distribute instances for granular scope management. You can simplify the allocation to subscriptions by choosing shared scope. But for cost management or budgeting purposes, you can allocate quantities to specific subscriptions.

 You can split a reservation into two reservations though PowerShell, CLI, or through the API.

### <a name="split-a-reservation-by-using-powershell"></a>Split a reservation by using PowerShell

1. Get the reservation order ID by running the following command:

    ```powershell
    # Get the reservation orders you have access to
    Get-AzureRmReservationOrder
    ```

2. Get the details of a reservation:

    ```powershell
    Get-AzureRmReservation -ReservationOrderId a08160d4-ce6b-4295-bf52-b90a5d4c96a0 -ReservationId b8be062a-fb0a-46c1-808a-5a844714965a
    ```

3. Split the reservation into two and distribute the instances:

    ```powershell
    # Split the reservation. The sum of the reservations, the quantity, must equal the total number of instances in the reservation that you're splitting.
    Split-AzureRmReservation -ReservationOrderId a08160d4-ce6b-4295-bf52-b90a5d4c96a0 -ReservationId b8be062a-fb0a-46c1-808a-5a844714965a -Quantity 3,2
    ```
4. You can update the scope by running the following command:

    ```powershell
    Update-AzureRmReservation -ReservationOrderId a08160d4-ce6b-4295-bf52-b90a5d4c96a0 -ReservationId 5257501b-d3e8-449d-a1ab-4879b1863aca -AppliedScopeType Single -AppliedScope /subscriptions/15bb3be0-76d5-491c-8078-61fe3468d414
    ```

## <a name="cancellations-and-exchanges"></a>Cancellations and exchanges

Depending on the reservation type, you may be able to cancel or exchange a reservation. For more information, see the cancellation and exchanges sections in the following topics:

- [Prepay for Virtual Machines with Azure Reserved VM Instances](..//virtual-machines/windows/prepay-reserved-vm-instances.md#cancellations-and-exchanges)
- [Prepay for SUSE software plans from Azure Reservations](../virtual-machines/linux/prepay-suse-software-charges.md#cancellation-and-exchanges-not-allowed)
- [Prepay for SQL Database compute resources with Azure SQL Database reserved capacity](../sql-database/sql-database-reserved-capacity.md#cancellations-and-exchanges)

## <a name="change-optimize-setting-for-reserved-vm-instances"></a>Change optimize setting for Reserved VM Instances

 When you buy a Reserved VM Instance, you choose instance size flexibility or capacity priority. Instance size flexibility applies the reservation discount to other VMs in the same [VM size group](https://aka.ms/RIVMGroups). Capacity priority prioritizes data center capacity for your deployments. This option offers additional confidence in your ability to launch the VM instances when you need them.

By default, when the scope of the reservation is shared, the instance size flexibility is on. The data center capacity isn't prioritized for VM deployments.

For reservations where the scope is single, you can optimize the reservation for capacity priority instead of VM instance size flexibility.

To update the optimize setting for the reservation:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Select **All Services** > **Reservations**.
3. Select the reservation.
4. Select **Settings** > **Configuration**.
5. Change the **Optimize for** setting.

## <a name="next-steps"></a>Next steps

To learn more about Azure Reservations, see the following articles:

- [What are Azure Reservations?](billing-save-compute-costs-reservations.md)
- [Prepay for Virtual Machines with Azure Reserved VM Instances](../virtual-machines/windows/prepay-reserved-vm-instances.md)
- [Prepay for SQL Database compute resources with Azure SQL Database reserved capacity](../sql-database/sql-database-reserved-capacity.md)
- [Prepay for SUSE software plans from Azure Reservations](../virtual-machines/linux/prepay-suse-software-charges.md)
- [Understand how the VM reservation discount is applied](billing-understand-vm-reservation-charges.md)
- [Understand how the SUSE Linux Enterprise software plan discount is applied](../billing/billing-understand-suse-reservation-charges.md)
- [Understand how other reservation discounts are applied](billing-understand-reservation-charges.md)
- [Understand reservation usage for your Pay-As-You-Go subscription](billing-understand-reserved-instance-usage.md)
- [Understand reservation usage for your Enterprise enrollment](billing-understand-reserved-instance-usage-ea.md)
- [Windows software costs not included with Reservations](billing-reserved-instance-windows-software-costs.md)

## <a name="need-help-contact-support"></a>Need help? Contact support

If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.
