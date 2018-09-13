---
title: Data storage in LUIS - Language Understanding
titleSuffix: Azure Cognitive Services
description: Learn how data is stored in Language Understanding (LUIS). LUIS stores data encrypted in an Azure data store corresponding to the region specified by the key.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 05/08/2018
ms.author: diberry
ms.openlocfilehash: a34426efd998a5573277e9129b832f5167c5da5e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855847"
---
# <a name="data-storage-and-removal-in-language-understanding-luis-cognitive-services"></a>Data storage and removal in Language Understanding (LUIS) Cognitive Services
LUIS stores data encrypted in an Azure data store corresponding to the region specified by the key. This data is stored for 30 days. 

## <a name="export-and-delete-app"></a>Export and delete app
Users have full control over [exporting](luis-how-to-start-new-app.md#export-app) and [deleting](luis-how-to-start-new-app.md#delete-app) the app. 

## <a name="utterances-in-an-intent"></a>Utterances in an intent
Delete example utterances used for training [LUIS](luis-reference-regions.md). If you delete an example utterance from your LUIS app, it is removed from the LUIS web service and is unavailable for export.

## <a name="utterances-in-review"></a>Utterances in review
You can delete utterances from the list of user utterances that LUIS suggests in the **[Review endpoint utterances page](luis-how-to-review-endoint-utt.md)**. Deleting utterances from this list prevents them from being suggested, but doesn't delete them from logs.

## <a name="accounts"></a>Accounts
If you delete an account, all apps are deleted, along with their example utterances and logs. The data is retained for 60 days before the account and data are deleted permanently.

Deleting account is available from the **Settings** page. Select your account name in the top right navigation bar to get to the **Settings** page.

## <a name="data-inactivity-as-an-expired-subscription"></a>Data inactivity as an expired subscription
For the purposes of data retention and deletion, an inactive LUIS app may at _Microsoft’s discretion_ be treated as an expired subscription. An app is considered inactive if it meets the following criteria for the last 90 days: 

* Has had **no** calls made to it.
* Has not been modified.
* Does not have a current key assigned to it.
* Has not had a user sign in to it.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Learn about exporting and deleting an app](luis-how-to-start-new-app.md)