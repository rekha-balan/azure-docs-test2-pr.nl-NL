---
title: Move Web App Resources to another Resource Group
description: Describes the scenarios where you can move Web Apps and App Services from one Resource Group to another.
services: app-service
documentationcenter: ''
author: ZainRizvi
manager: erikre
editor: ''
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 1b5059dc052005b6079f70ecf6771a3771df8d87
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551249"
---
# <a name="supported-move-configurations"></a><span data-ttu-id="b23f9-103">Supported Move Configurations</span><span class="sxs-lookup"><span data-stu-id="b23f9-103">Supported Move Configurations</span></span>
<span data-ttu-id="b23f9-104">You can move Azure Web App resources using the [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b23f9-104">You can move Azure Web App resources using the [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="b23f9-105">Azure Web Apps currently supports the following move scenarios:</span><span class="sxs-lookup"><span data-stu-id="b23f9-105">Azure Web Apps currently supports the following move scenarios:</span></span>

* <span data-ttu-id="b23f9-106">Move the entire contents of a resource group (web apps, app service plans, and certificates) to another resource group.</span><span class="sxs-lookup"><span data-stu-id="b23f9-106">Move the entire contents of a resource group (web apps, app service plans, and certificates) to another resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="b23f9-107">The destination resource group can not contain any Microsoft.Web resources in this scenario.</span><span class="sxs-lookup"><span data-stu-id="b23f9-107">The destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="b23f9-108">Move individual web apps to a different resource group, while still hosting them in their current app service plan (the app service plan stays in the old resource group).</span><span class="sxs-lookup"><span data-stu-id="b23f9-108">Move individual web apps to a different resource group, while still hosting them in their current app service plan (the app service plan stays in the old resource group).</span></span>


