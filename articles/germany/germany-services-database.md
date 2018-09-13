---
title: Azure Germany database services | Microsoft Docs
description: Provides a comparison of database services for Azure Germany
services: germany
cloud: na
documentationcenter: na
author: gitralf
manager: rainerst
ms.assetid: na
ms.service: germany
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/13/2017
ms.author: ralfwi
ms.openlocfilehash: f409f70a49e4592bc5fd83a0f8c9fb9311e6371b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869047"
---
# <a name="azure-germany-database-services"></a>Azure Germany database services
## <a name="sql-database"></a>SQL Database
Azure SQL Database V12 is generally available in Azure Germany. For guidance on metadata visibility configuration and protection best practices, see the [Microsoft Security Center for SQL Database Engine](https://msdn.microsoft.com/library/bb510589.aspx) and the [SQL Database global documentation](../sql-database/index.yml).

### <a name="variations"></a>Variations
The address for SQL Database in Azure Germany is different from the address in global Azure:

| Service type | Global Azure | Azure Germany |
| --- | --- | --- |
| SQL Database | *.database.windows.net | *.database.cloudapi.de |


## <a name="azure-redis-cache"></a>Azure Redis Cache
For details on Azure Redis Cache and how to use it, see [Azure Redis Cache global documentation](../redis-cache/index.md).

### <a name="variations"></a>Variations
The URLs for accessing and managing Azure Redis Cache in Azure Germany are different from the URLs in global Azure:

| Service type | Global Azure | Azure Germany |
| --- | --- | --- |
| Cache endpoint | *.redis.cache.windows.net | *.redis.cache.cloudapi.de |
| Azure portal | https://portal.azure.com | https://portal.microsoftazure.de |

> [!NOTE]
> All your scripts and code need to account for the appropriate endpoints and environments. For more information, see "To connect to Microsoft Azure Germany" in [Manage Azure Redis Cache with Azure PowerShell](../redis-cache/cache-howto-manage-redis-cache-powershell.md).
>
>


## <a name="next-steps"></a>Next steps
For supplemental information and updates, subscribe to the [Azure Germany blog](https://blogs.msdn.microsoft.com/azuregermany/).
