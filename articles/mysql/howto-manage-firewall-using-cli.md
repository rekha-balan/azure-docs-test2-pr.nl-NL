---
title: Create and manage Azure Database for MySQL firewall rules using Azure CLI
description: This article describes how to create and manage Azure Database for MySQL firewall rules using Azure CLI command-line.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.devlang: azure-cli
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: e6bb06d8ae46afbb946754113e1d81a90e3ddc57
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869559"
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-by-using-the-azure-cli"></a><span data-ttu-id="3ec2c-103">Create and manage Azure Database for MySQL firewall rules by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3ec2c-103">Create and manage Azure Database for MySQL firewall rules by using the Azure CLI</span></span>
<span data-ttu-id="3ec2c-104">Server-level firewall rules allow administrators to manage access to an Azure Database for MySQL Server from a specific IP address or a range of IP addresses.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-104">Server-level firewall rules allow administrators to manage access to an Azure Database for MySQL Server from a specific IP address or a range of IP addresses.</span></span> <span data-ttu-id="3ec2c-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="3ec2c-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="3ec2c-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ec2c-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3ec2c-107">Prerequisites</span></span>
* <span data-ttu-id="3ec2c-108">[Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3ec2c-108">[Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="3ec2c-109">An [Azure Database for MySQL server and database](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3ec2c-109">An [Azure Database for MySQL server and database](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="3ec2c-110">Firewall rule commands:</span><span class="sxs-lookup"><span data-stu-id="3ec2c-110">Firewall rule commands:</span></span>
<span data-ttu-id="3ec2c-111">The **az mysql server firewall-rule** command is used from the Azure CLI to create, delete, list, show, and update firewall rules.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-111">The **az mysql server firewall-rule** command is used from the Azure CLI to create, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="3ec2c-112">Commands:</span><span class="sxs-lookup"><span data-stu-id="3ec2c-112">Commands:</span></span>
- <span data-ttu-id="3ec2c-113">**create**: Create an Azure MySQL server firewall rule.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-113">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="3ec2c-114">**delete**: Delete an Azure MySQL server firewall rule.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-114">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="3ec2c-115">**list**: List the Azure MySQL server firewall rules.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-115">**list**: List the Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="3ec2c-116">**show**: Show the details of an Azure MySQL server firewall rule.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-116">**show**: Show the details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="3ec2c-117">**update**: Update an Azure MySQL server firewall rule.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-117">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="log-in-to-azure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="3ec2c-118">Log in to Azure and list your Azure Database for MySQL Servers</span><span class="sxs-lookup"><span data-stu-id="3ec2c-118">Log in to Azure and list your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="3ec2c-119">Securely connect Azure CLI with your Azure account by using the **az login** command.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-119">Securely connect Azure CLI with your Azure account by using the **az login** command.</span></span>

1. <span data-ttu-id="3ec2c-120">From the command-line, run the following command:</span><span class="sxs-lookup"><span data-stu-id="3ec2c-120">From the command-line, run the following command:</span></span>
```azurecli
az login
```
<span data-ttu-id="3ec2c-121">This command outputs a code to use in the next step.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-121">This command outputs a code to use in the next step.</span></span>

2. <span data-ttu-id="3ec2c-122">Use a web browser to open the page [https://aka.ms/devicelogin](https://aka.ms/devicelogin), and then enter the code.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-122">Use a web browser to open the page [https://aka.ms/devicelogin](https://aka.ms/devicelogin), and then enter the code.</span></span>

3. <span data-ttu-id="3ec2c-123">At the prompt, log in using your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-123">At the prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="3ec2c-124">After your login is authorized, a list of subscriptions is printed in the console.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-124">After your login is authorized, a list of subscriptions is printed in the console.</span></span> <span data-ttu-id="3ec2c-125">Copy the ID of the desired subscription to set the current subscription to use.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-125">Copy the ID of the desired subscription to set the current subscription to use.</span></span> <span data-ttu-id="3ec2c-126">Use the [az account set](/cli/azure/account#az-account-set) command.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-126">Use the [az account set](/cli/azure/account#az-account-set) command.</span></span>
   ```azurecli-interactive
   az account set --subscription <your subscription id>
   ```

5. <span data-ttu-id="3ec2c-127">List the Azure Databases for MySQL servers for your subscription and resource group if you are unsure of the names.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-127">List the Azure Databases for MySQL servers for your subscription and resource group if you are unsure of the names.</span></span> <span data-ttu-id="3ec2c-128">Use the [az mysql server list](/cli/azure/mysql/server#az-mysql-server-list) command.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-128">Use the [az mysql server list](/cli/azure/mysql/server#az-mysql-server-list) command.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myresourcegroup
   ```

   <span data-ttu-id="3ec2c-129">Note the name attribute in the listing, which you need to specify the MySQL server to work on.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-129">Note the name attribute in the listing, which you need to specify the MySQL server to work on.</span></span> <span data-ttu-id="3ec2c-130">If needed, confirm the details for that server and using the name attribute to ensure it is correct.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-130">If needed, confirm the details for that server and using the name attribute to ensure it is correct.</span></span> <span data-ttu-id="3ec2c-131">Use the [az mysql server show](/cli/azure/mysql/server#az-mysql-server-show) command.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-131">Use the [az mysql server show](/cli/azure/mysql/server#az-mysql-server-show) command.</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myresourcegroup --name mydemoserver
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="3ec2c-132">List firewall rules on Azure Database for MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ec2c-132">List firewall rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="3ec2c-133">Using the server name and the resource group name, list the existing server firewall rules on the server.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-133">Using the server name and the resource group name, list the existing server firewall rules on the server.</span></span> <span data-ttu-id="3ec2c-134">Use the [az mysql server firewall list](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-list) command.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-134">Use the [az mysql server firewall list](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-list) command.</span></span>  <span data-ttu-id="3ec2c-135">Notice that the server name attribute is specified in the **--server** switch and not in the **--name** switch.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-135">Notice that the server name attribute is specified in the **--server** switch and not in the **--name** switch.</span></span> 
```azurecli-interactive
az mysql server firewall-rule list --resource-group myresourcegroup --server-name mydemoserver
```
<span data-ttu-id="3ec2c-136">The output lists the rules, if any, in JSON format (by default).</span><span class="sxs-lookup"><span data-stu-id="3ec2c-136">The output lists the rules, if any, in JSON format (by default).</span></span> <span data-ttu-id="3ec2c-137">You can use the **--output table** switch to output the results in a more readable table format.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-137">You can use the **--output table** switch to output the results in a more readable table format.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myresourcegroup --server-name mydemoserver --output table
```
## <a name="create-a-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="3ec2c-138">Create a firewall rule on Azure Database for MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ec2c-138">Create a firewall rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="3ec2c-139">Using the Azure MySQL server name and the resource group name, create a new firewall rule on the server.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-139">Using the Azure MySQL server name and the resource group name, create a new firewall rule on the server.</span></span> <span data-ttu-id="3ec2c-140">Use the [az mysql server firewall create](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-create) command.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-140">Use the [az mysql server firewall create](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-create) command.</span></span> <span data-ttu-id="3ec2c-141">Provide a name for the rule, as well as the start IP and end IP (to provide access to a range of IP addresses) for the rule.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-141">Provide a name for the rule, as well as the start IP and end IP (to provide access to a range of IP addresses) for the rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server-name mydemoserver --name FirewallRule1 --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```

<span data-ttu-id="3ec2c-142">To allow access for a single IP address, provide the same IP address as the Start IP and End IP, as in this example.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-142">To allow access for a single IP address, provide the same IP address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server-name mydemoserver --name FirewallRule1 --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```

<span data-ttu-id="3ec2c-143">To allow applications from Azure IP addresses to connect to your Azure Database for MySQL server, provide the IP address 0.0.0.0 as the Start IP and End IP, as in this example.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-143">To allow applications from Azure IP addresses to connect to your Azure Database for MySQL server, provide the IP address 0.0.0.0 as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server mysql --name "AllowAllWindowsAzureIps" --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!IMPORTANT]
> <span data-ttu-id="3ec2c-144">This option configures the firewall to allow all connections from Azure including connections from the subscriptions of other customers.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-144">This option configures the firewall to allow all connections from Azure including connections from the subscriptions of other customers.</span></span> <span data-ttu-id="3ec2c-145">When selecting this option, make sure your login and user permissions limit access to only authorized users.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-145">When selecting this option, make sure your login and user permissions limit access to only authorized users.</span></span>
> 

<span data-ttu-id="3ec2c-146">Upon success, each create command output lists the details of the firewall rule you have created, in JSON format (by default).</span><span class="sxs-lookup"><span data-stu-id="3ec2c-146">Upon success, each create command output lists the details of the firewall rule you have created, in JSON format (by default).</span></span> <span data-ttu-id="3ec2c-147">If there is a failure, the output shows error message text instead.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-147">If there is a failure, the output shows error message text instead.</span></span>

## <a name="update-a-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="3ec2c-148">Update a firewall rule on Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="3ec2c-148">Update a firewall rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="3ec2c-149">Using the Azure MySQL server name and the resource group name, update an existing firewall rule on the server.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-149">Using the Azure MySQL server name and the resource group name, update an existing firewall rule on the server.</span></span> <span data-ttu-id="3ec2c-150">Use the [az mysql server firewall update](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-update) command.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-150">Use the [az mysql server firewall update](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-update) command.</span></span> <span data-ttu-id="3ec2c-151">Provide the name of the existing firewall rule as input, as well as the start IP and end IP attributes to update.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-151">Provide the name of the existing firewall rule as input, as well as the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myresourcegroup --server-name mydemoserver --name FirewallRule1 --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="3ec2c-152">Upon success, the command output lists the details of the firewall rule you have updated, in JSON format (by default).</span><span class="sxs-lookup"><span data-stu-id="3ec2c-152">Upon success, the command output lists the details of the firewall rule you have updated, in JSON format (by default).</span></span> <span data-ttu-id="3ec2c-153">If there is a failure, the output shows error message text instead.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-153">If there is a failure, the output shows error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="3ec2c-154">If the firewall rule does not exist, the rule is created by the update command.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-154">If the firewall rule does not exist, the rule is created by the update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="3ec2c-155">Show firewall rule details on Azure Database for MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ec2c-155">Show firewall rule details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="3ec2c-156">Using the Azure MySQL server name and the resource group name, show the existing firewall rule details from the server.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-156">Using the Azure MySQL server name and the resource group name, show the existing firewall rule details from the server.</span></span> <span data-ttu-id="3ec2c-157">Use the [az mysql server firewall show](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-show) command.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-157">Use the [az mysql server firewall show](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-show) command.</span></span> <span data-ttu-id="3ec2c-158">Provide the name of the existing firewall rule as input.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-158">Provide the name of the existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myresourcegroup --server-name mydemoserver --name FirewallRule1
```
<span data-ttu-id="3ec2c-159">Upon success, the command output lists the details of the firewall rule you have specified, in JSON format (by default).</span><span class="sxs-lookup"><span data-stu-id="3ec2c-159">Upon success, the command output lists the details of the firewall rule you have specified, in JSON format (by default).</span></span> <span data-ttu-id="3ec2c-160">If there is a failure, the output shows error message text instead.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-160">If there is a failure, the output shows error message text instead.</span></span>

## <a name="delete-a-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="3ec2c-161">Delete a firewall rule on Azure Database for MySQL Server</span><span class="sxs-lookup"><span data-stu-id="3ec2c-161">Delete a firewall rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="3ec2c-162">Using the Azure MySQL server name and the resource group name, remove an existing firewall rule from the server.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-162">Using the Azure MySQL server name and the resource group name, remove an existing firewall rule from the server.</span></span> <span data-ttu-id="3ec2c-163">Use the [az mysql server firewall delete](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-delete) command.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-163">Use the [az mysql server firewall delete](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-delete) command.</span></span> <span data-ttu-id="3ec2c-164">Provide the name of the existing firewall rule.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-164">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myresourcegroup --server-name mydemoserver --name FirewallRule1
```
<span data-ttu-id="3ec2c-165">Upon success, there is no output.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-165">Upon success, there is no output.</span></span> <span data-ttu-id="3ec2c-166">Upon failure, error message text displays.</span><span class="sxs-lookup"><span data-stu-id="3ec2c-166">Upon failure, error message text displays.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ec2c-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="3ec2c-167">Next steps</span></span>
- <span data-ttu-id="3ec2c-168">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md).</span><span class="sxs-lookup"><span data-stu-id="3ec2c-168">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md).</span></span>
- <span data-ttu-id="3ec2c-169">[Create and manage Azure Database for MySQL firewall rules using the Azure portal](./howto-manage-firewall-using-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3ec2c-169">[Create and manage Azure Database for MySQL firewall rules using the Azure portal](./howto-manage-firewall-using-portal.md).</span></span>
