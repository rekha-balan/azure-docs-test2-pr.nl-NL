---
title: Affiliation entity attributes in the Academic Knowledge API | Microsoft Docs
description: Learn the attributes you can use with the Affiliation entity in the Academic Knowledge API in Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/23/2017
ms.author: alch
ms.openlocfilehash: cffceaf1b0b9dc15d0cc8d58877b5e6f68055433
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549445"
---
# <a name="affiliation-entity"></a>Affiliation Entity

<sub> *Below attributes are specific to affiliation entity. (Ty = '5') </sub>

Name    |Description                            |Type       | Operations
------- | ------------------------------------- | --------- | ----------------------------
Id      |Entity ID                              |Int64      |Equals
AfN     |Affiliation normalized name        |String     |Equals
DAfN    |Affiliation display name       |String     |none
CC      |Affiliation total citation count           |Int32      |none  
ECC     |Affiliation total estimated citation count |Int32      |none
SSD     |Satori data                            |String     |none