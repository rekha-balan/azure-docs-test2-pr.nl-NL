---
title: Journal entity attributes in the Academic Knowledge API | Microsoft Docs
description: Learn the attributes you can use with the Journal entity in the Academic Knowledge API in Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.component: academic-knowledge
ms.topic: article
ms.date: 03/23/2017
ms.author: alch
ms.openlocfilehash: e782c57b8ac57028e070c16382c53ec76666e94d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44793590"
---
# <a name="journal-entity"></a>Journal Entity

<sub> *Following attributes are specific to journal entity. (Ty = '2') </sub>

Name    |Description                            |Type       | Operations
------- | ------------------------------------- | --------- | ----------------------------
Id      |Entity ID                              |Int64      |Equals
DJN     |Journal normalized name                |String     |none
JN      |Journal display name                   |String     |Equals
CC      |Journal total citation count           |Int32      |none  
ECC     |Journal total estimated citation count |Int32      |none