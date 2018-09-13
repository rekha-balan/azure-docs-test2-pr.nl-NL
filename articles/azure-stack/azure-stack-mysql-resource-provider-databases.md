---
title: Using databases provided by the MySQL Adapter RP on AzureStack | Microsoft Docs
description: How to create and manage MySQL databases provisioned using the MySQL Adapter Resource Provider
services: azure-stack
documentationCenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2018
ms.author: jeffgilb
ms.reviewer: jeffgo
ms.openlocfilehash: 77dca29b0c60726f0a072dd662aba0d12730502a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855651"
---
# <a name="create-mysql-databases"></a><span data-ttu-id="42b50-103">Create MySQL databases</span><span class="sxs-lookup"><span data-stu-id="42b50-103">Create MySQL databases</span></span>

<span data-ttu-id="42b50-104">You can create and manage self-service databases in the user portal.</span><span class="sxs-lookup"><span data-stu-id="42b50-104">You can create and manage self-service databases in the user portal.</span></span> <span data-ttu-id="42b50-105">An Azure Stack user needs a subscription with an offer that includes the MySQL database service.</span><span class="sxs-lookup"><span data-stu-id="42b50-105">An Azure Stack user needs a subscription with an offer that includes the MySQL database service.</span></span>

## <a name="test-your-deployment-by-creating-a-mysql-database"></a><span data-ttu-id="42b50-106">Test your deployment by creating a MySQL database</span><span class="sxs-lookup"><span data-stu-id="42b50-106">Test your deployment by creating a MySQL database</span></span>

1. <span data-ttu-id="42b50-107">Sign in to the Azure Stack user portal.</span><span class="sxs-lookup"><span data-stu-id="42b50-107">Sign in to the Azure Stack user portal.</span></span>
2. <span data-ttu-id="42b50-108">Select **+ New** > **Data + Storage** > **MySQL Database** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="42b50-108">Select **+ New** > **Data + Storage** > **MySQL Database** > **Add**.</span></span>
3. <span data-ttu-id="42b50-109">Under **Create MySQL Database**, enter the Database Name, and configure the other settings as required for your environment.</span><span class="sxs-lookup"><span data-stu-id="42b50-109">Under **Create MySQL Database**, enter the Database Name, and configure the other settings as required for your environment.</span></span>

    ![Create a test MySQL database](./media/azure-stack-mysql-rp-deploy/mysql-create-db.png)

4. <span data-ttu-id="42b50-111">Under **Create Database**, select **SKU**.</span><span class="sxs-lookup"><span data-stu-id="42b50-111">Under **Create Database**, select **SKU**.</span></span> <span data-ttu-id="42b50-112">Under **Select a MySQL SKU**, pick the SKU for your database.</span><span class="sxs-lookup"><span data-stu-id="42b50-112">Under **Select a MySQL SKU**, pick the SKU for your database.</span></span>

    ![Select a MySQL SKU](./media/azure-stack-mysql-rp-deploy/mysql-select-sku.png)

    >[!Note]
    ><span data-ttu-id="42b50-114">As hosting servers are added to Azure Stack, they're assigned a SKU.</span><span class="sxs-lookup"><span data-stu-id="42b50-114">As hosting servers are added to Azure Stack, they're assigned a SKU.</span></span> <span data-ttu-id="42b50-115">Databases are created in the pool of hosting servers in a SKU.</span><span class="sxs-lookup"><span data-stu-id="42b50-115">Databases are created in the pool of hosting servers in a SKU.</span></span>

5. <span data-ttu-id="42b50-116">Under **Login**, select ***Configure required settings***.</span><span class="sxs-lookup"><span data-stu-id="42b50-116">Under **Login**, select ***Configure required settings***.</span></span>
6. <span data-ttu-id="42b50-117">Under **Select a Login**, you can choose an existing login or select **+ Create a new login** to set up a new login.</span><span class="sxs-lookup"><span data-stu-id="42b50-117">Under **Select a Login**, you can choose an existing login or select **+ Create a new login** to set up a new login.</span></span>  <span data-ttu-id="42b50-118">Enter a **Database login** name and **Password**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="42b50-118">Enter a **Database login** name and **Password**, and then select **OK**.</span></span>

    ![Create a new database login](./media/azure-stack-mysql-rp-deploy/create-new-login.png)

    >[!NOTE]
    ><span data-ttu-id="42b50-120">The length of the Database login name can't exceed 32 characters in MySQL 5.7.</span><span class="sxs-lookup"><span data-stu-id="42b50-120">The length of the Database login name can't exceed 32 characters in MySQL 5.7.</span></span> <span data-ttu-id="42b50-121">In earlier editions, it can't exceed 16 characters.</span><span class="sxs-lookup"><span data-stu-id="42b50-121">In earlier editions, it can't exceed 16 characters.</span></span>

7. <span data-ttu-id="42b50-122">Select **Create** to finish setting up the database.</span><span class="sxs-lookup"><span data-stu-id="42b50-122">Select **Create** to finish setting up the database.</span></span>

<span data-ttu-id="42b50-123">After the database is deployed, take note of the **Connection String** under **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="42b50-123">After the database is deployed, take note of the **Connection String** under **Essentials**.</span></span> <span data-ttu-id="42b50-124">You can use this string in any application that needs to access the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="42b50-124">You can use this string in any application that needs to access the MySQL database.</span></span>

![Get the connection string for the MySQL database](./media/azure-stack-mysql-rp-deploy/mysql-db-created.png)

## <a name="update-the-administrative-password"></a><span data-ttu-id="42b50-126">Update the administrative password</span><span class="sxs-lookup"><span data-stu-id="42b50-126">Update the administrative password</span></span>

<span data-ttu-id="42b50-127">You can modify the password by changing it on the MySQL server instance.</span><span class="sxs-lookup"><span data-stu-id="42b50-127">You can modify the password by changing it on the MySQL server instance.</span></span>

1. <span data-ttu-id="42b50-128">Select **ADMINISTRATIVE RESOURCES** > **MySQL Hosting Servers**.</span><span class="sxs-lookup"><span data-stu-id="42b50-128">Select **ADMINISTRATIVE RESOURCES** > **MySQL Hosting Servers**.</span></span> <span data-ttu-id="42b50-129">Select the hosting server.</span><span class="sxs-lookup"><span data-stu-id="42b50-129">Select the hosting server.</span></span>
2. <span data-ttu-id="42b50-130">Under **Settings**, select **Password**.</span><span class="sxs-lookup"><span data-stu-id="42b50-130">Under **Settings**, select **Password**.</span></span>
3. <span data-ttu-id="42b50-131">Under **Password**, enter the new password and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="42b50-131">Under **Password**, enter the new password and then select **Save**.</span></span>

![Update the admin password](./media/azure-stack-mysql-rp-deploy/mysql-update-password.png)

## <a name="next-steps"></a><span data-ttu-id="42b50-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="42b50-133">Next steps</span></span>

[<span data-ttu-id="42b50-134">Update the MySQL resource provider</span><span class="sxs-lookup"><span data-stu-id="42b50-134">Update the MySQL resource provider</span></span>](azure-stack-mysql-resource-provider-update.md)
