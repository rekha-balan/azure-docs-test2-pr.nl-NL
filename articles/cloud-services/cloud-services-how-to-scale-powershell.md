---
title: Scale an Azure cloud service in Windows PowerShell | Microsoft Docs
description: (classic) Learn how to use PowerShell to scale a web role or worker role in or out in Azure.
services: cloud-services
documentationcenter: ''
author: mmccrory
manager: timlt
editor: ''
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: a7ae8ff202d403dff19b8c9a6a09492235db27ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784542"
---
# <a name="how-to-scale-a-cloud-service-in-powershell"></a>How to scale a cloud service in PowerShell

You can use Windows PowerShell to scale a web role or worker role in or out by adding or removing instances.  

## <a name="log-in-to-azure"></a>Log in to Azure

Before you can perform any operations on your subscription through PowerShell, you must log in:

```powershell
Add-AzureAccount
```

If you have multiple subscriptions associated with your account, you may need to change the current subscription depending on where your cloud service resides. To check the current subscription, run:

```powershell
Get-AzureSubscription -Current
```

If you need to change the current subscription, run:

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-the-current-instance-count-for-your-role"></a>Check the current instance count for your role

To check the current state of your role, run:

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

You should get back information about the role, including its current OS version and instance count. In this case, the role has a single instance.

![Information about the role](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-the-role-by-adding-more-instances"></a>Scale out the role by adding more instances

To scale out your role, pass the desired number of instances as the **Count** parameter to the **Set-AzureRole** cmdlet:

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

The cmdlet blocks momentarily while the new instances are provisioned and started. During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see the new target instance count. And if you inspect the role status in the portal, you should see the new instance starting up:

![VM instance starting in portal](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

Once the new instances have started, the cmdlet will return successfully:

![Role instance increase success](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-the-role-by-removing-instances"></a>Scale in the role by removing instances

You can scale in a role by removing instances in the same way. Set the **Count** parameter on **Set-AzureRole** to the number of instances you want to have after the scale in operation is complete.

## <a name="next-steps"></a>Next steps

It is not possible to configure auto-scale for cloud services from PowerShell. To do that, see [How to auto scale a cloud service](cloud-services-how-to-scale-portal.md).
