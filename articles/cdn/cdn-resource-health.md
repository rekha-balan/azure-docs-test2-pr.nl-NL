---
title: Monitor the health of Azure CDN resources| Microsoft Docs
description: Learn how to monitor the health of your Azure CDN resources using Azure Resource Health.
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: ''
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: b560eb877c57ebdcc02b7a9457c44a4acff3851e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555481"
---
# <a name="monitor-the-health-of-azure-cdn-resources"></a>Monitor the health of Azure CDN resources
  
Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).  You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.

>[!IMPORTANT] 
>Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.  Azure CDN resource health does not verify individual CDN endpoints.
>
>The signals that feed Azure CDN resource health may be up to 15 minutes delayed.

## <a name="how-to-find-azure-cdn-resource-health"></a>How to find Azure CDN resource health

1. In the [Azure portal](https://portal.azure.com), browse to your CDN profile.

2. Click the **Settings** button.

    ![Settings button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-resource-health/cdn-profile-settings.png)

3. Under *Support + troubleshooting*, click **Resource health**.

    ![CDN resource health](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
>You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.  You can quickly get to *Help + support* by clicking the circled **?** in the upper right corner of the portal.
>
> ![Help + support](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a>Azure CDN-specific messages

Statuses related to Azure CDN resource health can be found below.

|Message | Recommended Action |
|---|---|
|You may have stopped, removed, or misconfigured one or more of your CDN endpoints | You may have stopped, removed, or misconfigured one or more of your CDN endpoints.|
|We are sorry, the CDN management service is currently unavailable | Check back here for status updates; If your problem persists after the expected resolution time, contact support.|
|We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers | Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support. |
|We're sorry, CDN endpoint configuration changes are experiencing propagation delays | Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.|
|We're sorry, we are experiencing issues loading the supplemental portal | Check back here for status updates; If your problem persists after the expected resolution time, contact support.|
We are sorry, we are experiencing issues with some of our CDN providers | Check back here for status updates; If your problem persists after the expected resolution time, contact support. |

## <a name="next-steps"></a>Next steps

- [Read an overview of Azure resource health](../resource-health/resource-health-overview.md)
- [Troubleshoot issues with CDN compression](./cdn-troubleshoot-compression.md)
- [Troubleshoot issues with 404 errors](./cdn-troubleshoot-endpoint.md)


