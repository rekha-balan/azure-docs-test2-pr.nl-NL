---
title: Export your Azure subscription top level information | Microsoft Docs
description: Describes how you can view all Azure subscription IDs associated with your account.
keywords: ''
services: billing
documentationcenter: ''
author: adpick
manager: adpick
editor: ''
tags: billing
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/15/2018
ms.author: adpick
ms.openlocfilehash: 7bc9f4df6e98dd86283c4389466b13b8f6bb4d15
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868117"
---
# <a name="export-and-view-your-top-level-subscription-information"></a><span data-ttu-id="666e8-103">Export and view your top-level Subscription information</span><span class="sxs-lookup"><span data-stu-id="666e8-103">Export and view your top-level Subscription information</span></span>
<span data-ttu-id="666e8-104">If you need to view the set of subscription IDs associated with your user credentials, [download a .json file with your subscription information from the Azure Account Center](http://account.azure.com/subscriptions/download).</span><span class="sxs-lookup"><span data-stu-id="666e8-104">If you need to view the set of subscription IDs associated with your user credentials, [download a .json file with your subscription information from the Azure Account Center](http://account.azure.com/subscriptions/download).</span></span>

[!INCLUDE [gdpr-dsr-and-stp-note](../../includes/gdpr-dsr-and-stp-note.md)]

<span data-ttu-id="666e8-105">The downloaded .json file provides the following information:</span><span class="sxs-lookup"><span data-stu-id="666e8-105">The downloaded .json file provides the following information:</span></span>
- <span data-ttu-id="666e8-106">Email: The email address associated with your account.</span><span class="sxs-lookup"><span data-stu-id="666e8-106">Email: The email address associated with your account.</span></span>
- <span data-ttu-id="666e8-107">Puid: The unique identifier associated with your billing account.</span><span class="sxs-lookup"><span data-stu-id="666e8-107">Puid: The unique identifier associated with your billing account.</span></span>
- <span data-ttu-id="666e8-108">SubscriptionIds: A list of subscriptions that belong to your account, enumerated by subscription ID.</span><span class="sxs-lookup"><span data-stu-id="666e8-108">SubscriptionIds: A list of subscriptions that belong to your account, enumerated by subscription ID.</span></span>

### <a name="subscriptionsjson-sample"></a><span data-ttu-id="666e8-109">subscriptions.json sample</span><span class="sxs-lookup"><span data-stu-id="666e8-109">subscriptions.json sample</span></span>
~~~~
{
  "Email":"admin@contoso.com",
  "Puid":"00052xxxxxxxxxxx",
  "SubscriptionIds":[
    "38124d4d-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "7c8308f1-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "39a25f2b-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "52ec2489-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "e42384b2-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "90757cdc-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
  ]
}
~~~~
