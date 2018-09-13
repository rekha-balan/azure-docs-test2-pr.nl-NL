---
title: Conference Series entity attributes in the Academic Knowledge API | Microsoft Docs
description: Learn about the attributes you can use with the Conference Series entity in Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/23/2017
ms.author: alch
ms.openlocfilehash: 58d63c6a93c011d9a1460f25f8cb85f8b5f1c05b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671152"
---
# <a name="conference-series-entity"></a>Conference Series Entity

<sub> *Below attributes are specific to conference series entity. (Ty = '3') </sub>

Name    |Description                            |Type       | Operations
------- | ------------------------------------- | --------- | ----------------------------
Id      |Entity ID                              |Int64      |Equals
CN      |Conference series normalized name      |String     |Equals
DCN     |Conference series display name         |String     |none
CC      |Conference series total citation count         |Int32      |none  
ECC     |Conference series total estimated citation count   |Int32      |none
F.FId   |Field of study entity ID associated with the conference series |Int64  | Equals
F.FN    |Field of study name associated with the conference series  | Equals,<br/>StartsWith
SSD     |Satori data                            |String     |none
