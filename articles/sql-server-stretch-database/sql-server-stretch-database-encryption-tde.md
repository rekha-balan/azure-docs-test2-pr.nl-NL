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
ms.openlocfilehash: ceb355d2ba872ed5d3886c6dc82ca75b1854db0a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819811"
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="70bcb-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span><span class="sxs-lookup"><span data-stu-id="70bcb-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="70bcb-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span><span class="sxs-lookup"><span data-stu-id="70bcb-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="70bcb-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span><span class="sxs-lookup"><span data-stu-id="70bcb-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="70bcb-108">The database encryption key is protected by a built-in server certificate.</span><span class="sxs-lookup"><span data-stu-id="70bcb-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="70bcb-109">The built-in server certificate is unique for each Azure server.</span><span class="sxs-lookup"><span data-stu-id="70bcb-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="70bcb-110">Microsoft automatically rotates these certificates at least every 90 days.</span><span class="sxs-lookup"><span data-stu-id="70bcb-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="70bcb-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span><span class="sxs-lookup"><span data-stu-id="70bcb-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="70bcb-112">Enabling Encryption</span><span class="sxs-lookup"><span data-stu-id="70bcb-112">Enabling Encryption</span></span>
<span data-ttu-id="70bcb-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span><span class="sxs-lookup"><span data-stu-id="70bcb-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="70bcb-114">Open the database in the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="70bcb-114">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="70bcb-115">In the database blade, click the **Settings** button</span><span class="sxs-lookup"><span data-stu-id="70bcb-115">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="70bcb-116">Select the **Transparent data encryption** option ![][1]</span><span class="sxs-lookup"><span data-stu-id="70bcb-116">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="70bcb-117">Select the **On** setting, and then select **Save**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="70bcb-117">Select the **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="70bcb-118">Disabling Encryption</span><span class="sxs-lookup"><span data-stu-id="70bcb-118">Disabling Encryption</span></span>
<span data-ttu-id="70bcb-119">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span><span class="sxs-lookup"><span data-stu-id="70bcb-119">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="70bcb-120">Open the database in the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="70bcb-120">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="70bcb-121">In the database blade, click the **Settings** button</span><span class="sxs-lookup"><span data-stu-id="70bcb-121">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="70bcb-122">Select the **Transparent data encryption** option</span><span class="sxs-lookup"><span data-stu-id="70bcb-122">Select the **Transparent data encryption** option</span></span>
4. <span data-ttu-id="70bcb-123">Select the **Off** setting, and then select **Save**</span><span class="sxs-lookup"><span data-stu-id="70bcb-123">Select the **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
