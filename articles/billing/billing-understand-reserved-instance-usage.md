---
title: Understand Azure Reservations usage for Pay-As-You-Go subscription | Microsoft Docs
description: Learn how to read your usage to understand how the Azure reservation for your Pay-As-You-Go subscription is applied.
services: billing
documentationcenter: ''
author: manish-shukla01
manager: manshuk
editor: ''
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2018
ms.author: manshuk
ms.openlocfilehash: 1226b2f73d556da2ff7d73f6f322e0bd1590f915
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858056"
---
# <a name="understand-azure-reservation-usage-for-your-pay-as-you-go-subscription"></a>Understand Azure reservation usage for your Pay-As-You-Go subscription

Use the ReservationId from [Reservation page](https://portal.azure.com/?microsoft_azure_marketplace_ItemHideKey=Reservations&Microsoft_Azure_Reservations=true#blade/Microsoft_Azure_Reservations/ReservationsBrowseBlade) and the usage file from the [Azure Accounts portal](https://account.azure.com) to evaluate your reservation usage.

If you are a customer with an Enterprise Agreement, see [Understand reservation usage for your Enterprise enrollment.](billing-understand-reserved-instance-usage-ea.md).

This article assumes that the reservation is applied to a single subscription. If the reservation is applied to more than one subscription, your reservation benefit may span multiple usage CSV files.

## <a name="usage-for-reserved-virtual-machine-instances"></a>Usage for Reserved Virtual Machine Instances

For the following sections, assume that you are running a Standard_DS1_v2 Windows VM in the east US region and your reserved VM instance information looks like the following table:

| Field | Value |
|---| :---: |
|ReservationId |8117adfb-1d94-4675-be2b-f3c1bca808b6|
|Quantity |1|
|SKU | Standard_DS1_v2|
|Region | eastus |

The hardware portion of the VM is covered because the deployed VM matches the reservation attributes. To see what Windows software isn't covered by the reserved VM instance, see [Azure Reserve VM Instances Windows software costs](billing-reserved-instance-windows-software-costs.md)

### <a name="statement-section-of-csv-file-for-vms"></a>Statement section of CSV file for VMs

This section of your CSV file shows the total usage for your reservation. Apply the filter on the **Meter Subcategory** field that contains **"Reservation-"**. You see something like the following screenshot:

![Screenshot of filtered reservation usage details and charges](./media/billing-understand-reserved-instance-usage/billing-payg-reserved-instance-csv-statements.png)

The **Reservation-Base VM** line has the total number of hours that are covered by the reservation. This line is $0.00 because the reservation covers it. The **Reservation-Windows Svr (1 Core)** line covers the cost of Windows software.

### <a name="daily-usage-section-of-csv-file"></a>Daily usage section of CSV file

Filter on **Additional Info** and type in your **Reservation ID**. The following screenshot shows the fields related to the reservation.

![Screenshot of daily usage details and charges](./media/billing-understand-reserved-instance-usage/billing-payg-reserved-instance-csv-details.png)

1. **ReservationId** in the **Additional Info** field is the reservation that's applied to the VM.
2. **ConsumptionMeter** is the meter ID for the VM.
3. The **Reservation-Base VM** **Meter Subcategory** line represents the $0 cost in statement section. The cost of running this VM is already paid by the reservation.
4. **Meter ID** is the meter ID for the reservation. The cost of this meter is $0. This meter id appears for any VM that qualifies for the reservation discount.
5. Standard_DS1_v2 is one vCPU VM and the VM is deployed without Azure Hybrid Benefit. So, this meter covers the extra charge of the Windows software. To find the meter corresponding to D series 1 core VM, see [Azure Reserve VM Instances Windows software costs](billing-reserved-instance-windows-software-costs.md). If you have the Azure Hybrid Benefit, this extra charge is not applied.

## <a name="usage-for-sql-database-reserved-capacity-reservations"></a>Usage for SQL Database reserved capacity reservations

For the following sections, assume that you are running a SQL Database Gen 4 in the east US region and your reservation information looks like the following table:

| Field | Value |
|---| --- |
|ReservationId |446ec809-423d-467c-8c5c-bbd5d22906b1|
|Quantity |2|
|Product| SQL Database Gen 4 (2 Core)|
|Region | eastus |

### <a name="statement-section-of-csv-file"></a>Statement section of CSV file

Filter on **Reserved Instance Usage** meter name. You see something like the following screenshot:

![CSV file for SQL Database reserved capacity](./media/billing-understand-reserved-instance-usage/billing-payg-sql-db-reserved-capacity-csv-statements.png)

The **Reserved Instance Usage** line has the total number of core hours covered by the reservation. The rate is $0 for this line as the reservation covered the cost.

### <a name="detail-section-of-csv-file"></a>Detail section of CSV file

Filter on **Additional Info** and type in your **Reservation ID**. The following screenshot shows the fields related to the SQL Database reserved capacity reservation.

![CSV file for SQL Database reserved capacity](./media/billing-understand-reserved-instance-usage/billing-payg-sql-db-reserved-capacity-csv-details.png)

1. **ReservationId** in the **Additional Info** field is the SQL Database reserved capacity reservation that's applied to the SQL database resource.
2. **ConsumptionMeter** is the meter ID for the SQL Database resource.
3. The **Meter Id** is the reservation meter. The cost of this meter is $0. Any SQL Database resources that qualify for the reservation discount shows this meter ID in the CSV file.

## <a name="next-steps"></a>Next steps

To learn more about Azure Reservations, see the following articles:

- [What are Azure Reservations?](billing-save-compute-costs-reservations.md)
- [Prepay for Virtual Machines with Azure Reserved VM Instances](../virtual-machines/windows/prepay-reserved-vm-instances.md)
- [Prepay for SQL Database compute resources with Azure SQL Database reserved capacity](../sql-database/sql-database-reserved-capacity.md)
- [Manage Azure Reservations](billing-manage-reserved-vm-instance.md)
- [Understand how the reservation discount is applied](billing-understand-vm-reservation-charges.md)
- [Understand reservation usage for your Enterprise enrollment](billing-understand-reserved-instance-usage-ea.md)
- [Windows software costs not included with Reservations](billing-reserved-instance-windows-software-costs.md)

## <a name="need-help-contact-support"></a>Need help? Contact support

If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.