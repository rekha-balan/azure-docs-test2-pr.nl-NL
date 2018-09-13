---
title: include file
description: include file
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 06/04/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 244d6be318662be794cac58aaa8350b433b6cb37
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45108888"
---
Do not associate a route table that includes a route with a destination of 0.0.0.0/0 to the gateway subnet. Doing so prevents the gateway from functioning properly.