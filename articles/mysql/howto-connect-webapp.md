---
title: Connect existing Azure App Service to Azure Database for MySQL
description: Instructions for how to properly connect an existing Azure App Service to Azure Database for MySQL
services: mysql
author: ajlam
ms.author: andrela
editor: jasonwhowell
manager: kfile
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: ff4a28e2f9a0149016d0e47c24e4665ab2e0500d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857288"
---
# <a name="connect-an-existing-azure-app-service-to-azure-database-for-mysql-server"></a>Connect an existing Azure App Service to Azure Database for MySQL server
This topic explains how to connect an existing Azure App Service to your Azure Database for MySQL server.

## <a name="before-you-begin"></a>Before you begin
Log in to the [Azure portal](https://portal.azure.com). Create an Azure Database for MySQL server. For details, refer to [How to create Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How to create Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).

Currently there are two solutions to enable access from an Azure App Service to an Azure Database for MySQL. Both solutions involve setting up server-level firewall rules.

## <a name="solution-1---create-a-firewall-rule-to-allow-all-ips"></a>Solution 1 - Create a firewall rule to allow all IPs
Azure Database for MySQL provides access security using a firewall to protect your data. When connecting from an Azure App Service to Azure Database for MySQL server, keep in mind that the outbound IPs of App Service are dynamic in nature. 

To ensure the availability of your Azure App Service, we recommend using this solution to allow ALL IPs.

> [!NOTE]
> Microsoft is working on a long-term solution to avoid allowing all IPs for Azure services to connect to Azure Database for MySQL.

1. On the MySQL server blade, under the Settings heading, click **Connection Security** to open the Connection Security blade for Azure Database for MySQL.

   ![Azure portal - click Connection Security](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Enter **RULE NAME**, **START IP**, and **END IP**, and then click **Save**.
   - Rule name: Allow-All-IPs
   - Start IP: 0.0.0.0
   - End IP: 255.255.255.255

   ![Azure portal - Add all IPs](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-to-explicitly-allow-outbound-ips"></a>Solution 2 - Create a firewall rule to explicitly allow outbound IPs
You can explicitly add all the outbound IPs of your Azure App Service.

1. On the App Service Properties blade, view your **OUTBOUND IP ADDRESS**.

   ![Azure portal - View outbound IPs](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. On the MySQL Connection security blade, add outbound IPs one by one.

   ![Azure portal - Add explicit IPs](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. Remember to **Save** your firewall rules.

Though the Azure App service attempts to keep IP addresses constant over time, there are cases where the IP addresses may change. For example, this can occur when the app recycles or a scale operation occurs, or when new computers are added in Azure regional data centers to increase capacity. When the IP addresses change, the app could experience downtime in the event it can no longer connect to the MySQL server. Keep this consideration in mind when choosing one of the preceding solutions.

## <a name="ssl-configuration"></a>SSL configuration
Azure Database for MySQL has SSL enabled by default. If your application is not using SSL to connect to the database, then you need to disable SSL on the MySQL server. For details on how to configure SSL, see [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).

## <a name="next-steps"></a>Next steps
For more information about connection strings, refer to [Connection Strings](howto-connection-string.md).
