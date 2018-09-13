---
title: Journal entity attributes in the Academic Knowledge API | Microsoft Docs
description: Learn the attributes you can use with the Journal entity in the Academic Knowledge API in Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/23/2017
ms.author: alch
ms.openlocfilehash: 000d6b38253608fc1e91d3f1116eaf5098cb97e9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662479"
---
# <a name="journal-entity"></a>Journal Entity

<sub> *Below attributes are specific to journal entity. (Ty = '2') </sub>

Name    |Description                            |Type       | Operations
------- | ------------------------------------- | --------- | ----------------------------
Id      |Entity ID                              |Int64      |Equals
DJN     |Journal normalized name                |String     |none
JN      |Journal display name                   |String     |Equals
CC      |Journal total citation count           |Int32      |none  
ECC     |Journal total estimated citation count |Int32      |none
SSD     |Satori data                            |String     |none