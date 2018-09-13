---
title: Enable Transparent Data Encryption for Stretch Database - Azure | Microsoft Docs
description: Enable Transparent Data Encryption (TDE) for SQL Server Stretch Database on Azure
services: sql-server-stretch-database
documentationcenter: ''
author: douglaslMS
manager: barbkess
editor: ''
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 38e1909713cbd1c9302cdefa519ec7f17f79752b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555347"
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="9fedf-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span><span class="sxs-lookup"><span data-stu-id="9fedf-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="9fedf-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span><span class="sxs-lookup"><span data-stu-id="9fedf-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="9fedf-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span><span class="sxs-lookup"><span data-stu-id="9fedf-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="9fedf-108">The database encryption key is protected by a built-in server certificate.</span><span class="sxs-lookup"><span data-stu-id="9fedf-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="9fedf-109">The built-in server certificate is unique for each Azure server.</span><span class="sxs-lookup"><span data-stu-id="9fedf-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="9fedf-110">Microsoft automatically rotates these certificates at least every 90 days.</span><span class="sxs-lookup"><span data-stu-id="9fedf-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="9fedf-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span><span class="sxs-lookup"><span data-stu-id="9fedf-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="9fedf-112">Enabling Encryption</span><span class="sxs-lookup"><span data-stu-id="9fedf-112">Enabling Encryption</span></span>
<span data-ttu-id="9fedf-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span><span class="sxs-lookup"><span data-stu-id="9fedf-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="9fedf-114">Open the database in the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="9fedf-114">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="9fedf-115">In the database blade, click the **Settings** button</span><span class="sxs-lookup"><span data-stu-id="9fedf-115">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="9fedf-116">Select the **Transparent data encryption** option ![][1]</span><span class="sxs-lookup"><span data-stu-id="9fedf-116">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="9fedf-117">Select the **On** setting, and then select **Save**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="9fedf-117">Select the **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="9fedf-118">Disabling Encryption</span><span class="sxs-lookup"><span data-stu-id="9fedf-118">Disabling Encryption</span></span>
<span data-ttu-id="9fedf-119">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span><span class="sxs-lookup"><span data-stu-id="9fedf-119">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="9fedf-120">Open the database in the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="9fedf-120">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="9fedf-121">In the database blade, click the **Settings** button</span><span class="sxs-lookup"><span data-stu-id="9fedf-121">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="9fedf-122">Select the **Transparent data encryption** option</span><span class="sxs-lookup"><span data-stu-id="9fedf-122">Select the **Transparent data encryption** option</span></span>
4. <span data-ttu-id="9fedf-123">Select the **Off** setting, and then select **Save**</span><span class="sxs-lookup"><span data-stu-id="9fedf-123">Select the **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-server-stretch-database/media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-server-stretch-database/media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->


