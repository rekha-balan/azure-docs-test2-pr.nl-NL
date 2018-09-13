---
title: Azure CLI script - Create an Azure Database for MySQL
description: This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 02/28/2018
ms.openlocfilehash: acdc2b40530be190212b8b8f35443ce8d4ee4bde
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967200"
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="45ad3-103">Create a MySQL server and configure a firewall rule using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="45ad3-103">Create a MySQL server and configure a firewall rule using the Azure CLI</span></span>
<span data-ttu-id="45ad3-104">This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.</span><span class="sxs-lookup"><span data-stu-id="45ad3-104">This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="45ad3-105">Once the script runs successfully, the MySQL server is accessible by all Azure services and the configured IP address.</span><span class="sxs-lookup"><span data-stu-id="45ad3-105">Once the script runs successfully, the MySQL server is accessible by all Azure services and the configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="45ad3-106">If you choose to run the CLI locally, this article requires Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="45ad3-106">If you choose to run the CLI locally, this article requires Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="45ad3-107">Check the version by running `az --version`.</span><span class="sxs-lookup"><span data-stu-id="45ad3-107">Check the version by running `az --version`.</span></span> <span data-ttu-id="45ad3-108">See [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) to install or upgrade your version of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="45ad3-108">See [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) to install or upgrade your version of Azure CLI.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="45ad3-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="45ad3-109">Sample script</span></span>
<span data-ttu-id="45ad3-110">In this sample script, edit the highlighted lines to update the admin username and password to your own.</span><span class="sxs-lookup"><span data-stu-id="45ad3-110">In this sample script, edit the highlighted lines to update the admin username and password to your own.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=18-19 "Create an Azure Database for MySQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="45ad3-111">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="45ad3-111">Clean up deployment</span></span>
<span data-ttu-id="45ad3-112">Use the following command to remove the resource group and all resources associated with it after the script has been run.</span><span class="sxs-lookup"><span data-stu-id="45ad3-112">Use the following command to remove the resource group and all resources associated with it after the script has been run.</span></span> 
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete the resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="45ad3-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="45ad3-113">Script explanation</span></span>
<span data-ttu-id="45ad3-114">This script uses the commands outlined in the following table:</span><span class="sxs-lookup"><span data-stu-id="45ad3-114">This script uses the commands outlined in the following table:</span></span>

| <span data-ttu-id="45ad3-115">**Command**</span><span class="sxs-lookup"><span data-stu-id="45ad3-115">**Command**</span></span> | <span data-ttu-id="45ad3-116">**Notes**</span><span class="sxs-lookup"><span data-stu-id="45ad3-116">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="45ad3-117">az group create</span><span class="sxs-lookup"><span data-stu-id="45ad3-117">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="45ad3-118">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="45ad3-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="45ad3-119">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="45ad3-119">az mysql server create</span></span>](/cli/azure/mysql/server#az-msql-server-create) | <span data-ttu-id="45ad3-120">Creates a MySQL server that hosts the databases.</span><span class="sxs-lookup"><span data-stu-id="45ad3-120">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="45ad3-121">az mysql server firewall create</span><span class="sxs-lookup"><span data-stu-id="45ad3-121">az mysql server firewall create</span></span>](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-create) | <span data-ttu-id="45ad3-122">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span><span class="sxs-lookup"><span data-stu-id="45ad3-122">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span></span> |
| [<span data-ttu-id="45ad3-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="45ad3-123">az group delete</span></span>](/cli/azure/group#az-group-delete) | <span data-ttu-id="45ad3-124">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="45ad3-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="45ad3-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="45ad3-125">Next steps</span></span>
- <span data-ttu-id="45ad3-126">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="45ad3-126">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure).</span></span>
- <span data-ttu-id="45ad3-127">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="45ad3-127">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
