---
title: Understand versioning in LUIS - Azure | Microsoft Docs
description: Learn how to use versions to manage changes in Language Understanding (LUIS)
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 03/13/2018
ms.author: diberry
ms.openlocfilehash: 17abe383d3074d636605c3b1b91927f89f7dd896
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966124"
---
# <a name="versions"></a>Versions
Create different models of the same app with [versions](luis-how-to-manage-versions.md). 

## <a name="version-id"></a>Version ID
The version ID consists of characters, digits or '.' and cannot be longer than 10 characters.

## <a name="initial-version"></a>Initial version
The initial version (0.1) is the default active version. 

## <a name="active-version"></a>Active version
To [set a version](luis-how-to-manage-versions.md#set-active-version) as the active means it is currently edited and tested in the [LUIS](luis-reference-regions.md) website. Set a version as active to access its data, make updates, as well as to test and publish it.

The name of the currently active version is displayed in the top, left panel after the app name. 

[ ![Change active version](./media/luis-concept-version/version-in-nav-bar-inline.png) ](./media/luis-concept-version/version-in-nav-bar-expanded.png#lightbox)

## <a name="versions-and-publishing-slots"></a>Versions and publishing slots
You publish to either the stage and product slots. Each slot can have a different version or the same version. This is useful for verifying changes between model versions via the endpoint, which is available to bots or other LUIS calling applications. 

## <a name="clone-a-version"></a>Clone a version
Clone a version to create a copy of an existing version and save it as a new version. Clone a version to use the same content of the existing version as a starting point for the new version. Once you clone a version, the new version becomes the **active** version. 

## <a name="import-and-export-a-version"></a>Import and export a version
You can import a version at the app level. That version becomes the active version and used the version ID in the "versionId" property of the app file. You can also import at the version level into an existing app. The new version becomes the active version. 

You can export a version at the app level or you can export a version at the version level. The only difference is that the app-level exported version is the currently active version while at the version level, you can choose any version to export on the **[Settings](luis-how-to-manage-versions.md)** page. 

The exported file does not contain machine-learned information because the app is retrained after it is imported. The exported file does not contain collaborators -- you need to add these back once the version is imported into the new app.

## <a name="export-each-version-as-app-backup"></a>Export each version as app backup
In order to back up your LUIS app, export each version on the **[Settings](luis-how-to-manage-versions.md)** page.

## <a name="delete-a-version"></a>Delete a version
You can delete all versions except the active version from the Versions list on Settings page. 

## <a name="version-availability-at-the-endpoint"></a>Version availability at the endpoint
Trained versions are not automatically available at your app [endpoint](luis-glossary.md#endpoint). You must [publish](luis-how-to-publish-app.md) or republish a version in order for it to be available at your app endpoint. You can publish to **Staging** and **Production**, giving you up to two versions of the app available at the endpoint. If you need more versions of the app available at an endpoint, you should export the version and reimport to a new app. The new app has a different app ID.

## <a name="collaborators"></a>Collaborators
The owner and all [collaborators](luis-how-to-collaborate.md) have full access to all versions of the app.

## <a name="next-steps"></a>Next steps

See how to add [versioning](luis-how-to-manage-versions.md) on the app settings page. 

Learn how to design [intents](luis-concept-intent.md) into the model.