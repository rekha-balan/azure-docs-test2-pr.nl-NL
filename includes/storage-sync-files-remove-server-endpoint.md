---
title: include file
description: include file
services: storage
author: wmgries
ms.service: storage
ms.topic: include
ms.date: 05/31/2018
ms.author: wgries
ms.custom: include file
ms.openlocfilehash: 96d65b34b30f81ed376e76cbe5eee2955691a59b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868283"
---
No: removing a server endpoint is not like rebooting a server! Removing and recreating the server endpoint is almost never an appropriate solution to fixing issues with sync, cloud tiering, or other aspects of Azure File Sync. Removing a server endpoint is a destructive operation, and may result in data loss in the case that tiered files exist outside of the server endpoint namespace (see [Why do tiered files exist outside of the server endpoint namespace](../articles/storage/files/storage-files-faq.md#afs-tiered-files-out-of-endpoint) for more information) or in inaccessible files for tiered files existing within the server endpoint namespace. These issues will not resolve when the server endpoint is recreated. Tiered files may exist within your server endpoint namespace even if you never had cloud tiering enabled. We therefore recommend that you do not remove the server endpoint unless you would like to stop using Azure File Sync with this particular folder or have been explicitly instructed to do so by a Microsoft engineer. For more information on remove server endpoints, see [Remove a server endpoint](../articles/storage/files/storage-sync-files-server-endpoint.md#remove-a-server-endpoint).    