---
title: Auto scale a cloud service in the portal (classic portal) | Microsoft Docs
description: Learn how to use the portal to configure auto scale rules for a cloud service web role or worker role in Azure.
services: cloud-services
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: adegeo
ms.openlocfilehash: 351ef4e18793777ae17fe1d22df45e85a5fb3833
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563157"
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-portal"></a>How to configure auto scaling for a Cloud Service in the portal
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-scale-portal.md)
> * [Azure classic portal](cloud-services-how-to-scale.md)

Conditions can be set for a cloud service worker role that trigger a scale in or out operation. The conditions for the role can be based on the CPU, disk, or network load of the role. You can also set a condition based on a message queue or the metric of some other Azure resource associated with your subscription.

> [!NOTE]
> This article focuses on Cloud Service web and worker roles. When you create a virtual machine (classic) directly, it is hosted in a cloud service. You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.

## <a name="considerations"></a>Considerations
You should consider the following information before you configure scaling for your application:

* Scaling is affected by core usage.

    Larger role instances use more cores. You can scale an application only within the limit of cores for your subscription. For example, say your subscription has a limit of 20 cores. If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores. For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).

* You can scale based on a queue message threshold. For more information about how to use queues, see [How to use the Queue Storage Service](../storage/storage-dotnet-how-to-use-queues.md).

* You can also scale other resources associated with your subscription.

* To enable high availability of your application, you should ensure that it is deployed with two or more role instances. For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).

> [!WARNING]
> Automatic scaling only works with Classic Azure Storage Accounts. It does not work with Azure Resource Manager Storage Accounts.


## <a name="where-scale-is-located"></a>Where scale is located
After you select your cloud service, you should have the cloud service blade visible.

1. On the cloud service blade, on the **Roles and Instances** tile, select the name of the cloud service.   
   **IMPORTANT**: Make sure to click the cloud service role, not the role instance that is below the role.
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/roles-instances.png)
2. Select the **scale** tile.
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a>Automatic scale
You can configure scale settings for a role with either two modes **manual** or **automatic**. Manual is as you would expect, you set the absolute count of instances. Automatic however allows you to set rules that govern how and by how much you should scale.

Set the **Scale by** option to **schedule and performance rules**.

![Cloud services scale settings with profile and rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. An existing profile.
2. Add a rule for the parent profile.
3. Add another profile.

Select **Add Profile**. The profile determines which mode you want to use for the scale: **always**, **recurrence**, **fixed date**.

After you have configured the profile and rules, select the **Save** icon at the top.

#### <a name="profile"></a>Profile
The profile sets minimum and maximum instances for the scale, and also when this scale range is active.

* **Always**
  
    Always keep this range of instances available.  
  
    ![Cloud service that always scale](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/select-always.png)
* **Recurrence**
  
    Choose a set of days of the week to scale.
  
    ![Cloud service scale with a recurrence schedule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/select-recurrence.png)
* **Fixed Date**
  
    A fixed date range to scale the role.
  
    ![CLoud service scale with a fixed date](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/select-fixed.png)

After you have configured the profile, select the **OK** button at the bottom of the profile blade.

#### <a name="rule"></a>Rule
Rules are added to a profile and represent a condition that triggers the scale. 

The rule trigger is based on a metric of the cloud service (CPU usage, disk activity, or network activity) to which you can add a conditional value. Additionally you can have the trigger based on a message queue or the metric of some other Azure resource associated with your subscription.

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/rule-settings.png)

After you have configured the rule, select the **OK** button at the bottom of the rule blade.

## <a name="back-to-manual-scale"></a>Back to manual scale
Navigate to the [scale settings](#where-scale-is-located) and set the **Scale by** option to **an instance count that I enter manually**.

![Cloud services scale settings with profile and rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/manual-basics.png)

This setting removes automated scaling from the role and then you can set the instance count directly. 

1. The scale (manual or automated) option.
2. A role instance slider to set the instances to scale to.
3. Instances of the role to scale to.

After you have configured the scale settings, select the **Save** icon at the top.









