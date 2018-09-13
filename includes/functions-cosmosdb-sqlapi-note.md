---
title: include file
description: include file
services: functions
author: ggailey777
manager: jeconnoc
ms.service: functions
ms.topic: include
ms.date: 08/22/2018
ms.author: glenga
ms.custom: include file
ms.openlocfilehash: bb915c18965a55c2b1fc7fe3cf1fa923d7f43fd6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45373849"
---
Azure Cosmos DB bindings are only supported for use with the SQL API. For all other Azure Cosmos DB APIs, you should access the database from your function by using the static client for your API, including [MongoDB API](../articles/cosmos-db/mongodb-introduction.md), [Cassandra API](../articles/cosmos-db/cassandra-introduction.md), [Gremlin API](../articles/cosmos-db/graph-introduction.md), and [Table API](../articles/cosmos-db/table-introduction.md).
