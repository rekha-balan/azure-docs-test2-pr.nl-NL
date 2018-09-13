---
title: Override HTTP behavior using the Azure CDN rules engine | Microsoft Docs
description: The rules engine allows you to customize how HTTP requests are handled by Azure CDN, such as blocking the delivery of certain types of content, define a caching policy, and modify HTTP headers.
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: c246be51526e582b8d9d7092213689dbe1cfe407
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562976"
---
# <a name="override-http-behavior-using-the-azure-cdn-rules-engine"></a>Override HTTP behavior using the Azure CDN rules engine
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Overview
The rules engine allows you to customize how HTTP requests are handled, such as blocking the delivery of certain types of content, defining a caching policy, and modifying HTTP headers.  This tutorial will demonstrate creating a rule that will change the caching behavior of CDN assets.  There's also video content available in the "[See also](#see-also)" section.

   > [!TIP] 
   > For a reference to the syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).
   > 


## <a name="tutorial"></a>Tutorial
1. From the CDN profile blade, click the **Manage** button.
   
    ![CDN profile blade manage button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-rules-engine/cdn-manage-btn.png)
   
    The CDN management portal opens.
2. Click on the **HTTP Large** tab, followed by **Rules Engine**.
   
    Options for a new rule are displayed.
   
    ![CDN new rule options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > The order in which multiple rules are listed affects how they are handled. A subsequent rule may override the actions specified by a previous rule.
   > 
   > 
3. Enter a name in the **Name / Description** textbox.
4. Identify the type of requests the rule will apply to.  By default, the **Always** match condition is selected.  You'll use **Always** for this tutorial, so leave that selected.
   
   ![CDN match condition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > There are many types of match conditions available in the dropdown.  Clicking on the blue informational icon to the left of the match condition will explain the currently selected condition in detail.
   > 
   >  For the full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).
   >  
   > For the full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).
   > 
   > 
5. Click the **+** button next to **Features** to add a new feature.  In the dropdown on the left, select **Force Internal Max-Age**.  In the textbox that appears, enter **300**.  Leave the remaining default values.
   
   ![CDN feature](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > As with match conditions, clicking the blue informational icon to the left of the new feature will display details about this feature.  In the case of **Force Internal Max-Age**, we are overriding the asset's **Cache-Control** and **Expires** headers to control when the CDN edge node will refresh the asset from the origin.  Our example of 300 seconds means the CDN edge node will cache the asset for 5 minutes before refreshing the asset from its origin.
   > 
   > For the full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).
   > 
   > 
6. Click the **Add** button to save the new rule.  The new rule is now awaiting approval. Once it has been approved, the status will change from **Pending XML** to **Active XML**.
   
   > [!IMPORTANT]
   > Rules changes may take up to 90 minutes to propagate through the CDN.
   > 
   > 

## <a name="see-also"></a>See also
* [Azure CDN Overview](cdn-overview.md)
* [Rules Engine Reference](cdn-rules-engine-reference.md)
* [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md)
* [Rules Engine Conditional Expressions](cdn-rules-engine-reference-conditional-expressions.md)
* [Rules Engine Features](cdn-rules-engine-reference-features.md)
* [Overriding default HTTP behavior using the rules engine](cdn-rules-engine.md)
* [Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)



