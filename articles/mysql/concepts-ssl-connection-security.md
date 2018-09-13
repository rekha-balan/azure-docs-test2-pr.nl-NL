---
title: SSL connectivity for Azure Database for MySQL
description: Information for configuring Azure Database for MySQL and associated applications to properly use SSL connections
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: kfile
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: ee7e0ec8524d66ee89cf7b2c4d44b70efa784f8f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864965"
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a>SSL connectivity in Azure Database for MySQL
Azure Database for MySQL supports connecting your database server to client applications using Secure Sockets Layer (SSL). Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.

## <a name="default-settings"></a>Default settings
By default, the database service should be configured to require SSL connections when connecting to MySQL.  We recommend to avoid disabling the SSL option whenever possible. 

When provisioning a new Azure Database for MySQL server through the Azure portal and CLI, enforcement of SSL connections is enabled by default. 

Connection strings for various programming languages are shown in the Azure portal. Those connection strings include the required SSL parameters to connect to your database. In the Azure portal, select your server. Under the **Settings** heading, select the **Connection strings**. The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.

To learn how to enable or disable SSL connection when developing application, refer to [How to configure SSL](howto-configure-ssl.md). 

## <a name="next-steps"></a>Next steps
[Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)
