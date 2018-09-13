---
title: Manage speed and concurrency of your encoding with Azure Media Services | Microsoft Docs
description: This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks with Azure Media Services.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: c4bfe2a1f1d22a3b23f381a7afe600d1cfc962b2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670423"
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a>Manage speed and concurrency of your encoding

This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.

## <a name="overview"></a>Overview

In Media Services, a **Reserved Unit Type** determines the speed with which your media processing tasks are processed. You can pick between the following reserved unit types: **S1**, **S2**, or **S3**. For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type. The [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.

In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units**. The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account. For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks to be processed. The remaining tasks will wait in the queue and will get picked up for processing sequentially when a running task finishes. If an account does not have any reserved units provisioned, then tasks will be picked up sequentially. In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.

For detailed information and examples that show how to scale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.

## <a name="next-step"></a>Next step

[Scale encoding units](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a>Media Services learning paths
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

