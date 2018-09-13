---
title: Migrate apps to latest schema - Azure Logic Apps | Microsoft Docs
description: How to migrate your logic apps to the latest schema version
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.assetid: 3e177e49-fd69-43e9-9b9b-218abb250c31
ms.topic: article
ms.date: 08/25/2018
ms.openlocfilehash: 8a6925d79b225a34d980472d4fb3241ab9eb1017
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784061"
---
# <a name="migrate-logic-apps-to-latest-schema-version"></a><span data-ttu-id="54f1f-103">Migrate logic apps to latest schema version</span><span class="sxs-lookup"><span data-stu-id="54f1f-103">Migrate logic apps to latest schema version</span></span>

<span data-ttu-id="54f1f-104">To move your existing logic apps to the newest schema, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="54f1f-104">To move your existing logic apps to the newest schema, follow these steps:</span></span> 

1. <span data-ttu-id="54f1f-105">In the [Azure portal](https://portal.azure.com), open your logic app in the Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="54f1f-105">In the [Azure portal](https://portal.azure.com), open your logic app in the Logic App Designer.</span></span>

2. <span data-ttu-id="54f1f-106">On your logic app's menu, choose **Overview**.</span><span class="sxs-lookup"><span data-stu-id="54f1f-106">On your logic app's menu, choose **Overview**.</span></span> <span data-ttu-id="54f1f-107">On the toolbar, choose **Update Schema**.</span><span class="sxs-lookup"><span data-stu-id="54f1f-107">On the toolbar, choose **Update Schema**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="54f1f-108">When you chooose **Update Schema**, Azure Logic Apps automatically runs the migration steps and provides the code output for you.</span><span class="sxs-lookup"><span data-stu-id="54f1f-108">When you chooose **Update Schema**, Azure Logic Apps automatically runs the migration steps and provides the code output for you.</span></span> <span data-ttu-id="54f1f-109">You can use this output for updating your logic app definition.</span><span class="sxs-lookup"><span data-stu-id="54f1f-109">You can use this output for updating your logic app definition.</span></span> <span data-ttu-id="54f1f-110">However, make sure you follow best practices as described in the following **Best practices** section.</span><span class="sxs-lookup"><span data-stu-id="54f1f-110">However, make sure you follow best practices as described in the following **Best practices** section.</span></span>

   ![Update Schema](./media/connectors-schema-migration/update-schema.png)

   <span data-ttu-id="54f1f-112">The Update Schema page appears and shows a link to a document that describes the improvements in the new schema.</span><span class="sxs-lookup"><span data-stu-id="54f1f-112">The Update Schema page appears and shows a link to a document that describes the improvements in the new schema.</span></span>

## <a name="best-practices"></a><span data-ttu-id="54f1f-113">Best practices</span><span class="sxs-lookup"><span data-stu-id="54f1f-113">Best practices</span></span>

<span data-ttu-id="54f1f-114">Here are some best practices for migrating your logic apps to the latest schema version:</span><span class="sxs-lookup"><span data-stu-id="54f1f-114">Here are some best practices for migrating your logic apps to the latest schema version:</span></span>

* <span data-ttu-id="54f1f-115">Copy the migrated script to a new logic app.</span><span class="sxs-lookup"><span data-stu-id="54f1f-115">Copy the migrated script to a new logic app.</span></span> <span data-ttu-id="54f1f-116">Don't overwrite the old version until you complete your testing and confirm that your migrated app works as expected.</span><span class="sxs-lookup"><span data-stu-id="54f1f-116">Don't overwrite the old version until you complete your testing and confirm that your migrated app works as expected.</span></span>

* <span data-ttu-id="54f1f-117">Test your logic app **before** putting in production.</span><span class="sxs-lookup"><span data-stu-id="54f1f-117">Test your logic app **before** putting in production.</span></span>

* <span data-ttu-id="54f1f-118">After you finish migration, start updating your logic apps to use the [managed APIs](../connectors/apis-list.md) where possible.</span><span class="sxs-lookup"><span data-stu-id="54f1f-118">After you finish migration, start updating your logic apps to use the [managed APIs](../connectors/apis-list.md) where possible.</span></span> <span data-ttu-id="54f1f-119">For example, start using Dropbox v2 everywhere that you use DropBox v1.</span><span class="sxs-lookup"><span data-stu-id="54f1f-119">For example, start using Dropbox v2 everywhere that you use DropBox v1.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54f1f-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="54f1f-120">Next steps</span></span>

* <span data-ttu-id="54f1f-121">Learn how to [manually migrate your Logic apps](../logic-apps/logic-apps-schema-2015-08-01.md)</span><span class="sxs-lookup"><span data-stu-id="54f1f-121">Learn how to [manually migrate your Logic apps](../logic-apps/logic-apps-schema-2015-08-01.md)</span></span>
