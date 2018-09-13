---
title: Server concepts in Azure Database for MySQL
description: This topic provides considerations and guidelines for working with Azure Database for MySQL servers.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: 9d94f897546ea1e1190aab91e80eb9868224e5a7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871562"
---
# <a name="server-concepts-in-azure-database-for-mysql"></a><span data-ttu-id="dc0f2-103">Server concepts in Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="dc0f2-103">Server concepts in Azure Database for MySQL</span></span>
<span data-ttu-id="dc0f2-104">This article provides considerations and guidelines for working with Azure Database for MySQL servers.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-104">This article provides considerations and guidelines for working with Azure Database for MySQL servers.</span></span>

## <a name="what-is-an-azure-database-for-mysql-server"></a><span data-ttu-id="dc0f2-105">What is an Azure Database for MySQL server?</span><span class="sxs-lookup"><span data-stu-id="dc0f2-105">What is an Azure Database for MySQL server?</span></span>

<span data-ttu-id="dc0f2-106">An Azure Database for MySQL server is a central administrative point for multiple databases.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-106">An Azure Database for MySQL server is a central administrative point for multiple databases.</span></span> <span data-ttu-id="dc0f2-107">It is the same MySQL server construct that you may be familiar with in the on-premises world.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-107">It is the same MySQL server construct that you may be familiar with in the on-premises world.</span></span> <span data-ttu-id="dc0f2-108">Specifically, the Azure Database for MySQL service is managed, provides performance guarantees, and exposes access and features at server-level.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-108">Specifically, the Azure Database for MySQL service is managed, provides performance guarantees, and exposes access and features at server-level.</span></span>

<span data-ttu-id="dc0f2-109">An Azure Database for MySQL server:</span><span class="sxs-lookup"><span data-stu-id="dc0f2-109">An Azure Database for MySQL server:</span></span>

- <span data-ttu-id="dc0f2-110">Is created within an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-110">Is created within an Azure subscription.</span></span>
- <span data-ttu-id="dc0f2-111">Is the parent resource for databases.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-111">Is the parent resource for databases.</span></span>
- <span data-ttu-id="dc0f2-112">Provides a namespace for databases.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-112">Provides a namespace for databases.</span></span>
- <span data-ttu-id="dc0f2-113">Is a container with strong lifetime semantics - delete a server and it deletes the contained databases.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-113">Is a container with strong lifetime semantics - delete a server and it deletes the contained databases.</span></span>
- <span data-ttu-id="dc0f2-114">Collocates resources in a region.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-114">Collocates resources in a region.</span></span>
- <span data-ttu-id="dc0f2-115">Provides a connection endpoint for server and database access.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-115">Provides a connection endpoint for server and database access.</span></span>
- <span data-ttu-id="dc0f2-116">Provides the scope for management policies that apply to its databases: login, firewall, users, roles, configurations, etc.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-116">Provides the scope for management policies that apply to its databases: login, firewall, users, roles, configurations, etc.</span></span>
- <span data-ttu-id="dc0f2-117">Is available in multiple versions.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-117">Is available in multiple versions.</span></span> <span data-ttu-id="dc0f2-118">For more information, see [Supported Azure Database for MySQL database versions](./concepts-supported-versions.md).</span><span class="sxs-lookup"><span data-stu-id="dc0f2-118">For more information, see [Supported Azure Database for MySQL database versions](./concepts-supported-versions.md).</span></span>

<span data-ttu-id="dc0f2-119">Within an Azure Database for MySQL server, you can create one or multiple databases.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-119">Within an Azure Database for MySQL server, you can create one or multiple databases.</span></span> <span data-ttu-id="dc0f2-120">You can opt to create a single database per server to use all the resources or to create multiple databases to share the resources.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-120">You can opt to create a single database per server to use all the resources or to create multiple databases to share the resources.</span></span> <span data-ttu-id="dc0f2-121">The pricing is structured per-server, based on the configuration of pricing tier, vCores, and storage (GB).</span><span class="sxs-lookup"><span data-stu-id="dc0f2-121">The pricing is structured per-server, based on the configuration of pricing tier, vCores, and storage (GB).</span></span> <span data-ttu-id="dc0f2-122">For more information, see [Pricing tiers](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="dc0f2-122">For more information, see [Pricing tiers](./concepts-service-tiers.md).</span></span>

## <a name="how-do-i-connect-and-authenticate-to-an-azure-database-for-mysql-server"></a><span data-ttu-id="dc0f2-123">How do I connect and authenticate to an Azure Database for MySQL server?</span><span class="sxs-lookup"><span data-stu-id="dc0f2-123">How do I connect and authenticate to an Azure Database for MySQL server?</span></span>

<span data-ttu-id="dc0f2-124">The following elements help ensure safe access to your database.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-124">The following elements help ensure safe access to your database.</span></span>
|||
| :-- | :-- |
| <span data-ttu-id="dc0f2-125">**Authentication and authorization**</span><span class="sxs-lookup"><span data-stu-id="dc0f2-125">**Authentication and authorization**</span></span> | <span data-ttu-id="dc0f2-126">Azure Database for MySQL server supports native MySQL authentication.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-126">Azure Database for MySQL server supports native MySQL authentication.</span></span> <span data-ttu-id="dc0f2-127">You can connect and authenticate to a server with the server's admin login.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-127">You can connect and authenticate to a server with the server's admin login.</span></span> |
| <span data-ttu-id="dc0f2-128">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="dc0f2-128">**Protocol**</span></span> | <span data-ttu-id="dc0f2-129">The service supports a message-based protocol used by MySQL.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-129">The service supports a message-based protocol used by MySQL.</span></span> |
| <span data-ttu-id="dc0f2-130">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="dc0f2-130">**TCP/IP**</span></span> | <span data-ttu-id="dc0f2-131">The protocol is supported over TCP/IP and over Unix-domain sockets.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-131">The protocol is supported over TCP/IP and over Unix-domain sockets.</span></span> |
| <span data-ttu-id="dc0f2-132">**Firewall**</span><span class="sxs-lookup"><span data-stu-id="dc0f2-132">**Firewall**</span></span> | <span data-ttu-id="dc0f2-133">To help protect your data, a firewall rule prevents all access to your database server, until you specify which computers have permission.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-133">To help protect your data, a firewall rule prevents all access to your database server, until you specify which computers have permission.</span></span> <span data-ttu-id="dc0f2-134">See [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md).</span><span class="sxs-lookup"><span data-stu-id="dc0f2-134">See [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md).</span></span> |
| <span data-ttu-id="dc0f2-135">**SSL**</span><span class="sxs-lookup"><span data-stu-id="dc0f2-135">**SSL**</span></span> | <span data-ttu-id="dc0f2-136">The service supports enforcing SSL connections between your applications and your database server.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-136">The service supports enforcing SSL connections between your applications and your database server.</span></span>  <span data-ttu-id="dc0f2-137">See [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="dc0f2-137">See [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span> |

## <a name="how-do-i-manage-a-server"></a><span data-ttu-id="dc0f2-138">How do I manage a server?</span><span class="sxs-lookup"><span data-stu-id="dc0f2-138">How do I manage a server?</span></span>
<span data-ttu-id="dc0f2-139">You can manage Azure Database for MySQL servers by using the Azure portal or the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="dc0f2-139">You can manage Azure Database for MySQL servers by using the Azure portal or the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc0f2-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="dc0f2-140">Next steps</span></span>
- <span data-ttu-id="dc0f2-141">For an overview of the service, see [Azure Database for MySQL Overview](./overview.md)</span><span class="sxs-lookup"><span data-stu-id="dc0f2-141">For an overview of the service, see [Azure Database for MySQL Overview](./overview.md)</span></span>
- <span data-ttu-id="dc0f2-142">For information about specific resource quotas and limitations based on your **service tier**, see [Service tiers](./concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="dc0f2-142">For information about specific resource quotas and limitations based on your **service tier**, see [Service tiers](./concepts-service-tiers.md)</span></span>
- <span data-ttu-id="dc0f2-143">For information about connecting to the service, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="dc0f2-143">For information about connecting to the service, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md).</span></span>
