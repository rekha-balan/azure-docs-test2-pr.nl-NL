---
title: Azure CLI script - Restore an Azure Database for MySQL server
description: This sample Azure CLI script shows how to restore an Azure Database for MySQL server and its databases to a previous point in time.
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
ms.openlocfilehash: 5e4eae95eb881ba685f2668073c556373b2e6c10
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855988"
---
# <a name="restore-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="8b53d-103">Restore an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8b53d-103">Restore an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="8b53d-104">This sample CLI script restores a single Azure Database for MySQL server to a previous point in time.</span><span class="sxs-lookup"><span data-stu-id="8b53d-104">This sample CLI script restores a single Azure Database for MySQL server to a previous point in time.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8b53d-105">If you choose to run the CLI locally, this article requires Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="8b53d-105">If you choose to run the CLI locally, this article requires Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8b53d-106">Check the version by running `az --version`.</span><span class="sxs-lookup"><span data-stu-id="8b53d-106">Check the version by running `az --version`.</span></span> <span data-ttu-id="8b53d-107">See [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) to install or upgrade your version of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8b53d-107">See [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) to install or upgrade your version of Azure CLI.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8b53d-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="8b53d-108">Sample script</span></span>
<span data-ttu-id="8b53d-109">In this sample script, edit the highlighted lines to update the admin username and password to your own.</span><span class="sxs-lookup"><span data-stu-id="8b53d-109">In this sample script, edit the highlighted lines to update the admin username and password to your own.</span></span> <span data-ttu-id="8b53d-110">Replace the subscription ID used in the `az monitor` commands with your own subscription ID.</span><span class="sxs-lookup"><span data-stu-id="8b53d-110">Replace the subscription ID used in the `az monitor` commands with your own subscription ID.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/backup-restore-pitr/backup-restore.sh?highlight=18-19 "Restore Azure Database for MySQL.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8b53d-111">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="8b53d-111">Clean up deployment</span></span>
<span data-ttu-id="8b53d-112">Use the following command to remove the resource group and all resources associated with it after the script has been run.</span><span class="sxs-lookup"><span data-stu-id="8b53d-112">Use the following command to remove the resource group and all resources associated with it after the script has been run.</span></span> 
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/backup-restore-pitr/delete-mysql.sh  "Delete the resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="8b53d-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="8b53d-113">Script explanation</span></span>
<span data-ttu-id="8b53d-114">This script uses the commands outlined in the following table:</span><span class="sxs-lookup"><span data-stu-id="8b53d-114">This script uses the commands outlined in the following table:</span></span>

| <span data-ttu-id="8b53d-115">**Command**</span><span class="sxs-lookup"><span data-stu-id="8b53d-115">**Command**</span></span> | <span data-ttu-id="8b53d-116">**Notes**</span><span class="sxs-lookup"><span data-stu-id="8b53d-116">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="8b53d-117">az group create</span><span class="sxs-lookup"><span data-stu-id="8b53d-117">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="8b53d-118">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="8b53d-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8b53d-119">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="8b53d-119">az mysql server create</span></span>](/cli/azure/mysql/server#az-mysql-server-create) | <span data-ttu-id="8b53d-120">Creates a MySQL server that hosts the databases.</span><span class="sxs-lookup"><span data-stu-id="8b53d-120">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="8b53d-121">az mysql server restore</span><span class="sxs-lookup"><span data-stu-id="8b53d-121">az mysql server restore</span></span>](/cli/azure/mysql/server#az-mysql-server-restore) | <span data-ttu-id="8b53d-122">Restore a server from backup.</span><span class="sxs-lookup"><span data-stu-id="8b53d-122">Restore a server from backup.</span></span> |
| [<span data-ttu-id="8b53d-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="8b53d-123">az group delete</span></span>](/cli/azure/group#az-group-delete) | <span data-ttu-id="8b53d-124">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="8b53d-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8b53d-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="8b53d-125">Next steps</span></span>
- <span data-ttu-id="8b53d-126">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="8b53d-126">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure).</span></span>
- <span data-ttu-id="8b53d-127">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="8b53d-127">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>