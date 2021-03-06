---
title: Azure Database Migration Service Overview | Microsoft Docs
description: Overview of the Azure Database Migration Service, which provides seamless migrations from many database sources to Azure Data platforms.
services: database-migration
author: HJToland3
ms.author: jtoland
manager: ''
ms.reviewer: douglasl
ms.service: database-migration
ms.workload: data-services
ms.topic: article
ms.date: 09/01/2018
ms.openlocfilehash: d59850b0234912b02b003f4fc8089d76130151ba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869940"
---
# <a name="what-is-the-azure-database-migration-service"></a>What is the Azure Database Migration Service?
The Azure Database Migration Service is a fully managed service designed to enable seamless migrations from multiple database sources to Azure Data platforms with minimal downtime.

## <a name="migrate-databases-to-azure-with-familiar-tools"></a>Migrate databases to Azure with familiar tools
The Azure Database Migration Service integrates some of the functionality of our existing tools and services. It provides customers with a comprehensive, highly available solution. The service uses the [Data Migration Assistant](http://aka.ms/dma) to generate assessment reports that provide recommendations to guide you through the changes required prior to performing a migration. It's up to you to perform any remediation required. When you're ready to begin the migration process, the Azure Database Migration Service performs all of the required steps. You can fire and forget your migration projects with peace of mind, knowing that the process takes advantage of best practices as determined by Microsoft.

## <a name="regional-availability"></a>Regional availability
The Azure Database Migration Service is currently available in the following regions:

![Azure Database Migration Service regional availability](media\overview\dms-regional-availability.png)

> [!NOTE]
> Online migrations and SKU recommendation functionality are currently available only in the **Central US**, **East US 2**, and **West Europe** regions.

For the most up-to-date information about regional availability of the Azure Database Migration Service, on the Azure global infrastructure site, see [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).

## <a name="next-steps"></a>Next steps
- [Create an instance of the Azure Database Migration Service by using the Azure portal](quickstart-create-data-migration-service-portal.md).
- [Migrate SQL Server to Azure SQL Database](tutorial-sql-server-to-azure-sql.md).
- [Overview of prerequisites for using the Azure Database Migration Service](pre-reqs.md).
- [FAQ about using the Azure Database Migration Service](faq.md).
