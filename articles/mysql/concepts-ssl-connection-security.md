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
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="a2e80-103">SSL connectivity in Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="a2e80-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="a2e80-104">Azure Database for MySQL supports connecting your database server to client applications using Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="a2e80-104">Azure Database for MySQL supports connecting your database server to client applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="a2e80-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span><span class="sxs-lookup"><span data-stu-id="a2e80-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="a2e80-106">Default settings</span><span class="sxs-lookup"><span data-stu-id="a2e80-106">Default settings</span></span>
<span data-ttu-id="a2e80-107">By default, the database service should be configured to require SSL connections when connecting to MySQL.</span><span class="sxs-lookup"><span data-stu-id="a2e80-107">By default, the database service should be configured to require SSL connections when connecting to MySQL.</span></span>  <span data-ttu-id="a2e80-108">We recommend to avoid disabling the SSL option whenever possible.</span><span class="sxs-lookup"><span data-stu-id="a2e80-108">We recommend to avoid disabling the SSL option whenever possible.</span></span> 

<span data-ttu-id="a2e80-109">When provisioning a new Azure Database for MySQL server through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="a2e80-109">When provisioning a new Azure Database for MySQL server through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="a2e80-110">Connection strings for various programming languages are shown in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a2e80-110">Connection strings for various programming languages are shown in the Azure portal.</span></span> <span data-ttu-id="a2e80-111">Those connection strings include the required SSL parameters to connect to your database.</span><span class="sxs-lookup"><span data-stu-id="a2e80-111">Those connection strings include the required SSL parameters to connect to your database.</span></span> <span data-ttu-id="a2e80-112">In the Azure portal, select your server.</span><span class="sxs-lookup"><span data-stu-id="a2e80-112">In the Azure portal, select your server.</span></span> <span data-ttu-id="a2e80-113">Under the **Settings** heading, select the **Connection strings**.</span><span class="sxs-lookup"><span data-stu-id="a2e80-113">Under the **Settings** heading, select the **Connection strings**.</span></span> <span data-ttu-id="a2e80-114">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span><span class="sxs-lookup"><span data-stu-id="a2e80-114">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="a2e80-115">To learn how to enable or disable SSL connection when developing application, refer to [How to configure SSL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="a2e80-115">To learn how to enable or disable SSL connection when developing application, refer to [How to configure SSL](howto-configure-ssl.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a2e80-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="a2e80-116">Next steps</span></span>
[<span data-ttu-id="a2e80-117">Connection libraries for Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="a2e80-117">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
