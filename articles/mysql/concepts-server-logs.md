---
title: Server logs for Azure Database for MySQL
description: Describes the logs available in Azure Database for MySQL, and the available parameters for enabling different logging levels.
services: mysql
author: rachel-msft
ms.author: raagyema
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: 50e4b9b8b8f9433ec725aaa982e969cec7afb91c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871162"
---
# <a name="server-logs-in-azure-database-for-mysql"></a><span data-ttu-id="2f3cc-103">Server Logs in Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="2f3cc-103">Server Logs in Azure Database for MySQL</span></span>
<span data-ttu-id="2f3cc-104">In Azure Database for MySQL, the slow query log is available to users.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-104">In Azure Database for MySQL, the slow query log is available to users.</span></span> <span data-ttu-id="2f3cc-105">Access to the transaction log is not supported.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-105">Access to the transaction log is not supported.</span></span> <span data-ttu-id="2f3cc-106">The slow query log can be used to identify performance bottlenecks for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-106">The slow query log can be used to identify performance bottlenecks for troubleshooting.</span></span> 

<span data-ttu-id="2f3cc-107">For more information about the MySQL slow query log, see the MySQL reference manual's [slow query log section](https://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html).</span><span class="sxs-lookup"><span data-stu-id="2f3cc-107">For more information about the MySQL slow query log, see the MySQL reference manual's [slow query log section](https://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html).</span></span>

## <a name="access-server-logs"></a><span data-ttu-id="2f3cc-108">Access server logs</span><span class="sxs-lookup"><span data-stu-id="2f3cc-108">Access server logs</span></span>
<span data-ttu-id="2f3cc-109">You can list and download Azure Database for MySQL server logs using the Azure portal, and the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-109">You can list and download Azure Database for MySQL server logs using the Azure portal, and the Azure CLI.</span></span>

<span data-ttu-id="2f3cc-110">In the Azure portal, select your Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-110">In the Azure portal, select your Azure Database for MySQL server.</span></span> <span data-ttu-id="2f3cc-111">Under the **Monitoring** heading, select the **Server Logs** page.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-111">Under the **Monitoring** heading, select the **Server Logs** page.</span></span>

<span data-ttu-id="2f3cc-112">For more information on Azure CLI, see [Configure and access server logs using Azure CLI](howto-configure-server-logs-in-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2f3cc-112">For more information on Azure CLI, see [Configure and access server logs using Azure CLI](howto-configure-server-logs-in-cli.md).</span></span>

## <a name="log-retention"></a><span data-ttu-id="2f3cc-113">Log retention</span><span class="sxs-lookup"><span data-stu-id="2f3cc-113">Log retention</span></span>
<span data-ttu-id="2f3cc-114">Logs are available for up to seven days from their creation.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-114">Logs are available for up to seven days from their creation.</span></span> <span data-ttu-id="2f3cc-115">If the total size of the available logs exceeds 7.5 GB, then the oldest files are deleted until space is available.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-115">If the total size of the available logs exceeds 7.5 GB, then the oldest files are deleted until space is available.</span></span> 

<span data-ttu-id="2f3cc-116">Logs are rotated every 24 hours or 7.5 GB, whichever comes first.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-116">Logs are rotated every 24 hours or 7.5 GB, whichever comes first.</span></span>


## <a name="configure-logging"></a><span data-ttu-id="2f3cc-117">Configure logging</span><span class="sxs-lookup"><span data-stu-id="2f3cc-117">Configure logging</span></span> 
<span data-ttu-id="2f3cc-118">By default the slow query log is disabled.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-118">By default the slow query log is disabled.</span></span> <span data-ttu-id="2f3cc-119">To enable it, set slow_query_log to ON.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-119">To enable it, set slow_query_log to ON.</span></span>

<span data-ttu-id="2f3cc-120">Other parameters you can adjust include:</span><span class="sxs-lookup"><span data-stu-id="2f3cc-120">Other parameters you can adjust include:</span></span>

- <span data-ttu-id="2f3cc-121">**long_query_time**: if a query takes longer than long_query_time (in seconds) that query is logged.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-121">**long_query_time**: if a query takes longer than long_query_time (in seconds) that query is logged.</span></span> <span data-ttu-id="2f3cc-122">The default is 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-122">The default is 10 seconds.</span></span>
- <span data-ttu-id="2f3cc-123">**log_slow_admin_statements**: if ON includes administrative statements like ALTER_TABLE and ANALYZE_TABLE in the statements written to the slow_query_log.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-123">**log_slow_admin_statements**: if ON includes administrative statements like ALTER_TABLE and ANALYZE_TABLE in the statements written to the slow_query_log.</span></span>
- <span data-ttu-id="2f3cc-124">**log_queries_not_using_indexes**: determines whether queries that do not use indexes are logged to the slow_query_log</span><span class="sxs-lookup"><span data-stu-id="2f3cc-124">**log_queries_not_using_indexes**: determines whether queries that do not use indexes are logged to the slow_query_log</span></span>
- <span data-ttu-id="2f3cc-125">**log_throttle_queries_not_using_indexes**: This parameter limits the number of non-index queries that can be written to the slow query log.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-125">**log_throttle_queries_not_using_indexes**: This parameter limits the number of non-index queries that can be written to the slow query log.</span></span> <span data-ttu-id="2f3cc-126">This parameter takes effect when log_queries_not_using_indexes is set to ON.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-126">This parameter takes effect when log_queries_not_using_indexes is set to ON.</span></span>

<span data-ttu-id="2f3cc-127">See the MySQL [slow query log documentation](https://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html) for full descriptions of the slow query log parameters.</span><span class="sxs-lookup"><span data-stu-id="2f3cc-127">See the MySQL [slow query log documentation](https://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html) for full descriptions of the slow query log parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f3cc-128">Next Steps</span><span class="sxs-lookup"><span data-stu-id="2f3cc-128">Next Steps</span></span>
- <span data-ttu-id="2f3cc-129">[How to configure and access server logs from the Azure CLI](howto-configure-server-logs-in-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2f3cc-129">[How to configure and access server logs from the Azure CLI](howto-configure-server-logs-in-cli.md).</span></span>
