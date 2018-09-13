---
title: Azure CLI script - Download server logs in Azure Database for MySQL
description: This sample Azure CLI script shows how to enable and download the server logs of an Azure Database for MySQL server.
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
ms.openlocfilehash: 98f1179dd6dff4cd8b0125266899374d80893d26
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870227"
---
# <a name="enable-and-download-server-slow-query-logs-of-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="3c158-103">Enable and download server slow query logs of an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3c158-103">Enable and download server slow query logs of an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="3c158-104">This sample CLI script enables and downloads the slow query logs of a single Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="3c158-104">This sample CLI script enables and downloads the slow query logs of a single Azure Database for MySQL server.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3c158-105">If you choose to run the CLI locally, this article requires Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="3c158-105">If you choose to run the CLI locally, this article requires Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3c158-106">Check the version by running `az --version`.</span><span class="sxs-lookup"><span data-stu-id="3c158-106">Check the version by running `az --version`.</span></span> <span data-ttu-id="3c158-107">See [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) to install or upgrade your version of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="3c158-107">See [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) to install or upgrade your version of Azure CLI.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3c158-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="3c158-108">Sample script</span></span>
<span data-ttu-id="3c158-109">In this sample script, edit the highlighted lines to update the admin username and password to your own.</span><span class="sxs-lookup"><span data-stu-id="3c158-109">In this sample script, edit the highlighted lines to update the admin username and password to your own.</span></span> <span data-ttu-id="3c158-110">Replace the <log_file_name> in the `az monitor` commands with your own server log file name.</span><span class="sxs-lookup"><span data-stu-id="3c158-110">Replace the <log_file_name> in the `az monitor` commands with your own server log file name.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/server-logs/server-logs.sh?highlight=18-19 "Manipulate with server logs.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3c158-111">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="3c158-111">Clean up deployment</span></span>
<span data-ttu-id="3c158-112">Use the following command to remove the resource group and all resources associated with it after the script has been run.</span><span class="sxs-lookup"><span data-stu-id="3c158-112">Use the following command to remove the resource group and all resources associated with it after the script has been run.</span></span> 
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/server-logs/delete-mysql.sh  "Delete the resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="3c158-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="3c158-113">Script explanation</span></span>
<span data-ttu-id="3c158-114">This script uses the commands outlined in the following table:</span><span class="sxs-lookup"><span data-stu-id="3c158-114">This script uses the commands outlined in the following table:</span></span>

| <span data-ttu-id="3c158-115">**Command**</span><span class="sxs-lookup"><span data-stu-id="3c158-115">**Command**</span></span> | <span data-ttu-id="3c158-116">**Notes**</span><span class="sxs-lookup"><span data-stu-id="3c158-116">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="3c158-117">az group create</span><span class="sxs-lookup"><span data-stu-id="3c158-117">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="3c158-118">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="3c158-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3c158-119">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="3c158-119">az mysql server create</span></span>](/cli/azure/mysql/server#az-msql-server-create) | <span data-ttu-id="3c158-120">Creates a MySQL server that hosts the databases.</span><span class="sxs-lookup"><span data-stu-id="3c158-120">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="3c158-121">az mysql server configuration list</span><span class="sxs-lookup"><span data-stu-id="3c158-121">az mysql server configuration list</span></span>](/cli/azure/mysql/server/configuration#az-mysql-server-configuration-list) | <span data-ttu-id="3c158-122">List the configuration values for a server.</span><span class="sxs-lookup"><span data-stu-id="3c158-122">List the configuration values for a server.</span></span> |
| [<span data-ttu-id="3c158-123">az mysql server configuration set</span><span class="sxs-lookup"><span data-stu-id="3c158-123">az mysql server configuration set</span></span>](/cli/azure/mysql/server/configuration#az-mysql-server-configuration-set) | <span data-ttu-id="3c158-124">Update the configuration of a server.</span><span class="sxs-lookup"><span data-stu-id="3c158-124">Update the configuration of a server.</span></span> |
| [<span data-ttu-id="3c158-125">az mysql server-logs list</span><span class="sxs-lookup"><span data-stu-id="3c158-125">az mysql server-logs list</span></span>](/cli/azure/mysql/server-logs#az-mysql-server-logs-list) | <span data-ttu-id="3c158-126">List log files for a server.</span><span class="sxs-lookup"><span data-stu-id="3c158-126">List log files for a server.</span></span> |
| [<span data-ttu-id="3c158-127">az mysql server-logs download</span><span class="sxs-lookup"><span data-stu-id="3c158-127">az mysql server-logs download</span></span>](/cli/azure/mysql/server-logs#az-mysql-server-logs-download) | <span data-ttu-id="3c158-128">Download log files.</span><span class="sxs-lookup"><span data-stu-id="3c158-128">Download log files.</span></span> |
| [<span data-ttu-id="3c158-129">az group delete</span><span class="sxs-lookup"><span data-stu-id="3c158-129">az group delete</span></span>](/cli/azure/group#az-group-delete) | <span data-ttu-id="3c158-130">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="3c158-130">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3c158-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="3c158-131">Next steps</span></span>
- <span data-ttu-id="3c158-132">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="3c158-132">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure).</span></span>
- <span data-ttu-id="3c158-133">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="3c158-133">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
