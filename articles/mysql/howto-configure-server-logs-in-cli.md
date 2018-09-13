---
title: Access server logs in Azure Database for MySQL by using Azure CLI
description: This article describes how to access the server logs in Azure Database for MySQL by using the Azure CLI command-line utility.
services: mysql
author: rachel-msft
ms.author: raagyema
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.devlang: azure-cli
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: 57b72ded77484dc1c8ca4c62811b62e171365db4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969447"
---
# <a name="configure-and-access-server-logs-by-using-azure-cli"></a><span data-ttu-id="f029c-103">Configure and access server logs by using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f029c-103">Configure and access server logs by using Azure CLI</span></span>
<span data-ttu-id="f029c-104">You can download the Azure Database for MySQL server logs by using Azure CLI, the Azure command-line utility.</span><span class="sxs-lookup"><span data-stu-id="f029c-104">You can download the Azure Database for MySQL server logs by using Azure CLI, the Azure command-line utility.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f029c-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f029c-105">Prerequisites</span></span>
<span data-ttu-id="f029c-106">To step through this how-to guide, you need:</span><span class="sxs-lookup"><span data-stu-id="f029c-106">To step through this how-to guide, you need:</span></span>
- [<span data-ttu-id="f029c-107">Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="f029c-107">Azure Database for MySQL server</span></span>](quickstart-create-mysql-server-database-using-azure-cli.md)
- <span data-ttu-id="f029c-108">The [Azure CLI 2.0](/cli/azure/install-azure-cli) or Azure Cloud Shell in the browser</span><span class="sxs-lookup"><span data-stu-id="f029c-108">The [Azure CLI 2.0](/cli/azure/install-azure-cli) or Azure Cloud Shell in the browser</span></span>

## <a name="configure-logging-for-azure-database-for-mysql"></a><span data-ttu-id="f029c-109">Configure logging for Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="f029c-109">Configure logging for Azure Database for MySQL</span></span>
<span data-ttu-id="f029c-110">You can configure the server to access the MySQL slow query log by taking the following steps:</span><span class="sxs-lookup"><span data-stu-id="f029c-110">You can configure the server to access the MySQL slow query log by taking the following steps:</span></span>
1. <span data-ttu-id="f029c-111">Turn on logging by setting the **slow\_query\_log** parameter to ON.</span><span class="sxs-lookup"><span data-stu-id="f029c-111">Turn on logging by setting the **slow\_query\_log** parameter to ON.</span></span>
2. <span data-ttu-id="f029c-112">Adjust other parameters, such as **long\_query\_time** and **log\_slow\_admin\_statements**.</span><span class="sxs-lookup"><span data-stu-id="f029c-112">Adjust other parameters, such as **long\_query\_time** and **log\_slow\_admin\_statements**.</span></span>

<span data-ttu-id="f029c-113">To learn how to set the value of these parameters through Azure CLI, see [How to configure server parameters](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f029c-113">To learn how to set the value of these parameters through Azure CLI, see [How to configure server parameters](howto-configure-server-parameters-using-cli.md).</span></span> 

<span data-ttu-id="f029c-114">For example, the following CLI command turns on the slow query log, sets the long query time to 10 seconds, and then turns off the logging of the slow admin statement.</span><span class="sxs-lookup"><span data-stu-id="f029c-114">For example, the following CLI command turns on the slow query log, sets the long query time to 10 seconds, and then turns off the logging of the slow admin statement.</span></span> <span data-ttu-id="f029c-115">Finally, it lists the configuration options for your review.</span><span class="sxs-lookup"><span data-stu-id="f029c-115">Finally, it lists the configuration options for your review.</span></span>
```azurecli-interactive
az mysql server configuration set --name slow_query_log --resource-group myresourcegroup --server mydemoserver --value ON
az mysql server configuration set --name long_query_time --resource-group myresourcegroup --server mydemoserver --value 10
az mysql server configuration set --name log_slow_admin_statements --resource-group myresourcegroup --server mydemoserver --value OFF
az mysql server configuration list --resource-group myresourcegroup --server mydemoserver
```

## <a name="list-logs-for-azure-database-for-mysql-server"></a><span data-ttu-id="f029c-116">List logs for Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="f029c-116">List logs for Azure Database for MySQL server</span></span>
<span data-ttu-id="f029c-117">To list the available log files for your server, run the [az mysql server-logs list](/cli/azure/mysql/server-logs#az-mysql-server-logs-list) command.</span><span class="sxs-lookup"><span data-stu-id="f029c-117">To list the available log files for your server, run the [az mysql server-logs list](/cli/azure/mysql/server-logs#az-mysql-server-logs-list) command.</span></span>

<span data-ttu-id="f029c-118">You can list the log files for server **mydemoserver.mysql.database.azure.com** under the resource group **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="f029c-118">You can list the log files for server **mydemoserver.mysql.database.azure.com** under the resource group **myresourcegroup**.</span></span> <span data-ttu-id="f029c-119">Then direct the list of log files to a text file called **log\_files\_list.txt**.</span><span class="sxs-lookup"><span data-stu-id="f029c-119">Then direct the list of log files to a text file called **log\_files\_list.txt**.</span></span>
```azurecli-interactive
az mysql server-logs list --resource-group myresourcegroup --server mydemoserver > log_files_list.txt
```
## <a name="download-logs-from-the-server"></a><span data-ttu-id="f029c-120">Download logs from the server</span><span class="sxs-lookup"><span data-stu-id="f029c-120">Download logs from the server</span></span>
<span data-ttu-id="f029c-121">With the [az mysql server-logs download](/cli/azure/mysql/server-logs#az-mysql-server-logs-download) command, you can download individual log files for your server.</span><span class="sxs-lookup"><span data-stu-id="f029c-121">With the [az mysql server-logs download](/cli/azure/mysql/server-logs#az-mysql-server-logs-download) command, you can download individual log files for your server.</span></span> 

<span data-ttu-id="f029c-122">Use the following example to download the specific log file for the server **mydemoserver.mysql.database.azure.com** under the resource group **myresourcegroup** to your local environment.</span><span class="sxs-lookup"><span data-stu-id="f029c-122">Use the following example to download the specific log file for the server **mydemoserver.mysql.database.azure.com** under the resource group **myresourcegroup** to your local environment.</span></span>
```azurecli-interactive
az mysql server-logs download --name 20170414-mydemoserver-mysql.log --resource-group myresourcegroup --server mydemoserver
```

## <a name="next-steps"></a><span data-ttu-id="f029c-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="f029c-123">Next steps</span></span>
- <span data-ttu-id="f029c-124">Learn about [server logs in Azure Database for MySQL](concepts-server-logs.md).</span><span class="sxs-lookup"><span data-stu-id="f029c-124">Learn about [server logs in Azure Database for MySQL](concepts-server-logs.md).</span></span>
