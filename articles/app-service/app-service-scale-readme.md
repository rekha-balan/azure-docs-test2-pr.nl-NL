---
title: 'Azure App Service: Scaling App Service Applications'
description: Learn the ins and outs of scaling Application in App Service.
keywords: app service, azure app service, scale, scalable, app service plan, app service cost
services: app-service
documentationcenter: ''
author: btardif
manager: erikre
editor: ''
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: 4ebaafe69fc1f91c7890611b14e8600df5c40cde
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660542"
---
# <a name="azure-app-service-scaling-app-service-applications"></a>Azure App Service: Scaling App Service Applications
Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).
However, scaling an application is a complex problem that does not have a "one size fits all" solution. To correctly scale your application there are 3 key areas that will contribute to your applications success:

1. Understanding your application architecture and its weaknesses.
   * Is your Application Stateful? Stateless?
   * What are all the components of your application?
     * Where are the bottlenecks in the application?
   * When load is applied to your app, what will break first?
2. Understanding the expected load and performance requirements.
   * Does the application need to serve one thousand users? or one million?
   * Will traffic come from a single geographic location or globally?
   * Are there seasonal variations? traffic peaks?
   * How fast should the app respond? 1 second? 1 millisecond?
3. Understanding and correctly leverage the platform hosting your app.
   * What features should I leverage to achieve my scale goals?

This section will help you understand all the factors and help you devise a strategy that takes advantage of the necessary App Service features to achieve your scalability goals.

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

