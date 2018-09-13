---
title: include file
description: include file
services: storage
author: tamram
ms.service: storage
ms.topic: include
ms.date: 09/06/2018
ms.author: tamram
ms.custom: include file
ms.openlocfilehash: 3a3ee0cda3643ac73581f868e47905841d9f1563
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855965"
---
> [!IMPORTANT]
> - <span data-ttu-id="e89cc-103">The preview of Azure AD authentication for blobs and queues is intended for non-production use only.</span><span class="sxs-lookup"><span data-stu-id="e89cc-103">The preview of Azure AD authentication for blobs and queues is intended for non-production use only.</span></span> <span data-ttu-id="e89cc-104">Production service-level agreements (SLAs) are not currently available.</span><span class="sxs-lookup"><span data-stu-id="e89cc-104">Production service-level agreements (SLAs) are not currently available.</span></span> <span data-ttu-id="e89cc-105">If Azure AD authentication is not yet supported for your scenario, continue to use Shared Key authorization or SAS tokens in your applications.</span><span class="sxs-lookup"><span data-stu-id="e89cc-105">If Azure AD authentication is not yet supported for your scenario, continue to use Shared Key authorization or SAS tokens in your applications.</span></span>
>
> - <span data-ttu-id="e89cc-106">During the preview, RBAC role assignments may take up to five minutes to propagate.</span><span class="sxs-lookup"><span data-stu-id="e89cc-106">During the preview, RBAC role assignments may take up to five minutes to propagate.</span></span>
>
> - <span data-ttu-id="e89cc-107">You must use HTTPS to authenticate with Azure AD when calling blob and queue operations.</span><span class="sxs-lookup"><span data-stu-id="e89cc-107">You must use HTTPS to authenticate with Azure AD when calling blob and queue operations.</span></span>
>
> - <span data-ttu-id="e89cc-108">In the preview release, the Azure portal does not use Azure AD credentials to read and write blob and queue data.</span><span class="sxs-lookup"><span data-stu-id="e89cc-108">In the preview release, the Azure portal does not use Azure AD credentials to read and write blob and queue data.</span></span> <span data-ttu-id="e89cc-109">Instead, the portal continues to rely on the account access key.</span><span class="sxs-lookup"><span data-stu-id="e89cc-109">Instead, the portal continues to rely on the account access key.</span></span> <span data-ttu-id="e89cc-110">To view or update blob or queue data in the portal, the user must be assigned an RBAC role that encompasses  [Microsoft.Storage/storageAccounts/listkeys/action](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#storage-account-key-operator-service-role), which grants permissions to call [Storage Accounts - List Keys](https://docs.microsoft.com/rest/api/storagerp/storageaccounts/listkeys).</span><span class="sxs-lookup"><span data-stu-id="e89cc-110">To view or update blob or queue data in the portal, the user must be assigned an RBAC role that encompasses  [Microsoft.Storage/storageAccounts/listkeys/action](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#storage-account-key-operator-service-role), which grants permissions to call [Storage Accounts - List Keys](https://docs.microsoft.com/rest/api/storagerp/storageaccounts/listkeys).</span></span> <span data-ttu-id="e89cc-111">The Contributor and Reader roles for blobs and queues do not currently include the **listkeys** action as part of the preview release and so do not provide data access through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e89cc-111">The Contributor and Reader roles for blobs and queues do not currently include the **listkeys** action as part of the preview release and so do not provide data access through the Azure portal.</span></span> <span data-ttu-id="e89cc-112">To explore identity-based access to blob and queue data during the preview release, use PowerShell or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e89cc-112">To explore identity-based access to blob and queue data during the preview release, use PowerShell or Azure CLI.</span></span>