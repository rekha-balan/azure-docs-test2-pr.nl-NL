---
title: Related and linked resources in the tile gallery
description: Learn about related and linked resources that are displayed in the tile gallery of the Azure preview portal.
services: azure-portal
documentationcenter: ''
author: adamabdelhamed
manager: wpickett
editor: ''
ms.assetid: dba96d29-f518-49c8-bfd2-f14cecb44cbf
ms.service: azure-portal
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2015
ms.author: adamab
ms.openlocfilehash: efa7bce26c2c4c153b083e0e34d689a11d27dd16
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564184"
---
# <a name="related-and-linked-resources-in-the-tile-gallery"></a>Related and linked resources in the tile gallery
The tile gallery enables you to find tiles for a particular resource and drag them onto your current blade. Using the tile gallery, you can create management views that span resources. For any specified resource, the related resources include all the resources in its resource group, and any resources that link to or from the resource.

## <a name="linked-resources-in-resource-manager"></a>Linked resources in Resource Manager
Linking is a feature of the Resource Manager.  It enables you to declare relationships between resources even if they do not reside in the same resource group. Linking has no impact on the runtime of your resources, no impact on billing, and no impact on role-based access.  It's simply a mechanism you can use to represent relationships so that tools like the tile gallery can provide a rich management experience.  Your tools can inspect the links using the links API and provide custom relationship management experiences as well. 

## <a name="how-do-i-link-my-resources"></a>How do I link my resources?
When you create resources through the portal or by deploying a template through Azure PowerShell or Azure CLI, links are automatically created for some dependent resources. You can also programmatically link resources by using the [Linked Resources REST API](/rest/api/resources/resourcelinks).

## <a name="next-steps"></a>Next steps
* If you need an introduction to writing Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).
* To understand more about working with resource groups through the portal, see [Using the Azure portal to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).

