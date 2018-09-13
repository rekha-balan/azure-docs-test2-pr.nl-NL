---
title: Azure CLI script - Restore an Azure Database for MySQL server to a previous point in time
description: This sample CLI script restores Azure Database for MySQL server to a previous point in time.
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
ms.openlocfilehash: bea3a8057e9b99dc5847e23541d41c5c68393d48
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869827"
---
# <a name="restore-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="884d0-103">Restore an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="884d0-103">Restore an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="884d0-104">This sample CLI script restores a single Azure Database for MySQL server to a previous point in time.</span><span class="sxs-lookup"><span data-stu-id="884d0-104">This sample CLI script restores a single Azure Database for MySQL server to a previous point in time.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="884d0-105">If you choose to install and use the CLI locally, this sample requires that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="884d0-105">If you choose to install and use the CLI locally, this sample requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="884d0-106">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="884d0-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="884d0-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="884d0-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="884d0-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="884d0-108">Sample script</span></span>
<span data-ttu-id="884d0-109">In this sample script, change the highlighted lines to customize the admin username and password.</span><span class="sxs-lookup"><span data-stu-id="884d0-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="884d0-110">Replace the subscription ID used in the az monitor commands with your own subscription ID.</span><span class="sxs-lookup"><span data-stu-id="884d0-110">Replace the subscription ID used in the az monitor commands with your own subscription ID.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/backup-restore-pitr/backup-restore.sh?highlight=18-19 "Restore Azure Database for MySQL.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="884d0-111">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="884d0-111">Clean up deployment</span></span>
<span data-ttu-id="884d0-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="884d0-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/backup-restore-pitr/delete-mysql.sh  "Delete the resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="884d0-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="884d0-113">Script explanation</span></span>
<span data-ttu-id="884d0-114">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="884d0-114">This script uses the following commands.</span></span> <span data-ttu-id="884d0-115">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="884d0-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="884d0-116">**Command**</span><span class="sxs-lookup"><span data-stu-id="884d0-116">**Command**</span></span> | <span data-ttu-id="884d0-117">**Notes**</span><span class="sxs-lookup"><span data-stu-id="884d0-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="884d0-118">az group create</span><span class="sxs-lookup"><span data-stu-id="884d0-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="884d0-119">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="884d0-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="884d0-120">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="884d0-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="884d0-121">Creates a MySQL server that hosts the databases.</span><span class="sxs-lookup"><span data-stu-id="884d0-121">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="884d0-122">az mysql server restore</span><span class="sxs-lookup"><span data-stu-id="884d0-122">az mysql server restore</span></span>](/cli/azure/mysql/server#restore) | <span data-ttu-id="884d0-123">Restore a server from backup.</span><span class="sxs-lookup"><span data-stu-id="884d0-123">Restore a server from backup.</span></span> |
| [<span data-ttu-id="884d0-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="884d0-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="884d0-125">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="884d0-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="884d0-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="884d0-126">Next steps</span></span>
- <span data-ttu-id="884d0-127">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="884d0-127">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure).</span></span>
- <span data-ttu-id="884d0-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="884d0-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
