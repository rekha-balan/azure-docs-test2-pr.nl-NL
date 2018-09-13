---
title: How to backup and restore a server in Azure Database for MySQL
description: Learn how to backup and restore a server in Azure Database for MySQL by using the Azure CLI.
services: mysql
author: rachel-msft
ms.author: raagyema
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.devlang: azure-cli
ms.topic: article
ms.date: 04/01/2018
ms.openlocfilehash: f4253d4259d66b0c5746ef61cfc3cf4f4f2caad3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868967"
---
# <a name="how-to-back-up-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-cli"></a><span data-ttu-id="f210b-103">How to back up and restore a server in Azure Database for MySQL using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f210b-103">How to back up and restore a server in Azure Database for MySQL using the Azure CLI</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="f210b-104">Backup happens automatically</span><span class="sxs-lookup"><span data-stu-id="f210b-104">Backup happens automatically</span></span>
<span data-ttu-id="f210b-105">Azure Database for MySQL servers are backed up periodically to enable Restore features.</span><span class="sxs-lookup"><span data-stu-id="f210b-105">Azure Database for MySQL servers are backed up periodically to enable Restore features.</span></span> <span data-ttu-id="f210b-106">Using this feature you may restore the server and all its databases to an earlier point-in-time, on a new server.</span><span class="sxs-lookup"><span data-stu-id="f210b-106">Using this feature you may restore the server and all its databases to an earlier point-in-time, on a new server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f210b-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f210b-107">Prerequisites</span></span>
<span data-ttu-id="f210b-108">To complete this how-to guide, you need:</span><span class="sxs-lookup"><span data-stu-id="f210b-108">To complete this how-to guide, you need:</span></span>
- <span data-ttu-id="f210b-109">An [Azure Database for MySQL server and database](quickstart-create-mysql-server-database-using-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="f210b-109">An [Azure Database for MySQL server and database](quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="f210b-110">This how-to guide requires that you use Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="f210b-110">This how-to guide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f210b-111">To confirm the version, at the Azure CLI command prompt, enter `az --version`.</span><span class="sxs-lookup"><span data-stu-id="f210b-111">To confirm the version, at the Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="f210b-112">To install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f210b-112">To install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="set-backup-configuration"></a><span data-ttu-id="f210b-113">Set backup configuration</span><span class="sxs-lookup"><span data-stu-id="f210b-113">Set backup configuration</span></span>

<span data-ttu-id="f210b-114">You make the choice between configuring your server for either locally redundant backups or geographically redundant backups at server creation.</span><span class="sxs-lookup"><span data-stu-id="f210b-114">You make the choice between configuring your server for either locally redundant backups or geographically redundant backups at server creation.</span></span> 

> [!NOTE]
> <span data-ttu-id="f210b-115">After a server is created, the kind of redundancy it has, geographically redundant vs locally redundant, can't be switched.</span><span class="sxs-lookup"><span data-stu-id="f210b-115">After a server is created, the kind of redundancy it has, geographically redundant vs locally redundant, can't be switched.</span></span>
>

<span data-ttu-id="f210b-116">While creating a server via the `az mysql server create` command, the `--geo-redundant-backup` parameter decides your Backup Redundancy Option.</span><span class="sxs-lookup"><span data-stu-id="f210b-116">While creating a server via the `az mysql server create` command, the `--geo-redundant-backup` parameter decides your Backup Redundancy Option.</span></span> <span data-ttu-id="f210b-117">If `Enabled`, geo redundant backups are taken.</span><span class="sxs-lookup"><span data-stu-id="f210b-117">If `Enabled`, geo redundant backups are taken.</span></span> <span data-ttu-id="f210b-118">Or if `Disabled` locally redundant backups are taken.</span><span class="sxs-lookup"><span data-stu-id="f210b-118">Or if `Disabled` locally redundant backups are taken.</span></span> 

<span data-ttu-id="f210b-119">The backup retention period is set by the parameter `--backup-retention`.</span><span class="sxs-lookup"><span data-stu-id="f210b-119">The backup retention period is set by the parameter `--backup-retention`.</span></span> 

<span data-ttu-id="f210b-120">For more information about setting these values during create, see the [Azure Database for MySQL server CLI Quickstart](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f210b-120">For more information about setting these values during create, see the [Azure Database for MySQL server CLI Quickstart](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="f210b-121">The backup retention period of a server can be changed as follows:</span><span class="sxs-lookup"><span data-stu-id="f210b-121">The backup retention period of a server can be changed as follows:</span></span>

```azurecli-interactive
az mysql server update --name mydemoserver --resource-group myresourcegroup --backup-retention 10
```

<span data-ttu-id="f210b-122">The preceding example changes the backup retention period of mydemoserver to 10 days.</span><span class="sxs-lookup"><span data-stu-id="f210b-122">The preceding example changes the backup retention period of mydemoserver to 10 days.</span></span>

<span data-ttu-id="f210b-123">The backup retention period governs how far back in time a point-in-time restore can be retrieved, since it's based on backups available.</span><span class="sxs-lookup"><span data-stu-id="f210b-123">The backup retention period governs how far back in time a point-in-time restore can be retrieved, since it's based on backups available.</span></span> <span data-ttu-id="f210b-124">Point-in-time restore is described further in the next section.</span><span class="sxs-lookup"><span data-stu-id="f210b-124">Point-in-time restore is described further in the next section.</span></span>

## <a name="server-point-in-time-restore"></a><span data-ttu-id="f210b-125">Server point-in-time restore</span><span class="sxs-lookup"><span data-stu-id="f210b-125">Server point-in-time restore</span></span>
<span data-ttu-id="f210b-126">You can restore the server to a previous point in time.</span><span class="sxs-lookup"><span data-stu-id="f210b-126">You can restore the server to a previous point in time.</span></span> <span data-ttu-id="f210b-127">The restored data is copied to a new server, and the existing server is left as is.</span><span class="sxs-lookup"><span data-stu-id="f210b-127">The restored data is copied to a new server, and the existing server is left as is.</span></span> <span data-ttu-id="f210b-128">For example, if a table is accidentally dropped at noon today, you can restore to the time just before noon.</span><span class="sxs-lookup"><span data-stu-id="f210b-128">For example, if a table is accidentally dropped at noon today, you can restore to the time just before noon.</span></span> <span data-ttu-id="f210b-129">Then, you can retrieve the missing table and data from the restored copy of the server.</span><span class="sxs-lookup"><span data-stu-id="f210b-129">Then, you can retrieve the missing table and data from the restored copy of the server.</span></span> 

<span data-ttu-id="f210b-130">To restore the server, use the Azure CLI [az mysql server restore](/cli/azure/mysql/server#az-mysql-server-restore) command.</span><span class="sxs-lookup"><span data-stu-id="f210b-130">To restore the server, use the Azure CLI [az mysql server restore](/cli/azure/mysql/server#az-mysql-server-restore) command.</span></span>

### <a name="run-the-restore-command"></a><span data-ttu-id="f210b-131">Run the restore command</span><span class="sxs-lookup"><span data-stu-id="f210b-131">Run the restore command</span></span>

<span data-ttu-id="f210b-132">To restore the server, at the Azure CLI command prompt, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="f210b-132">To restore the server, at the Azure CLI command prompt, enter the following command:</span></span>

```azurecli-interactive
az mysql server restore --resource-group myresourcegroup --name mydemoserver-restored --restore-point-in-time 2018-03-13T13:59:00Z --source-server mydemoserver
```

<span data-ttu-id="f210b-133">The `az mysql server restore` command requires the following parameters:</span><span class="sxs-lookup"><span data-stu-id="f210b-133">The `az mysql server restore` command requires the following parameters:</span></span>
| <span data-ttu-id="f210b-134">Setting</span><span class="sxs-lookup"><span data-stu-id="f210b-134">Setting</span></span> | <span data-ttu-id="f210b-135">Suggested value</span><span class="sxs-lookup"><span data-stu-id="f210b-135">Suggested value</span></span> | <span data-ttu-id="f210b-136">Description</span><span class="sxs-lookup"><span data-stu-id="f210b-136">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="f210b-137">resource-group</span><span class="sxs-lookup"><span data-stu-id="f210b-137">resource-group</span></span> |  <span data-ttu-id="f210b-138">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="f210b-138">myresourcegroup</span></span> |  <span data-ttu-id="f210b-139">The resource group where the source server exists.</span><span class="sxs-lookup"><span data-stu-id="f210b-139">The resource group where the source server exists.</span></span>  |
| <span data-ttu-id="f210b-140">name</span><span class="sxs-lookup"><span data-stu-id="f210b-140">name</span></span> | <span data-ttu-id="f210b-141">mydemoserver-restored</span><span class="sxs-lookup"><span data-stu-id="f210b-141">mydemoserver-restored</span></span> | <span data-ttu-id="f210b-142">The name of the new server that is created by the restore command.</span><span class="sxs-lookup"><span data-stu-id="f210b-142">The name of the new server that is created by the restore command.</span></span> |
| <span data-ttu-id="f210b-143">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="f210b-143">restore-point-in-time</span></span> | <span data-ttu-id="f210b-144">2018-03-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="f210b-144">2018-03-13T13:59:00Z</span></span> | <span data-ttu-id="f210b-145">Select a point in time to restore to.</span><span class="sxs-lookup"><span data-stu-id="f210b-145">Select a point in time to restore to.</span></span> <span data-ttu-id="f210b-146">This date and time must be within the source server's backup retention period.</span><span class="sxs-lookup"><span data-stu-id="f210b-146">This date and time must be within the source server's backup retention period.</span></span> <span data-ttu-id="f210b-147">Use the ISO8601 date and time format.</span><span class="sxs-lookup"><span data-stu-id="f210b-147">Use the ISO8601 date and time format.</span></span> <span data-ttu-id="f210b-148">For example, you can use your own local time zone, such as `2018-03-13T05:59:00-08:00`.</span><span class="sxs-lookup"><span data-stu-id="f210b-148">For example, you can use your own local time zone, such as `2018-03-13T05:59:00-08:00`.</span></span> <span data-ttu-id="f210b-149">You can also use the UTC Zulu format, for example, `2018-03-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="f210b-149">You can also use the UTC Zulu format, for example, `2018-03-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="f210b-150">source-server</span><span class="sxs-lookup"><span data-stu-id="f210b-150">source-server</span></span> | <span data-ttu-id="f210b-151">mydemoserver</span><span class="sxs-lookup"><span data-stu-id="f210b-151">mydemoserver</span></span> | <span data-ttu-id="f210b-152">The name or ID of the source server to restore from.</span><span class="sxs-lookup"><span data-stu-id="f210b-152">The name or ID of the source server to restore from.</span></span> |

<span data-ttu-id="f210b-153">When you restore a server to an earlier point in time, a new server is created.</span><span class="sxs-lookup"><span data-stu-id="f210b-153">When you restore a server to an earlier point in time, a new server is created.</span></span> <span data-ttu-id="f210b-154">The original server and its databases from the specified point in time are copied to the new server.</span><span class="sxs-lookup"><span data-stu-id="f210b-154">The original server and its databases from the specified point in time are copied to the new server.</span></span>

<span data-ttu-id="f210b-155">The location and pricing tier values for the restored server remain the same as the original server.</span><span class="sxs-lookup"><span data-stu-id="f210b-155">The location and pricing tier values for the restored server remain the same as the original server.</span></span> 

<span data-ttu-id="f210b-156">After the restore process finishes, locate the new server and verify that the data is restored as expected.</span><span class="sxs-lookup"><span data-stu-id="f210b-156">After the restore process finishes, locate the new server and verify that the data is restored as expected.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="f210b-157">Geo restore</span><span class="sxs-lookup"><span data-stu-id="f210b-157">Geo restore</span></span>
<span data-ttu-id="f210b-158">If you configured your server for geographically redundant backups, a new server can be created from the backup of that existing server.</span><span class="sxs-lookup"><span data-stu-id="f210b-158">If you configured your server for geographically redundant backups, a new server can be created from the backup of that existing server.</span></span> <span data-ttu-id="f210b-159">This new server can be created in any region that Azure Database for MySQL is available.</span><span class="sxs-lookup"><span data-stu-id="f210b-159">This new server can be created in any region that Azure Database for MySQL is available.</span></span>  

<span data-ttu-id="f210b-160">To create a server using a geo redundant backup, use the Azure CLI `az mysql server georestore` command.</span><span class="sxs-lookup"><span data-stu-id="f210b-160">To create a server using a geo redundant backup, use the Azure CLI `az mysql server georestore` command.</span></span>

> [!NOTE]
> <span data-ttu-id="f210b-161">When a server is first created it may not be immediately available for geo restore.</span><span class="sxs-lookup"><span data-stu-id="f210b-161">When a server is first created it may not be immediately available for geo restore.</span></span> <span data-ttu-id="f210b-162">It may take a few hours for the necessary metadata to be populated.</span><span class="sxs-lookup"><span data-stu-id="f210b-162">It may take a few hours for the necessary metadata to be populated.</span></span>
>

<span data-ttu-id="f210b-163">To geo restore the server, at the Azure CLI command prompt, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="f210b-163">To geo restore the server, at the Azure CLI command prompt, enter the following command:</span></span>

```azurecli-interactive
az mysql server georestore --resource-group myresourcegroup --name mydemoserver-georestored --source-server mydemoserver --location eastus --sku-name GP_Gen4_8 
```
<span data-ttu-id="f210b-164">This command creates a new server called *mydemoserver-georestored* in East US that will belong to *myresourcegroup*.</span><span class="sxs-lookup"><span data-stu-id="f210b-164">This command creates a new server called *mydemoserver-georestored* in East US that will belong to *myresourcegroup*.</span></span> <span data-ttu-id="f210b-165">It is a General Purpose, Gen 4 server with 8 vCores.</span><span class="sxs-lookup"><span data-stu-id="f210b-165">It is a General Purpose, Gen 4 server with 8 vCores.</span></span> <span data-ttu-id="f210b-166">The server is created from the geo-redundant backup of *mydemoserver*, which is also in the resource group *myresourcegroup*</span><span class="sxs-lookup"><span data-stu-id="f210b-166">The server is created from the geo-redundant backup of *mydemoserver*, which is also in the resource group *myresourcegroup*</span></span>

<span data-ttu-id="f210b-167">If you want to create the new server in a different resource group from the existing server, then in the `--source-server` parameter you would qualify the server name as in the following example:</span><span class="sxs-lookup"><span data-stu-id="f210b-167">If you want to create the new server in a different resource group from the existing server, then in the `--source-server` parameter you would qualify the server name as in the following example:</span></span>

```azurecli-interactive
az mysql server georestore --resource-group newresourcegroup --name mydemoserver-georestored --source-server "/subscriptions/$<subscription ID>/resourceGroups/$<resource group ID>/providers/Microsoft.DBforMySQL/servers/mydemoserver" --location eastus --sku-name GP_Gen4_8

```

<span data-ttu-id="f210b-168">The `az mysql server georestore` command requies the following parameters:</span><span class="sxs-lookup"><span data-stu-id="f210b-168">The `az mysql server georestore` command requies the following parameters:</span></span>
| <span data-ttu-id="f210b-169">Setting</span><span class="sxs-lookup"><span data-stu-id="f210b-169">Setting</span></span> | <span data-ttu-id="f210b-170">Suggested value</span><span class="sxs-lookup"><span data-stu-id="f210b-170">Suggested value</span></span> | <span data-ttu-id="f210b-171">Description</span><span class="sxs-lookup"><span data-stu-id="f210b-171">Description</span></span>  |
| --- | --- | --- |
|<span data-ttu-id="f210b-172">resource-group</span><span class="sxs-lookup"><span data-stu-id="f210b-172">resource-group</span></span>| <span data-ttu-id="f210b-173">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="f210b-173">myresourcegroup</span></span> | <span data-ttu-id="f210b-174">The name of the resource group the new server will belong to.</span><span class="sxs-lookup"><span data-stu-id="f210b-174">The name of the resource group the new server will belong to.</span></span>|
|<span data-ttu-id="f210b-175">name</span><span class="sxs-lookup"><span data-stu-id="f210b-175">name</span></span> | <span data-ttu-id="f210b-176">mydemoserver-georestored</span><span class="sxs-lookup"><span data-stu-id="f210b-176">mydemoserver-georestored</span></span> | <span data-ttu-id="f210b-177">The name of the new server.</span><span class="sxs-lookup"><span data-stu-id="f210b-177">The name of the new server.</span></span> |
|<span data-ttu-id="f210b-178">source-server</span><span class="sxs-lookup"><span data-stu-id="f210b-178">source-server</span></span> | <span data-ttu-id="f210b-179">mydemoserver</span><span class="sxs-lookup"><span data-stu-id="f210b-179">mydemoserver</span></span> | <span data-ttu-id="f210b-180">The name of the existing server whose geo redundant backups are used.</span><span class="sxs-lookup"><span data-stu-id="f210b-180">The name of the existing server whose geo redundant backups are used.</span></span> |
|<span data-ttu-id="f210b-181">location</span><span class="sxs-lookup"><span data-stu-id="f210b-181">location</span></span> | <span data-ttu-id="f210b-182">eastus</span><span class="sxs-lookup"><span data-stu-id="f210b-182">eastus</span></span> | <span data-ttu-id="f210b-183">The location of the new server.</span><span class="sxs-lookup"><span data-stu-id="f210b-183">The location of the new server.</span></span> |
|<span data-ttu-id="f210b-184">sku-name</span><span class="sxs-lookup"><span data-stu-id="f210b-184">sku-name</span></span>| <span data-ttu-id="f210b-185">GP_Gen4_8</span><span class="sxs-lookup"><span data-stu-id="f210b-185">GP_Gen4_8</span></span> | <span data-ttu-id="f210b-186">This parameter sets the pricing tier, compute generation, and number of vCores of the new server.</span><span class="sxs-lookup"><span data-stu-id="f210b-186">This parameter sets the pricing tier, compute generation, and number of vCores of the new server.</span></span> <span data-ttu-id="f210b-187">GP_Gen4_8 maps to a General Purpose, Gen 4 server with 8 vCores.</span><span class="sxs-lookup"><span data-stu-id="f210b-187">GP_Gen4_8 maps to a General Purpose, Gen 4 server with 8 vCores.</span></span>|


>[!Important]
><span data-ttu-id="f210b-188">When creating a new server by a geo restore, it inherits the same storage size and pricing tier as the source server.</span><span class="sxs-lookup"><span data-stu-id="f210b-188">When creating a new server by a geo restore, it inherits the same storage size and pricing tier as the source server.</span></span> <span data-ttu-id="f210b-189">These values cannot be changed during creation.</span><span class="sxs-lookup"><span data-stu-id="f210b-189">These values cannot be changed during creation.</span></span> <span data-ttu-id="f210b-190">After the new server is created, its storage size can be scaled up.</span><span class="sxs-lookup"><span data-stu-id="f210b-190">After the new server is created, its storage size can be scaled up.</span></span>

<span data-ttu-id="f210b-191">After the restore process finishes, locate the new server and verify that the data is restored as expected.</span><span class="sxs-lookup"><span data-stu-id="f210b-191">After the restore process finishes, locate the new server and verify that the data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f210b-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="f210b-192">Next steps</span></span>
- <span data-ttu-id="f210b-193">Learn more about the service's [backups](concepts-backup.md).</span><span class="sxs-lookup"><span data-stu-id="f210b-193">Learn more about the service's [backups](concepts-backup.md).</span></span>
- <span data-ttu-id="f210b-194">Learn more about [business continuity](concepts-business-continuity.md) options.</span><span class="sxs-lookup"><span data-stu-id="f210b-194">Learn more about [business continuity](concepts-business-continuity.md) options.</span></span>
