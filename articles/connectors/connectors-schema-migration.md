---
title: How to migrate logic apps to schema version 2015-08-01-preview | Microsoft Docs
description: You can easily migrate your logic apps to the latest schema version. Just follow these steps.
services: logic-apps
documentationcenter: ''
author: MSFTMAN
manager: erikre
editor: ''
tags: connectors
ms.assetid: 3e177e49-fd69-43e9-9b9b-218abb250c31
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: deonhe
ms.openlocfilehash: f719c1c94ab2c515d572ee3578fc7a29eeadf7d6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564493"
---
# <a name="how-to-migrate-logic-apps-to-schema-version-2015-08-01-preview"></a>How to migrate logic apps to schema version 2015-08-01-preview
To move your existing logic apps to the new schema, do the following:  

1. Open your logic app in the Azure portal  
2. Click Update Schema:
   
   ![API Icon][step1]   
   The Update Schema page displays and provides a link to a document that provide details on the improvements in the new schema: ![API Icon][step2]

> [!NOTE]
> When you select **Update Schema**, we automatically run the migration steps and provide the code output for you. You can use this to update your definition, however, ensure you follow good coding practices such as those outlined in the **Best practices** section below.
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-to-the-latest-schema-version"></a>Best practices when migrating your Logic apps to the latest schema version:
* Copy the migrated script to a new Logic App - don't overwrite the old one until you've completed your testing and confirmed the migrated app works as expected.
* Test your Logic app **before** putting in production
* After migration completes, start updating your Logic apps to use the [managed APIs](apis-list.md) where possible. For example, you can start using Dropbox v2, whereever you are using DropBox v1.

## <a name="whats-next"></a>What's next
* [Learn how to manually migrate your Logic apps](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-schema-migration/migrateschema1.png
[step2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-schema-migration/migrateschema2.png







