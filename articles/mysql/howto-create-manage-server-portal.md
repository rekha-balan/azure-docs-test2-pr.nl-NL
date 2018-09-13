---
title: Create and manage Azure Database for MySQL server using Azure portal
description: This article describes how you can quickly create a new Azure Database for MySQL server and manage the server using the Azure Portal.
services: mysql
author: ajlam
ms.author: andrela
editor: jasonwhowell
manager: kfile
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: 065eb708a1d80b0eac618bd9039a859db6ef1340
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855657"
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="1132b-103">Create and manage Azure Database for MySQL server using Azure portal</span><span class="sxs-lookup"><span data-stu-id="1132b-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="1132b-104">This topic describes how you can quickly create a new Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="1132b-104">This topic describes how you can quickly create a new Azure Database for MySQL server.</span></span> <span data-ttu-id="1132b-105">It also includes information about how to manage the server by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1132b-105">It also includes information about how to manage the server by using the Azure portal.</span></span> <span data-ttu-id="1132b-106">Server management includes viewing server details and databases, resetting the password, scaling resources, and deleting the server.</span><span class="sxs-lookup"><span data-stu-id="1132b-106">Server management includes viewing server details and databases, resetting the password, scaling resources, and deleting the server.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="1132b-107">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1132b-107">Log in to the Azure portal</span></span>
<span data-ttu-id="1132b-108">Log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1132b-108">Log in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="1132b-109">Create an Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="1132b-109">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="1132b-110">Follow these steps to create an Azure Database for MySQL server named “mydemoserver.”</span><span class="sxs-lookup"><span data-stu-id="1132b-110">Follow these steps to create an Azure Database for MySQL server named “mydemoserver.”</span></span>

1. <span data-ttu-id="1132b-111">Click the **Create a resource** button located in the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1132b-111">Click the **Create a resource** button located in the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="1132b-112">On the New page, select **Databases**, and then on Databases page, select **Azure Database for MySQL**.</span><span class="sxs-lookup"><span data-stu-id="1132b-112">On the New page, select **Databases**, and then on Databases page, select **Azure Database for MySQL**.</span></span>

    > <span data-ttu-id="1132b-113">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-pricing-tiers.md) resources.</span><span class="sxs-lookup"><span data-stu-id="1132b-113">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-pricing-tiers.md) resources.</span></span> <span data-ttu-id="1132b-114">The database is created within an Azure resource group and in an Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="1132b-114">The database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

   ![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

3. <span data-ttu-id="1132b-116">Fill out the Azure Database for MySQL form by using the following information:</span><span class="sxs-lookup"><span data-stu-id="1132b-116">Fill out the Azure Database for MySQL form by using the following information:</span></span>

    | <span data-ttu-id="1132b-117">**Form Field**</span><span class="sxs-lookup"><span data-stu-id="1132b-117">**Form Field**</span></span> | <span data-ttu-id="1132b-118">**Field Description**</span><span class="sxs-lookup"><span data-stu-id="1132b-118">**Field Description**</span></span> |
    |----------------|-----------------------|
    | <span data-ttu-id="1132b-119">*Server name*</span><span class="sxs-lookup"><span data-stu-id="1132b-119">*Server name*</span></span> | <span data-ttu-id="1132b-120">mydemoserver (server name is globally unique)</span><span class="sxs-lookup"><span data-stu-id="1132b-120">mydemoserver (server name is globally unique)</span></span> |
    | <span data-ttu-id="1132b-121">*Subscription*</span><span class="sxs-lookup"><span data-stu-id="1132b-121">*Subscription*</span></span> | <span data-ttu-id="1132b-122">mysubscription (select from the drop-down menu)</span><span class="sxs-lookup"><span data-stu-id="1132b-122">mysubscription (select from the drop-down menu)</span></span> |
    | <span data-ttu-id="1132b-123">*Resource group*</span><span class="sxs-lookup"><span data-stu-id="1132b-123">*Resource group*</span></span> | <span data-ttu-id="1132b-124">myresourcegroup (create a new resource group or use an existing one)</span><span class="sxs-lookup"><span data-stu-id="1132b-124">myresourcegroup (create a new resource group or use an existing one)</span></span> |
    | <span data-ttu-id="1132b-125">*Select source*</span><span class="sxs-lookup"><span data-stu-id="1132b-125">*Select source*</span></span> | <span data-ttu-id="1132b-126">Blank (create a blank MySQL server)</span><span class="sxs-lookup"><span data-stu-id="1132b-126">Blank (create a blank MySQL server)</span></span> |
    | <span data-ttu-id="1132b-127">*Server admin login*</span><span class="sxs-lookup"><span data-stu-id="1132b-127">*Server admin login*</span></span> | <span data-ttu-id="1132b-128">myadmin (setup admin account name)</span><span class="sxs-lookup"><span data-stu-id="1132b-128">myadmin (setup admin account name)</span></span> |
    | <span data-ttu-id="1132b-129">*Password*</span><span class="sxs-lookup"><span data-stu-id="1132b-129">*Password*</span></span> | <span data-ttu-id="1132b-130">set admin account password</span><span class="sxs-lookup"><span data-stu-id="1132b-130">set admin account password</span></span> |
    | <span data-ttu-id="1132b-131">*Confirm password*</span><span class="sxs-lookup"><span data-stu-id="1132b-131">*Confirm password*</span></span> | <span data-ttu-id="1132b-132">confirm admin account password</span><span class="sxs-lookup"><span data-stu-id="1132b-132">confirm admin account password</span></span> |
    | <span data-ttu-id="1132b-133">*Location*</span><span class="sxs-lookup"><span data-stu-id="1132b-133">*Location*</span></span> | <span data-ttu-id="1132b-134">Southeast Asia (select between North Europe and West US)</span><span class="sxs-lookup"><span data-stu-id="1132b-134">Southeast Asia (select between North Europe and West US)</span></span> |
    | <span data-ttu-id="1132b-135">*Version*</span><span class="sxs-lookup"><span data-stu-id="1132b-135">*Version*</span></span> | <span data-ttu-id="1132b-136">5.7 (choose Azure Database for MySQL server version)</span><span class="sxs-lookup"><span data-stu-id="1132b-136">5.7 (choose Azure Database for MySQL server version)</span></span> |

4. <span data-ttu-id="1132b-137">Click **Pricing tier** to specify the service tier and performance level for your new server.</span><span class="sxs-lookup"><span data-stu-id="1132b-137">Click **Pricing tier** to specify the service tier and performance level for your new server.</span></span> <span data-ttu-id="1132b-138">Select the **General Purpose** tab. *Gen 4*, *2 vCores*, *5 GB*, and *7 days* are the default values for **Compute Generation**, **vCore**, **Storage**, and **Backup Retention Period**.</span><span class="sxs-lookup"><span data-stu-id="1132b-138">Select the **General Purpose** tab. *Gen 4*, *2 vCores*, *5 GB*, and *7 days* are the default values for **Compute Generation**, **vCore**, **Storage**, and **Backup Retention Period**.</span></span> <span data-ttu-id="1132b-139">You can leave those sliders as is.</span><span class="sxs-lookup"><span data-stu-id="1132b-139">You can leave those sliders as is.</span></span> <span data-ttu-id="1132b-140">To enable your server backups in geo-redundant storage select **Geographically Redundant** from the **Backup Redundancy Options**.</span><span class="sxs-lookup"><span data-stu-id="1132b-140">To enable your server backups in geo-redundant storage select **Geographically Redundant** from the **Backup Redundancy Options**.</span></span>

   ![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)

5. <span data-ttu-id="1132b-142">Click **Create** to provision the server.</span><span class="sxs-lookup"><span data-stu-id="1132b-142">Click **Create** to provision the server.</span></span> <span data-ttu-id="1132b-143">Provisioning takes a few minutes.</span><span class="sxs-lookup"><span data-stu-id="1132b-143">Provisioning takes a few minutes.</span></span>

    > <span data-ttu-id="1132b-144">Select the **Pin to dashboard** option to allow easy tracking of your deployments.</span><span class="sxs-lookup"><span data-stu-id="1132b-144">Select the **Pin to dashboard** option to allow easy tracking of your deployments.</span></span>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="1132b-145">Update an Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="1132b-145">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="1132b-146">After the new server has been provisioned, the user has several options for configuring the existing server, including resetting the administrator password and scaling the server up or down by changing vCore or storage.</span><span class="sxs-lookup"><span data-stu-id="1132b-146">After the new server has been provisioned, the user has several options for configuring the existing server, including resetting the administrator password and scaling the server up or down by changing vCore or storage.</span></span>

### <a name="change-the-administrator-user-password"></a><span data-ttu-id="1132b-147">Change the administrator user password</span><span class="sxs-lookup"><span data-stu-id="1132b-147">Change the administrator user password</span></span>
1. <span data-ttu-id="1132b-148">From the server **Overview**, click **Reset password** to show the password reset window.</span><span class="sxs-lookup"><span data-stu-id="1132b-148">From the server **Overview**, click **Reset password** to show the password reset window.</span></span>

   ![overview](./media/howto-create-manage-server-portal/overview.png)

2. <span data-ttu-id="1132b-150">Enter a new password and confirm the password in the window as shown:</span><span class="sxs-lookup"><span data-stu-id="1132b-150">Enter a new password and confirm the password in the window as shown:</span></span>

   ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)

3. <span data-ttu-id="1132b-152">Click **OK** to save the new password.</span><span class="sxs-lookup"><span data-stu-id="1132b-152">Click **OK** to save the new password.</span></span>

### <a name="scale-vcores-updown"></a><span data-ttu-id="1132b-153">Scale vCores up/down</span><span class="sxs-lookup"><span data-stu-id="1132b-153">Scale vCores up/down</span></span>

1. <span data-ttu-id="1132b-154">Click on **Pricing tier**, located under **Settings**.</span><span class="sxs-lookup"><span data-stu-id="1132b-154">Click on **Pricing tier**, located under **Settings**.</span></span>

2. <span data-ttu-id="1132b-155">Change the **vCore** setting by moving the slider to your desired value.</span><span class="sxs-lookup"><span data-stu-id="1132b-155">Change the **vCore** setting by moving the slider to your desired value.</span></span>

    ![scale-compute](./media/howto-create-manage-server-portal/scale-compute.png)

3. <span data-ttu-id="1132b-157">Click **OK** to save changes.</span><span class="sxs-lookup"><span data-stu-id="1132b-157">Click **OK** to save changes.</span></span>

### <a name="scale-storage-up"></a><span data-ttu-id="1132b-158">Scale Storage up</span><span class="sxs-lookup"><span data-stu-id="1132b-158">Scale Storage up</span></span>

1. <span data-ttu-id="1132b-159">Click on **Pricing tier**, located under **Settings**.</span><span class="sxs-lookup"><span data-stu-id="1132b-159">Click on **Pricing tier**, located under **Settings**.</span></span>

2. <span data-ttu-id="1132b-160">Change the **Storage** setting by moving the slider to your desired value.</span><span class="sxs-lookup"><span data-stu-id="1132b-160">Change the **Storage** setting by moving the slider to your desired value.</span></span>

    ![scale-storage](./media/howto-create-manage-server-portal/scale-storage.png)

3. <span data-ttu-id="1132b-162">Click **OK** to save changes.</span><span class="sxs-lookup"><span data-stu-id="1132b-162">Click **OK** to save changes.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="1132b-163">Delete an Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="1132b-163">Delete an Azure Database for MySQL server</span></span>

1. <span data-ttu-id="1132b-164">From the server **Overview**, click the **Delete** button to open the delete confirmation prompt.</span><span class="sxs-lookup"><span data-stu-id="1132b-164">From the server **Overview**, click the **Delete** button to open the delete confirmation prompt.</span></span>

    ![delete](./media/howto-create-manage-server-portal/delete.png)

2. <span data-ttu-id="1132b-166">Type the name of the server into the input box for double confirmation.</span><span class="sxs-lookup"><span data-stu-id="1132b-166">Type the name of the server into the input box for double confirmation.</span></span>

    ![confirm-delete](./media/howto-create-manage-server-portal/confirm.png)

3. <span data-ttu-id="1132b-168">Click the **Delete** button to confirm deleting the server.</span><span class="sxs-lookup"><span data-stu-id="1132b-168">Click the **Delete** button to confirm deleting the server.</span></span> <span data-ttu-id="1132b-169">Wait for the “Successfully deleted MySQL server" pop up to appear in the notification bar.</span><span class="sxs-lookup"><span data-stu-id="1132b-169">Wait for the “Successfully deleted MySQL server" pop up to appear in the notification bar.</span></span>

## <a name="list-the-azure-database-for-mysql-databases"></a><span data-ttu-id="1132b-170">List the Azure Database for MySQL databases</span><span class="sxs-lookup"><span data-stu-id="1132b-170">List the Azure Database for MySQL databases</span></span>
<span data-ttu-id="1132b-171">From the server **Overview**, scroll down until you see the database tile at the bottom.</span><span class="sxs-lookup"><span data-stu-id="1132b-171">From the server **Overview**, scroll down until you see the database tile at the bottom.</span></span> <span data-ttu-id="1132b-172">All databases in the server are listed in the table.</span><span class="sxs-lookup"><span data-stu-id="1132b-172">All databases in the server are listed in the table.</span></span>

   ![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="1132b-174">Show details of an Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="1132b-174">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="1132b-175">Click on **Properties**, located under **Settings** to view detailed information about the server.</span><span class="sxs-lookup"><span data-stu-id="1132b-175">Click on **Properties**, located under **Settings** to view detailed information about the server.</span></span>

![properties](./media/howto-create-manage-server-portal/properties.png)

## <a name="next-steps"></a><span data-ttu-id="1132b-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="1132b-177">Next steps</span></span>

[<span data-ttu-id="1132b-178">Quickstart: Create Azure Database for MySQL server using Azure portal</span><span class="sxs-lookup"><span data-stu-id="1132b-178">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)