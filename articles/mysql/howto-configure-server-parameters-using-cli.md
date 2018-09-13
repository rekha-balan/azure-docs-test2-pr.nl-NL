---
title: Configure the service parameters in Azure Database for MySQL
description: This article describes how to configure the service parameters in Azure Database for MySQL using the Azure CLI command line utility.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.devlang: azure-cli
ms.topic: article
ms.date: 07/18/2018
ms.openlocfilehash: 61fee0771d6847a0ec56de656057409bbcdcba16
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856987"
---
# <a name="customize-server-configuration-parameters-by-using-azure-cli"></a><span data-ttu-id="30166-103">Customize server configuration parameters by using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="30166-103">Customize server configuration parameters by using Azure CLI</span></span>
<span data-ttu-id="30166-104">You can list, show, and update configuration parameters for an Azure Database for MySQL server by using Azure CLI, the Azure command-line utility.</span><span class="sxs-lookup"><span data-stu-id="30166-104">You can list, show, and update configuration parameters for an Azure Database for MySQL server by using Azure CLI, the Azure command-line utility.</span></span> <span data-ttu-id="30166-105">A subset of engine configurations is exposed at the server-level and can be modified.</span><span class="sxs-lookup"><span data-stu-id="30166-105">A subset of engine configurations is exposed at the server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="30166-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="30166-106">Prerequisites</span></span>
<span data-ttu-id="30166-107">To step through this how-to guide, you need:</span><span class="sxs-lookup"><span data-stu-id="30166-107">To step through this how-to guide, you need:</span></span>
- [<span data-ttu-id="30166-108">An Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="30166-108">An Azure Database for MySQL server</span></span>](quickstart-create-mysql-server-database-using-azure-cli.md)
- <span data-ttu-id="30166-109">[Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use the Azure Cloud Shell in the browser.</span><span class="sxs-lookup"><span data-stu-id="30166-109">[Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-mysql-server"></a><span data-ttu-id="30166-110">List server configuration parameters for Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="30166-110">List server configuration parameters for Azure Database for MySQL server</span></span>
<span data-ttu-id="30166-111">To list all modifiable parameters in a server and their values, run the [az mysql server configuration list](/cli/azure/mysql/server/configuration#az-mysql-server-configuration-list) command.</span><span class="sxs-lookup"><span data-stu-id="30166-111">To list all modifiable parameters in a server and their values, run the [az mysql server configuration list](/cli/azure/mysql/server/configuration#az-mysql-server-configuration-list) command.</span></span>

<span data-ttu-id="30166-112">You can list the server configuration parameters for the server **mydemoserver.mysql.database.azure.com** under resource group **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="30166-112">You can list the server configuration parameters for the server **mydemoserver.mysql.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az mysql server configuration list --resource-group myresourcegroup --server mydemoserver
```
<span data-ttu-id="30166-113">For the definition of each of the listed parameters, see the MySQL reference section on [Server System Variables](https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html).</span><span class="sxs-lookup"><span data-stu-id="30166-113">For the definition of each of the listed parameters, see the MySQL reference section on [Server System Variables](https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html).</span></span>

## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="30166-114">Show server configuration parameter details</span><span class="sxs-lookup"><span data-stu-id="30166-114">Show server configuration parameter details</span></span>
<span data-ttu-id="30166-115">To show details about a particular configuration parameter for a server, run the [az mysql server configuration show](/cli/azure/mysql/server/configuration#az-mysql-server-configuration-show) command.</span><span class="sxs-lookup"><span data-stu-id="30166-115">To show details about a particular configuration parameter for a server, run the [az mysql server configuration show](/cli/azure/mysql/server/configuration#az-mysql-server-configuration-show) command.</span></span>

<span data-ttu-id="30166-116">This example shows details of the **slow\_query\_log** server configuration parameter for server **mydemoserver.mysql.database.azure.com** under resource group **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="30166-116">This example shows details of the **slow\_query\_log** server configuration parameter for server **mydemoserver.mysql.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az mysql server configuration show --name slow_query_log --resource-group myresourcegroup --server mydemoserver
```
## <a name="modify-a-server-configuration-parameter-value"></a><span data-ttu-id="30166-117">Modify a server configuration parameter value</span><span class="sxs-lookup"><span data-stu-id="30166-117">Modify a server configuration parameter value</span></span>
<span data-ttu-id="30166-118">You can also modify the value of a certain server configuration parameter, which updates the underlying configuration value for the MySQL server engine.</span><span class="sxs-lookup"><span data-stu-id="30166-118">You can also modify the value of a certain server configuration parameter, which updates the underlying configuration value for the MySQL server engine.</span></span> <span data-ttu-id="30166-119">To update the configuration, use the [az mysql server configuration set](/cli/azure/mysql/server/configuration#az-mysql-server-configuration-set) command.</span><span class="sxs-lookup"><span data-stu-id="30166-119">To update the configuration, use the [az mysql server configuration set](/cli/azure/mysql/server/configuration#az-mysql-server-configuration-set) command.</span></span> 

<span data-ttu-id="30166-120">To update the **slow\_query\_log** server configuration parameter of server **mydemoserver.mysql.database.azure.com** under resource group **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="30166-120">To update the **slow\_query\_log** server configuration parameter of server **mydemoserver.mysql.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az mysql server configuration set --name slow_query_log --resource-group myresourcegroup --server mydemoserver --value ON
```
<span data-ttu-id="30166-121">If you want to reset the value of a configuration parameter, omit the optional `--value` parameter, and the service applies the default value.</span><span class="sxs-lookup"><span data-stu-id="30166-121">If you want to reset the value of a configuration parameter, omit the optional `--value` parameter, and the service applies the default value.</span></span> <span data-ttu-id="30166-122">For the example above, it would look like:</span><span class="sxs-lookup"><span data-stu-id="30166-122">For the example above, it would look like:</span></span>
```azurecli-interactive
az mysql server configuration set --name slow_query_log --resource-group myresourcegroup --server mydemoserver
```
<span data-ttu-id="30166-123">This code resets the **slow\_query\_log** configuration to the default value **OFF**.</span><span class="sxs-lookup"><span data-stu-id="30166-123">This code resets the **slow\_query\_log** configuration to the default value **OFF**.</span></span> 

## <a name="working-with-the-time-zone-parameter"></a><span data-ttu-id="30166-124">Working with the time zone parameter</span><span class="sxs-lookup"><span data-stu-id="30166-124">Working with the time zone parameter</span></span>

### <a name="populating-the-time-zone-tables"></a><span data-ttu-id="30166-125">Populating the time zone tables</span><span class="sxs-lookup"><span data-stu-id="30166-125">Populating the time zone tables</span></span>

<span data-ttu-id="30166-126">The time zone tables on your server can be populated by calling the `az_load_timezone` stored procedure from a tool like the MySQL command line or MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="30166-126">The time zone tables on your server can be populated by calling the `az_load_timezone` stored procedure from a tool like the MySQL command line or MySQL Workbench.</span></span>

> [!NOTE]
> <span data-ttu-id="30166-127">If you are running the `az_load_timezone` command from MySQL Workbench, you may need to turn off safe update mode first using `SET SQL_SAFE_UPDATES=0;`.</span><span class="sxs-lookup"><span data-stu-id="30166-127">If you are running the `az_load_timezone` command from MySQL Workbench, you may need to turn off safe update mode first using `SET SQL_SAFE_UPDATES=0;`.</span></span>

```sql
CALL mysql.az_load_timezone();
```

<span data-ttu-id="30166-128">To view available time zone values, run the following command:</span><span class="sxs-lookup"><span data-stu-id="30166-128">To view available time zone values, run the following command:</span></span>

```sql
SELECT name FROM mysql.time_zone_name;
```

### <a name="setting-the-global-level-time-zone"></a><span data-ttu-id="30166-129">Setting the global level time zone</span><span class="sxs-lookup"><span data-stu-id="30166-129">Setting the global level time zone</span></span>

<span data-ttu-id="30166-130">The global level time zone can be set using the [az mysql server configuration set](/cli/azure/mysql/server/configuration#az-mysql-server-configuration-set) command.</span><span class="sxs-lookup"><span data-stu-id="30166-130">The global level time zone can be set using the [az mysql server configuration set](/cli/azure/mysql/server/configuration#az-mysql-server-configuration-set) command.</span></span>

<span data-ttu-id="30166-131">The following command updates the **time\_zone** server configuration parameter of server **mydemoserver.mysql.database.azure.com** under resource group **myresourcegroup** to **US/Pacific**.</span><span class="sxs-lookup"><span data-stu-id="30166-131">The following command updates the **time\_zone** server configuration parameter of server **mydemoserver.mysql.database.azure.com** under resource group **myresourcegroup** to **US/Pacific**.</span></span>

```azurecli-interactive
az mysql server configuration set --name time_zone --resource-group myresourcegroup --server mydemoserver --value "US/Pacific"
```

### <a name="setting-the-session-level-time-zone"></a><span data-ttu-id="30166-132">Setting the session level time zone</span><span class="sxs-lookup"><span data-stu-id="30166-132">Setting the session level time zone</span></span>

<span data-ttu-id="30166-133">The session level time zone can be set by running the `SET time_zone` command from a tool like the MySQL command line or MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="30166-133">The session level time zone can be set by running the `SET time_zone` command from a tool like the MySQL command line or MySQL Workbench.</span></span> <span data-ttu-id="30166-134">The example below sets the time zone to the **US/Pacific** time zone.</span><span class="sxs-lookup"><span data-stu-id="30166-134">The example below sets the time zone to the **US/Pacific** time zone.</span></span>  

```sql
SET time_zone = 'US/Pacific';
```

<span data-ttu-id="30166-135">Refer to the MySQL documentation for [Date and Time Functions](https://dev.mysql.com/doc/refman/5.7/en/date-and-time-functions.html#function_convert-tz).</span><span class="sxs-lookup"><span data-stu-id="30166-135">Refer to the MySQL documentation for [Date and Time Functions](https://dev.mysql.com/doc/refman/5.7/en/date-and-time-functions.html#function_convert-tz).</span></span>


## <a name="next-steps"></a><span data-ttu-id="30166-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="30166-136">Next steps</span></span>

- <span data-ttu-id="30166-137">How to configure [server parameters in Azure portal](howto-server-parameters.md)</span><span class="sxs-lookup"><span data-stu-id="30166-137">How to configure [server parameters in Azure portal](howto-server-parameters.md)</span></span>