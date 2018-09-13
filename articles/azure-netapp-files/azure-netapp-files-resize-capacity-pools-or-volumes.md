---
title: Resize the capacity pool or a volume for Azure NetApp Files  | Microsoft Docs
description: Describes how to change the size of a capacity pool or a volume.
services: azure-netapp-files
documentationcenter: ''
author: b-juche
manager: ''
editor: ''
ms.assetid: ''
ms.service: azure-netapp-files
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 04/03/2018
ms.author: b-juche
ms.openlocfilehash: 72da85fb7296d02bc6d5f7fcd3279953c312c920
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867780"
---
# <a name="resize-a-capacity-pool-or-a-volume"></a>Resize a capacity pool or a volume
You can change the size of a capacity pool or a volume as necessary. 

## <a name="resize-the-capacity-pool"></a>Resize the capacity pool 

You can change the capacity pool size in 4-TiB increments or decrements. Resizing the capacity pool changes the purchased Azure NetApp Files capacity.

1. From the Manage NetApp Account blade, click the capacity pool that you want to resize. 
2. Right-click the capacity pool name or click the "…" icon at the end of the capacity pool’s row to display the context menu. 
3. Use the context menu options to resize or delete the capacity pool.

## <a name="resize-a-volume"></a>Resize a volume

You can change the size of a volume as necessary. A volume's capacity consumption counts against its pool's provisioned capacity.

1. From the Manage NetApp Account blade, click **Volumes**. 
2. Right-click the name of the volume that you want to resize or click the "…" icon at the end of the volume's row to display the context menu.
3. Use the context menu options to resize or delete the volume.

