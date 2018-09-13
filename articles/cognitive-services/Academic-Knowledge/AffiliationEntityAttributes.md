---
title: Affiliation entity attributes in the Academic Knowledge API | Microsoft Docs
description: Learn the attributes you can use with the Affiliation entity in the Academic Knowledge API in Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.component: academic-knowledge
ms.topic: article
ms.date: 03/23/2017
ms.author: alch
ms.openlocfilehash: a0ec67cb811ca207b3d038028491da2516028f0b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44793824"
---
# <a name="affiliation-entity"></a>Affiliation Entity

<sub> *Following attributes are specific to affiliation entity. (Ty = '5') </sub>

Name    |Description                            |Type       | Operations
------- | ------------------------------------- | --------- | ----------------------------
Id      |Entity ID                              |Int64      |Equals
AfN     |Affiliation normalized name        |String     |Equals
DAfN    |Affiliation display name       |String     |none
CC      |Affiliation total citation count           |Int32      |none  
ECC     |Affiliation total estimated citation count |Int32      |none

## <a name="extended-metadata-attributes"></a>Extended Metadata Attributes ##

Name    | Description               
--------|---------------------------    
PC      |Affiliation's paper count