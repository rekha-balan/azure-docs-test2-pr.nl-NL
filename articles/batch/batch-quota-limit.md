---
title: Service quotas and limits for Azure Batch | Microsoft Docs
description: Learn about default Azure Batch quotas, limits, and constraints, and how to request quota increases
services: batch
documentationcenter: ''
author: tamram
manager: timlt
editor: ''
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f6308101de57274796e0533317359dc1133f431
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555121"
---
# <a name="batch-service-quotas-and-limits"></a>Batch service quotas and limits

As with other Azure services, there are limits on certain resources associated with the Batch service. Many of these limits are default quotas applied by Azure at the subscription or account level. This article discusses those defaults, and how you can request quota increases.

Keep these quotas in mind as you are designing and scaling up your Batch workloads. For example, if your pool isn't reaching the target number of compute nodes you've specified, you might have reached the core quota limit for your Batch account.

You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in the same subscription, but in different Azure regions.

If you plan to run production workloads in Batch, you may need to increase one or more of the quotas above the default. If you want to raise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.

> [!NOTE]
> A quota is a credit limit, not a capacity guarantee. If you have large-scale capacity needs, please contact Azure support.
> 
> 

## <a name="resource-quotas"></a>Resource quotas
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="other-limits"></a>Other limits
| **Resource** | **Maximum Limit** |
| --- | --- |
| [Concurrent tasks](batch-parallel-node-tasks.md) per compute node |4 x number of node cores |
| [Applications](batch-application-packages.md) per Batch account |20 |
| Application packages per application |40 |
| Application package size (each) |Approx. 195GB<sup>1</sup> |

<sup>1</sup> Azure Storage limit for maximum block blob size

## <a name="view-batch-quotas"></a>View Batch quotas
View your Batch account quotas in the [Azure portal][portal].

1. Select **Batch accounts** in the portal, then select the Batch account you're interested in.
2. Select **Properties** on the Batch account's menu blade
3. The Properties blade displays the **quotas** currently applied to the Batch account
   
    ![Batch account quotas][account_quotas]

## <a name="increase-a-quota"></a>Increase a quota
Follow these steps to request a quota increase using the [Azure portal][portal].

1. Select the **Help + support** tile on your portal dashboard, or the question mark (**?**) in the upper-right corner of the portal.
2. Select **New support request** > **Basics**.
3. On the **Basics** blade:
   
    a. **Issue Type** > **Quota**
   
    b. Select your subscription.
   
    c. **Quota type** > **Batch**
   
    d. **Support plan** > **Quota support - Included**
   
    Click **Next**.
4. On the **Problem** blade:
   
    a. Select a **Severity** according to your [business impact][support_sev].
   
    b. In **Details**, specify each quota you want to change, the Batch account name, and the new limit.
   
    Click **Next**.
5. On the **Contact information** blade:
   
    a. Select a **Preferred contact method**.
   
    b. Verify and enter the required contact details.
   
    Click **Create** to submit the support request.

Once you've submitted your support request, Azure support will contact you. Note that completing the request can take up to 2 business days.

## <a name="related-topics"></a>Related topics
* [Create an Azure Batch account using the Azure portal](batch-account-create-portal.md)
* [Azure Batch feature overview](batch-api-basics.md)
* [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-quota-limit/accountquota_portal.PNG

