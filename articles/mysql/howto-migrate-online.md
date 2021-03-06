---
title: Minimal-downtime migration to Azure Database for MySQL
description: This article describes how to perform a minimal-downtime migration of a MySQL database to Azure Database for MySQL by using the Azure Database Migration Service.
services: mysql
author: HJToland3
ms.author: jtoland
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 06/21/2018
ms.openlocfilehash: 55d5cf97225508d6c7c490347cfe21ced832300e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871350"
---
# <a name="minimal-downtime-migration-to-azure-database-for-mysql"></a>Minimal-downtime migration to Azure Database for MySQL
You can perform MySQL migrations to Azure Database for MySQL with minimal downtime by using the newly introduced **continuous sync capability** for the [Azure Database Migration Service](https://aka.ms/get-dms) (DMS). This functionality limits the amount of downtime that is incurred by the application.

## <a name="overview"></a>Overview
DMS performs an initial load of your on-premises to Azure Database for MySQL, and then continuously syncs any new transactions to Azure while the application remains running. After the data catches up on the target Azure side, you stop the application for a brief moment (minimum downtime), wait for the last batch of data (from the time you stop the application until the application is effectively unavailable to take any new traffic) to catch up in the target, and then update your connection string to point to Azure. When you are finished, your application will be live on Azure!

![Continuous sync with the Azure Database Migration Service](./media/howto-migrate-online/ContinuousSync.png)

- DMS migration of MySQL sources is currently in public preview. If you would like to try out the service to migrate your MySQL workloads, go ahead in the portal. Your feedback is invaluable in helping to further improve the service.

## <a name="next-steps"></a>Next steps
- View the video [Easily migrate MySQL/PostgreSQL apps to Azure managed service](https://medius.studios.ms/Embed/Video/THR2201?sid=THR2201), which contains a demo showing how to migrate MySQL apps to Azure Database for MySQL.
- [Migrate MySQL to Azure Database for MySQL online using DMS] (https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online).
