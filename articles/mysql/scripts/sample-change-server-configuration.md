---
title: Azure CLI script - Change server configurations
description: This sample CLI script lists all available server configurations and updates the value of innodb_lock_wait_timeout.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 02/28/2018
ms.openlocfilehash: 75b1228df8bc19ced1d8377768c08048e6ef9150
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870352"
---
# <a name="list-and-update-configurations-of-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="bcdf9-103">List and update configurations of an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bcdf9-103">List and update configurations of an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="bcdf9-104">This sample CLI script lists all available configuration parameters as well as their allowable values for Azure Database for MySQL server, and sets the *innodb_lock_wait_timeout* to a value that is other than the default one.</span><span class="sxs-lookup"><span data-stu-id="bcdf9-104">This sample CLI script lists all available configuration parameters as well as their allowable values for Azure Database for MySQL server, and sets the *innodb_lock_wait_timeout* to a value that is other than the default one.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bcdf9-105">If you choose to run the CLI locally, this article requires Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="bcdf9-105">If you choose to run the CLI locally, this article requires Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bcdf9-106">Check the version by running `az --version`.</span><span class="sxs-lookup"><span data-stu-id="bcdf9-106">Check the version by running `az --version`.</span></span> <span data-ttu-id="bcdf9-107">See [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) to install or upgrade your version of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="bcdf9-107">See [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) to install or upgrade your version of Azure CLI.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bcdf9-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="bcdf9-108">Sample script</span></span>
<span data-ttu-id="bcdf9-109">In this sample script, edit the highlighted lines to update the admin username and password to your own.</span><span class="sxs-lookup"><span data-stu-id="bcdf9-109">In this sample script, edit the highlighted lines to update the admin username and password to your own.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/change-server-configurations/change-server-configurations.sh?highlight=18-19 "List and update configurations of Azure Database for MySQL.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="bcdf9-110">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="bcdf9-110">Clean up deployment</span></span>
<span data-ttu-id="bcdf9-111">Use the following command to remove the resource group and all resources associated with it after the script has been run.</span><span class="sxs-lookup"><span data-stu-id="bcdf9-111">Use the following command to remove the resource group and all resources associated with it after the script has been run.</span></span> 
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/change-server-configurations/delete-mysql.sh  "Delete the resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="bcdf9-112">Script explanation</span><span class="sxs-lookup"><span data-stu-id="bcdf9-112">Script explanation</span></span>
<span data-ttu-id="bcdf9-113">This script uses the commands outlined in the following table:</span><span class="sxs-lookup"><span data-stu-id="bcdf9-113">This script uses the commands outlined in the following table:</span></span>

| <span data-ttu-id="bcdf9-114">**Command**</span><span class="sxs-lookup"><span data-stu-id="bcdf9-114">**Command**</span></span> | <span data-ttu-id="bcdf9-115">**Notes**</span><span class="sxs-lookup"><span data-stu-id="bcdf9-115">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="bcdf9-116">az group create</span><span class="sxs-lookup"><span data-stu-id="bcdf9-116">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="bcdf9-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="bcdf9-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bcdf9-118">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="bcdf9-118">az mysql server create</span></span>](/cli/azure/mysql/server#az-msql-server-create) | <span data-ttu-id="bcdf9-119">Creates a MySQL server that hosts the databases.</span><span class="sxs-lookup"><span data-stu-id="bcdf9-119">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="bcdf9-120">az mysql server configuration list</span><span class="sxs-lookup"><span data-stu-id="bcdf9-120">az mysql server configuration list</span></span>](/cli/azure/mysql/server/configuration#az-msql-server-configuration-list) | <span data-ttu-id="bcdf9-121">List the configurations of an Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="bcdf9-121">List the configurations of an Azure Database for MySQL server.</span></span> |
| [<span data-ttu-id="bcdf9-122">az mysql server configuration set</span><span class="sxs-lookup"><span data-stu-id="bcdf9-122">az mysql server configuration set</span></span>](/cli/azure/mysql/server/configuration#az-msql-server-configuration-set) | <span data-ttu-id="bcdf9-123">Update the configuration of an Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="bcdf9-123">Update the configuration of an Azure Database for MySQL server.</span></span> |
| [<span data-ttu-id="bcdf9-124">az mysql server configuration show</span><span class="sxs-lookup"><span data-stu-id="bcdf9-124">az mysql server configuration show</span></span>](/cli/azure/mysql/server/configuration#az-msql-server-configuration-show) | <span data-ttu-id="bcdf9-125">Show the configuration of an Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="bcdf9-125">Show the configuration of an Azure Database for MySQL server.</span></span> |
| [<span data-ttu-id="bcdf9-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="bcdf9-126">az group delete</span></span>](/cli/azure/group#az-group-delete) | <span data-ttu-id="bcdf9-127">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="bcdf9-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bcdf9-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="bcdf9-128">Next steps</span></span>
- <span data-ttu-id="bcdf9-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="bcdf9-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure).</span></span>
- <span data-ttu-id="bcdf9-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="bcdf9-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="bcdf9-131">For more information on server parameters, see [How To Configure Server Parameters in Azure Database for MySQL](../howto-server-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="bcdf9-131">For more information on server parameters, see [How To Configure Server Parameters in Azure Database for MySQL](../howto-server-parameters.md).</span></span>
