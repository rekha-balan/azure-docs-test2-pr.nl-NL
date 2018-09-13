---
title: Academic Graph entity attributes for the Academic Knowledge API | Microsoft Docs
description: Learn about the entity attributes you can use with the Academic Graph in the Academic Knowledge API.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.component: academic-knowledge
ms.topic: article
ms.date: 03/27/2017
ms.author: alch
ms.openlocfilehash: f771969c3c6f05e5d2c99b1fbf593ae039ccb12c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818355"
---
# <a name="entity-attributes"></a>Entity Attributes

The academic graph is composed of 7 types of entity. All entities will have a Entity ID and a Entity type.

## <a name="common-entity-attributes"></a>Common Entity Attributes
Name    |Description                |Type       | Operations
------- | ------------------------- | --------- | ----------------------------
Id      |Entity ID                  |Int64      |Equals
Ty      |Entity type                |enum   |Equals

## <a name="entity-type-enum"></a>Entity type enum
Name                                                            |value
----------------------------------------------------------------|-----
[Paper](PaperEntityAttributes.md)                               |0
[Author](AuthorEntityAttributes.md)                             |1
[Journal](JournalEntityAttributes.md)                           |2
[Conference Series](JournalEntityAttributes.md)                 |3
[Conference Instance](ConferenceInstanceEntityAttributes.md)    |4
[Affiliation](AffiliationEntityAttributes.md)                   |5
[Field Of Study](FieldsOfStudyEntityAttributes.md)                      |6

