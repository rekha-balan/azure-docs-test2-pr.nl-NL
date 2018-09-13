---
title: include file
description: include file
services: cosmos-db
author: SnehaGunda
ms.service: cosmos-db
ms.topic: include
ms.date: 04/13/2018
ms.author: sngun
ms.custom: include file
ms.openlocfilehash: 37d7b1d44c2a4b2f3cd2fd3ac881b106d5056279
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45109364"
---
You can now use the Data Explorer tool in the Azure portal to create a database and table. 

1. Click **Data Explorer** > **New Table**. 
    
    The **Add Table** area is displayed on the far right, you may need to scroll right to see it.

    ![Data Explorer in the Azure portal](./media/cosmos-db-create-table/azure-cosmosdb-data-explorer.png)

2. In the **Add Table** page, enter the settings for the new table.

    Setting|Suggested value|Description
    ---|---|---
    Table Id|sample-table|The ID for your new table. Table names have the same character requirements as database ids. Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.
    Storage capacity| Fixed (10 GB)|Use the default value of **Fixed (10 GB)**. This value is the storage capacity of the database.
    Throughput|400 RUs|Change the throughput to 400 request units per second (RU/s). If you want to reduce latency, you can scale up the throughput later.

    Click **OK**.

    Data Explorer displays the new database and table.

    ![The Azure portal Data Explorer, showing the new database and collection](./media/cosmos-db-create-table/azure-cosmos-db-new-table.png)