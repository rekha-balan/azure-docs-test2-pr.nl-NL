---
title: Field of Study entity attributes in the Academic Knowledge API | Microsoft Docs
description: Learn the attributes you can use with the Field of Study entity in the Academic Knowledge API in Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/31/2017
ms.author: alch
ms.openlocfilehash: 27c1f15e09b80166ff3daef2899b21a9a21a1f33
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562986"
---
# <a name="field-of-study-entity"></a>Field Of Study Entity

<sub> *Below attributes are specific to field of study entity. (Ty = '6') </sub>

Name    |Description                            |Type       | Operations
------- | ------------------------------------- | --------- | ----------------------------
Id      |Entity ID                              |Int64      |Equals
FN      |Field of study normalized name         |String     |Equals
DFN     |Field of study display name            |String     |none
CC      |Field of study total citation count    |Int32      |none  
ECC     |Field of total estimated citation count|Int32      |none
FL      |Level in fields of study hierarchy     |Int32      |Equals, <br/>IsBetween
FP.FN   |Parent field of study name             |String     |Equals
FP.FId  |Parent field of study ID               |Int64      |Equals
SSD     |Satori data                            |String     |none