---
title: Publish an app in Azure RemoteApp | Microsoft Docs
description: Learn how to publish applications and resources in Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4cd4d35f44320ac57f015b5444985e8b4976ccf0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554431"
---
# <a name="how-to-publish-an-app-in-remoteapp"></a>How to publish an app in RemoteApp
> [!IMPORTANT]
> Azure RemoteApp is being discontinued on August 31, 2017. Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.
> 
> 

After you create your RemoteApp collection, you need to publish the apps or resources that you want to make available for your users. The template images provided with your subscription only have a few apps published by default - to share the other apps, you need to publish them.

> [!NOTE]
> Do you need to update an app? You'll need to [update the image](remoteapp-update.md) first.
> 
> 

On the **Publishing** tab in the portal, click **Publish**. You can either add an app from your template image's **Start** menu or provide the path to where the app is installed on the template image. If you choose to add from the **Start** menu, choose the app to publish from the list. If you choose to provide the path to the app, enter a name for the app and the path to the app. Use variables in the path - for example, "%systemdrive%" instead of "c:\".

> [!NOTE]
> If you want to add your app from the **Start** menu, you need to have *added that app to the **Start** menu on your template image.* Otherwise, RemoteApp will only see what *is* on the **Start** menu, and you will be confused. 
> 
> To make sure your app is in the **Start** menu, place a shortcut file - **.lnk** - inside the %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.
> 
> If you forgot to add the app to the **Start** menu when you created the template, choose to add the path to the app. (Or recreate your template image, but that's quite a bit more work.)
> 
> 

