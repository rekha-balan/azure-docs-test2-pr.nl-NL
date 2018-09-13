---
title: MySQL Hosting Servers on Azure Stack | Microsoft Docs
description: How to add MySQL instances for provisioning through the MySQL Adapter Resource Provider
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
ms.date: 09/05/2018
ms.author: jeffgilb
ms.reviewer: jeffgo
ms.openlocfilehash: b498dadd862fec3d7b8aab38716dfd36484139c2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969119"
---
# <a name="add-hosting-servers-for-the-mysql-resource-provider"></a><span data-ttu-id="d5709-103">Add hosting servers for the MySQL resource provider</span><span class="sxs-lookup"><span data-stu-id="d5709-103">Add hosting servers for the MySQL resource provider</span></span>

<span data-ttu-id="d5709-104">You can host a MySQL instance on a virtual machine (VM) in [Azure Stack](azure-stack-poc.md), or on a VM outside your Azure Stack environment, as long as the MySQL resource provider can connect to the instance.</span><span class="sxs-lookup"><span data-stu-id="d5709-104">You can host a MySQL instance on a virtual machine (VM) in [Azure Stack](azure-stack-poc.md), or on a VM outside your Azure Stack environment, as long as the MySQL resource provider can connect to the instance.</span></span>

<span data-ttu-id="d5709-105">MySQL versions 5.6, 5.7 and 8.0 may be used for your hosting servers.</span><span class="sxs-lookup"><span data-stu-id="d5709-105">MySQL versions 5.6, 5.7 and 8.0 may be used for your hosting servers.</span></span> <span data-ttu-id="d5709-106">The MySQL RP does not support caching_sha2_password authentication; that will be added in the next release.</span><span class="sxs-lookup"><span data-stu-id="d5709-106">The MySQL RP does not support caching_sha2_password authentication; that will be added in the next release.</span></span> <span data-ttu-id="d5709-107">MySQL 8.0 servers must be configured to use mysql_native_password.</span><span class="sxs-lookup"><span data-stu-id="d5709-107">MySQL 8.0 servers must be configured to use mysql_native_password.</span></span> <span data-ttu-id="d5709-108">MariaDB is also supported.</span><span class="sxs-lookup"><span data-stu-id="d5709-108">MariaDB is also supported.</span></span>

## <a name="connect-to-a-mysql-hosting-server"></a><span data-ttu-id="d5709-109">Connect to a MySQL hosting server</span><span class="sxs-lookup"><span data-stu-id="d5709-109">Connect to a MySQL hosting server</span></span>

<span data-ttu-id="d5709-110">Make sure you have the credentials for an account with system admin privileges.</span><span class="sxs-lookup"><span data-stu-id="d5709-110">Make sure you have the credentials for an account with system admin privileges.</span></span> <span data-ttu-id="d5709-111">To add a hosting server, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="d5709-111">To add a hosting server, follow these steps:</span></span>

1. <span data-ttu-id="d5709-112">Sign in to the Azure Stack operator portal as a service admin.</span><span class="sxs-lookup"><span data-stu-id="d5709-112">Sign in to the Azure Stack operator portal as a service admin.</span></span>
2. <span data-ttu-id="d5709-113">Select **All services**.</span><span class="sxs-lookup"><span data-stu-id="d5709-113">Select **All services**.</span></span>
3. <span data-ttu-id="d5709-114">Under the  **ADMINISTRATIVE RESOURCES** category select **MySQL Hosting Servers** > **+Add**.</span><span class="sxs-lookup"><span data-stu-id="d5709-114">Under the  **ADMINISTRATIVE RESOURCES** category select **MySQL Hosting Servers** > **+Add**.</span></span> <span data-ttu-id="d5709-115">This opens the **Add a MySQL Hosting Server** dialog, shown in the following screen capture.</span><span class="sxs-lookup"><span data-stu-id="d5709-115">This opens the **Add a MySQL Hosting Server** dialog, shown in the following screen capture.</span></span>

   ![Configure a hosting server](./media/azure-stack-mysql-rp-deploy/mysql-add-hosting-server-2.png)

4. <span data-ttu-id="d5709-117">Provide the connection details of your MySQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="d5709-117">Provide the connection details of your MySQL Server instance.</span></span>

   * <span data-ttu-id="d5709-118">For **MySQL Hosting Server Name**, provide the fully qualified domain name (FQDN) or a valid IPv4 address.</span><span class="sxs-lookup"><span data-stu-id="d5709-118">For **MySQL Hosting Server Name**, provide the fully qualified domain name (FQDN) or a valid IPv4 address.</span></span> <span data-ttu-id="d5709-119">Don't use the short VM name.</span><span class="sxs-lookup"><span data-stu-id="d5709-119">Don't use the short VM name.</span></span>
   * <span data-ttu-id="d5709-120">A default MySQL instance isn't provided, so you have to specify the **Size of Hosting Server in GB**.</span><span class="sxs-lookup"><span data-stu-id="d5709-120">A default MySQL instance isn't provided, so you have to specify the **Size of Hosting Server in GB**.</span></span> <span data-ttu-id="d5709-121">Enter a size that's close to the capacity of the database server.</span><span class="sxs-lookup"><span data-stu-id="d5709-121">Enter a size that's close to the capacity of the database server.</span></span>
   * <span data-ttu-id="d5709-122">Keep the default setting for **Subscription**.</span><span class="sxs-lookup"><span data-stu-id="d5709-122">Keep the default setting for **Subscription**.</span></span>
   * <span data-ttu-id="d5709-123">For **Resource group**, create a new one, or use an existing group.</span><span class="sxs-lookup"><span data-stu-id="d5709-123">For **Resource group**, create a new one, or use an existing group.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d5709-124">If the MySQL instance can be accessed by the tenant and the admin Azure Resource Manager, you can put it under the control of the resource provider.</span><span class="sxs-lookup"><span data-stu-id="d5709-124">If the MySQL instance can be accessed by the tenant and the admin Azure Resource Manager, you can put it under the control of the resource provider.</span></span> <span data-ttu-id="d5709-125">But, the MySQL instance **must** be allocated exclusively to the resource provider.</span><span class="sxs-lookup"><span data-stu-id="d5709-125">But, the MySQL instance **must** be allocated exclusively to the resource provider.</span></span>

5. <span data-ttu-id="d5709-126">Select **SKUs** to open the **Create SKU** dialog.</span><span class="sxs-lookup"><span data-stu-id="d5709-126">Select **SKUs** to open the **Create SKU** dialog.</span></span>

   ![Create a MySQL SKU](./media/azure-stack-mysql-rp-deploy/mysql-new-sku.png)

   <span data-ttu-id="d5709-128">The SKU **Name** should reflect the properties of the SKU so users can deploy their databases to the appropriate SKU.</span><span class="sxs-lookup"><span data-stu-id="d5709-128">The SKU **Name** should reflect the properties of the SKU so users can deploy their databases to the appropriate SKU.</span></span>

6. <span data-ttu-id="d5709-129">Select **OK** to create the SKU.</span><span class="sxs-lookup"><span data-stu-id="d5709-129">Select **OK** to create the SKU.</span></span>
> [!NOTE]
> <span data-ttu-id="d5709-130">SKUs can take up to an hour to be visible in the portal.</span><span class="sxs-lookup"><span data-stu-id="d5709-130">SKUs can take up to an hour to be visible in the portal.</span></span> <span data-ttu-id="d5709-131">You can't create a database until the SKU is deployed and running.</span><span class="sxs-lookup"><span data-stu-id="d5709-131">You can't create a database until the SKU is deployed and running.</span></span>

7. <span data-ttu-id="d5709-132">Under **Add a MySQL Hosting Server**, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d5709-132">Under **Add a MySQL Hosting Server**, select **Create**.</span></span>

<span data-ttu-id="d5709-133">As you add servers, assign them to a new or existing SKU to differentiate service offerings.</span><span class="sxs-lookup"><span data-stu-id="d5709-133">As you add servers, assign them to a new or existing SKU to differentiate service offerings.</span></span> <span data-ttu-id="d5709-134">For example, you can have a MySQL enterprise instance that provides increased database and automatic backups.</span><span class="sxs-lookup"><span data-stu-id="d5709-134">For example, you can have a MySQL enterprise instance that provides increased database and automatic backups.</span></span> <span data-ttu-id="d5709-135">You can reserve this high-performance server for different departments in your organization.</span><span class="sxs-lookup"><span data-stu-id="d5709-135">You can reserve this high-performance server for different departments in your organization.</span></span>

## <a name="security-considerations-for-mysql"></a><span data-ttu-id="d5709-136">Security considerations for MySQL</span><span class="sxs-lookup"><span data-stu-id="d5709-136">Security considerations for MySQL</span></span>

<span data-ttu-id="d5709-137">The following information applies to the RP and MySQL hosting servers:</span><span class="sxs-lookup"><span data-stu-id="d5709-137">The following information applies to the RP and MySQL hosting servers:</span></span>

* <span data-ttu-id="d5709-138">Ensure that all hosting servers are configured for communication using TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="d5709-138">Ensure that all hosting servers are configured for communication using TLS 1.2.</span></span> <span data-ttu-id="d5709-139">See [Configuring MySQL to Use Encrypted Connections](https://dev.mysql.com/doc/refman/5.7/en/using-encrypted-connections.html).</span><span class="sxs-lookup"><span data-stu-id="d5709-139">See [Configuring MySQL to Use Encrypted Connections](https://dev.mysql.com/doc/refman/5.7/en/using-encrypted-connections.html).</span></span>
* <span data-ttu-id="d5709-140">Employ [Transparent Data Encryption](https://dev.mysql.com/doc/mysql-secure-deployment-guide/5.7/en/secure-deployment-data-encryption.html).</span><span class="sxs-lookup"><span data-stu-id="d5709-140">Employ [Transparent Data Encryption](https://dev.mysql.com/doc/mysql-secure-deployment-guide/5.7/en/secure-deployment-data-encryption.html).</span></span>
* <span data-ttu-id="d5709-141">The MySQL RP does not support caching_sha2_password authentication.</span><span class="sxs-lookup"><span data-stu-id="d5709-141">The MySQL RP does not support caching_sha2_password authentication.</span></span>

## <a name="increase-backend-database-capacity"></a><span data-ttu-id="d5709-142">Increase backend database capacity</span><span class="sxs-lookup"><span data-stu-id="d5709-142">Increase backend database capacity</span></span>

<span data-ttu-id="d5709-143">You can increase backend database capacity by deploying more MySQL servers in the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="d5709-143">You can increase backend database capacity by deploying more MySQL servers in the Azure Stack portal.</span></span> <span data-ttu-id="d5709-144">Add these servers to a new or existing SKU.</span><span class="sxs-lookup"><span data-stu-id="d5709-144">Add these servers to a new or existing SKU.</span></span> <span data-ttu-id="d5709-145">If you add a server to an existing SKU, make sure that the server characteristics are the same as the other servers in the SKU.</span><span class="sxs-lookup"><span data-stu-id="d5709-145">If you add a server to an existing SKU, make sure that the server characteristics are the same as the other servers in the SKU.</span></span>

## <a name="make-mysql-database-servers-available-to-your-users"></a><span data-ttu-id="d5709-146">Make MySQL database servers available to your users</span><span class="sxs-lookup"><span data-stu-id="d5709-146">Make MySQL database servers available to your users</span></span>

<span data-ttu-id="d5709-147">Create plans and offers to make MySQL database servers available to users.</span><span class="sxs-lookup"><span data-stu-id="d5709-147">Create plans and offers to make MySQL database servers available to users.</span></span> <span data-ttu-id="d5709-148">Add the Microsoft.MySqlAdapter service to the plan and create a new quota.</span><span class="sxs-lookup"><span data-stu-id="d5709-148">Add the Microsoft.MySqlAdapter service to the plan and create a new quota.</span></span> <span data-ttu-id="d5709-149">MySQL does not allow limiting the size of databases.</span><span class="sxs-lookup"><span data-stu-id="d5709-149">MySQL does not allow limiting the size of databases.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5709-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="d5709-150">Next steps</span></span>

[<span data-ttu-id="d5709-151">Create a MySQL database</span><span class="sxs-lookup"><span data-stu-id="d5709-151">Create a MySQL database</span></span>](azure-stack-mysql-resource-provider-databases.md)