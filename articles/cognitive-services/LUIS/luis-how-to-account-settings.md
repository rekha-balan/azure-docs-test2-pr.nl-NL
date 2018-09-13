---
title: Manage your account settings in LUIS | Microsoft Docs
description: Use LUIS website to manage your account settings.
titleSuffix: Azure
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 07/08/2018
ms.author: diberry
ms.openlocfilehash: 73e90e5ae86db2c2c4625762b285f8c86f0e241b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868851"
---
# <a name="manage-account-and-authoring-key"></a>Manage account and authoring key
The two key pieces of information for a LUIS account are the user account and the authoring key. Your login information is managed at [account.microsoft.com](https://account.microsoft.com). Your authoring key is managed from the [LUIS](luis-reference-regions.md) website **Settings** page. 

## <a name="authoring-key"></a>Authoring key

This single, region-specific authoring key, on the **Settings** page, allows you to author all your apps from the [LUIS](luis-reference-regions.md) website as well as the [authoring APIs](https://aka.ms/luis-authoring-api). As a convenience, the authoring key is allowed to make a [limited](luis-boundaries.md) number of endpoint queries each month. 

![LUIS Settings page](./media/luis-how-to-account-settings/account-settings.png)

The authoring key is used for any apps you own as well as any apps you are listed as a collaborator.

## <a name="authoring-key-regions"></a>Authoring key regions
The authoring key is specific to the [authoring region](luis-reference-regions.md#publishing-regions). The key does not work in a different region. 

## <a name="reset-authoring-key"></a>Reset authoring key
If your authoring key is compromised, reset the key. The key is reset on all your apps in the [LUIS](luis-reference-regions.md) website. If you author your apps via the authoring APIs, you need to change the value of `Ocp-Apim-Subscription-Key` to the new key. 

## <a name="delete-account"></a>Delete account
See [Data storage and removal](luis-concept-data-storage.md#accounts) for information about what data is deleted when you delete your account. 

## <a name="next-steps"></a>Next steps

Learn more about your [authoring key](luis-concept-keys.md#authoring-key). 

