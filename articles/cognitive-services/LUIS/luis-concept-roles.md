---
title: Understanding how roles are used in pattern-based entities - Azure| Microsoft Docs
description: Learn how a role is used in an pattern-based entity to give a name to a contextual entity subtype.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 06/08/2018
ms.author: diberry
ms.openlocfilehash: d2692cdce9da7428bd7b30c4feaf7347792618f5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857645"
---
# <a name="entity-roles-in-patterns-are-contextual-subtypes"></a>Entity roles in Patterns are contextual subtypes
Roles are named, contextual subtypes of an entity used only in [patterns](luis-concept-patterns.md).

For example, in the utterance `buy a ticket from New York to London`, both New York and London are cities but each has a different meaning in the sentence. New York is the origin city and London is the destination city. 

Roles give a name to those differences:

|Entity|Role|Purpose|
|--|--|--|
|Location|origin|where the plane leaves from|
|Location|destination|where the plane lands|

## <a name="how-are-roles-used-in-patterns"></a>How are roles used in patterns?
In a pattern's template utterance, roles are used within the utterance: 

```
buy a ticket from {Location:origin} to {Location:destination}
```

## <a name="role-syntax-in-patterns"></a>Role syntax in patterns
The entity and role are surrounded in parentheses, `{}`. The entity and the role are separated by a colon. 

## <a name="roles-versus-hierarchical-entities"></a>Roles versus Hierarchical entities
Hierarchical entities provide the same contextual information as roles but only to utterances in **intents**. Similarly, roles provide the same contextual information as hierarchical entities but only in **patterns**.

|Contextual learning|Used in|
|--|--|
|hierarchical entities|intents|
|roles|patterns|

## <a name="next-steps"></a>Next steps

* Learn how to add [roles](luis-how-to-add-entities.md#add-role-to-pattern-based-entity)
