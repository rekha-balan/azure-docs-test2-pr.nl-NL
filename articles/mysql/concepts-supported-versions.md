---
title: Supported versions in Azure Database for MySQL
description: Describes the supported versions in Azure Database for MySQL.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 05/23/2018
ms.openlocfilehash: c9a533ed9b9eb9ac53a02439b98a78954c7aaa11
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864757"
---
# <a name="supported-azure-database-for-mysql-server-versions"></a><span data-ttu-id="e4986-103">Supported Azure Database for MySQL server versions</span><span class="sxs-lookup"><span data-stu-id="e4986-103">Supported Azure Database for MySQL server versions</span></span>
<span data-ttu-id="e4986-104">Azure Database for MySQL has been developed from [MySQL Community Edition](https://www.mysql.com/products/community/), using the InnoDB engine.</span><span class="sxs-lookup"><span data-stu-id="e4986-104">Azure Database for MySQL has been developed from [MySQL Community Edition](https://www.mysql.com/products/community/), using the InnoDB engine.</span></span>  <span data-ttu-id="e4986-105">Azure Database for MySQL currently supports the following versions:</span><span class="sxs-lookup"><span data-stu-id="e4986-105">Azure Database for MySQL currently supports the following versions:</span></span>

## <a name="mysql-version-5639"></a><span data-ttu-id="e4986-106">MySQL Version 5.6.39</span><span class="sxs-lookup"><span data-stu-id="e4986-106">MySQL Version 5.6.39</span></span>
<span data-ttu-id="e4986-107">Refer to the MySQL [documentation](https://dev.mysql.com/doc/relnotes/mysql/5.6/en/news-5-6-39.html) to learn more about improvements and fixes in MySQL 5.6.39.</span><span class="sxs-lookup"><span data-stu-id="e4986-107">Refer to the MySQL [documentation](https://dev.mysql.com/doc/relnotes/mysql/5.6/en/news-5-6-39.html) to learn more about improvements and fixes in MySQL 5.6.39.</span></span>

## <a name="mysql-version-5721"></a><span data-ttu-id="e4986-108">MySQL Version 5.7.21</span><span class="sxs-lookup"><span data-stu-id="e4986-108">MySQL Version 5.7.21</span></span>
<span data-ttu-id="e4986-109">Refer to the MySQL [documentation](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-21.html) to learn about improvements and fixes in MySQL 5.7.21.</span><span class="sxs-lookup"><span data-stu-id="e4986-109">Refer to the MySQL [documentation](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-21.html) to learn about improvements and fixes in MySQL 5.7.21.</span></span>

> [!NOTE]
> <span data-ttu-id="e4986-110">In the service, a gateway is used to redirect the connections to server instances.</span><span class="sxs-lookup"><span data-stu-id="e4986-110">In the service, a gateway is used to redirect the connections to server instances.</span></span> <span data-ttu-id="e4986-111">After the connection is established, the MySQL client displays the version of MySQL set in the gateway, not the actual version running on your MySQL server instance.</span><span class="sxs-lookup"><span data-stu-id="e4986-111">After the connection is established, the MySQL client displays the version of MySQL set in the gateway, not the actual version running on your MySQL server instance.</span></span> <span data-ttu-id="e4986-112">To determine the version of your MySQL server instance, use the `SELECT VERSION();` command at the MySQL prompt.</span><span class="sxs-lookup"><span data-stu-id="e4986-112">To determine the version of your MySQL server instance, use the `SELECT VERSION();` command at the MySQL prompt.</span></span> 

## <a name="managing-updates-and-upgrades"></a><span data-ttu-id="e4986-113">Managing updates and upgrades</span><span class="sxs-lookup"><span data-stu-id="e4986-113">Managing updates and upgrades</span></span>
<span data-ttu-id="e4986-114">The service automatically manages patching for minor version updates.</span><span class="sxs-lookup"><span data-stu-id="e4986-114">The service automatically manages patching for minor version updates.</span></span> <span data-ttu-id="e4986-115">Major version upgrades are not supported (ex.</span><span class="sxs-lookup"><span data-stu-id="e4986-115">Major version upgrades are not supported (ex.</span></span> <span data-ttu-id="e4986-116">upgrading from MySQL 5.6 to MySQL 5.7).</span><span class="sxs-lookup"><span data-stu-id="e4986-116">upgrading from MySQL 5.6 to MySQL 5.7).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4986-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="e4986-117">Next steps</span></span>

<span data-ttu-id="e4986-118">For information about specific resource quotas and limitations based on your **service tier**, see [Service tiers](./concepts-pricing-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="e4986-118">For information about specific resource quotas and limitations based on your **service tier**, see [Service tiers](./concepts-pricing-tiers.md)</span></span>
