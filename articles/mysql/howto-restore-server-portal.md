---
title: How To Restore a Server in Azure Database for MySQL
description: This article describes how to restore a server in Azure Database for MySQL using the Azure portal.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 04/01/2018
ms.openlocfilehash: 6a34bbb5eefac117775c9876f3e4a25d3dade736
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870445"
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a><span data-ttu-id="be89d-103">How to backup and restore a server in Azure Database for MySQL using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="be89d-103">How to backup and restore a server in Azure Database for MySQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="be89d-104">Backup happens automatically</span><span class="sxs-lookup"><span data-stu-id="be89d-104">Backup happens automatically</span></span>
<span data-ttu-id="be89d-105">Azure Database for MySQL servers are backed up periodically to enable Restore features.</span><span class="sxs-lookup"><span data-stu-id="be89d-105">Azure Database for MySQL servers are backed up periodically to enable Restore features.</span></span> <span data-ttu-id="be89d-106">Using this feature you may restore the server and all its databases to an earlier point-in-time, on a new server.</span><span class="sxs-lookup"><span data-stu-id="be89d-106">Using this feature you may restore the server and all its databases to an earlier point-in-time, on a new server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be89d-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="be89d-107">Prerequisites</span></span>
<span data-ttu-id="be89d-108">To complete this how-to guide, you need:</span><span class="sxs-lookup"><span data-stu-id="be89d-108">To complete this how-to guide, you need:</span></span>
- <span data-ttu-id="be89d-109">An [Azure Database for MySQL server and database](quickstart-create-mysql-server-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="be89d-109">An [Azure Database for MySQL server and database](quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>

## <a name="set-backup-configuration"></a><span data-ttu-id="be89d-110">Set backup configuration</span><span class="sxs-lookup"><span data-stu-id="be89d-110">Set backup configuration</span></span>

<span data-ttu-id="be89d-111">You make the choice between configuring your server for either locally redundant backups or geographically redundant backups at server creation, in the **Pricing Tier** window.</span><span class="sxs-lookup"><span data-stu-id="be89d-111">You make the choice between configuring your server for either locally redundant backups or geographically redundant backups at server creation, in the **Pricing Tier** window.</span></span>

> [!NOTE]
> <span data-ttu-id="be89d-112">After a server is created, the kind of redundancy it has, geographically redundant vs locally redundant, can't be switched.</span><span class="sxs-lookup"><span data-stu-id="be89d-112">After a server is created, the kind of redundancy it has, geographically redundant vs locally redundant, can't be switched.</span></span>
>

<span data-ttu-id="be89d-113">While creating a server through the Azure portal, the **Pricing Tier** window is where you select either **Locally Redundant** or **Geographically Redundant** backups for your server.</span><span class="sxs-lookup"><span data-stu-id="be89d-113">While creating a server through the Azure portal, the **Pricing Tier** window is where you select either **Locally Redundant** or **Geographically Redundant** backups for your server.</span></span> <span data-ttu-id="be89d-114">This window is also where you select the **Backup Retention Period** - how long (in number of days) you want the server backups stored for.</span><span class="sxs-lookup"><span data-stu-id="be89d-114">This window is also where you select the **Backup Retention Period** - how long (in number of days) you want the server backups stored for.</span></span>

   ![Pricing Tier - Choose Backup Redundancy](./media/howto-restore-server-portal/pricing-tier.png)

<span data-ttu-id="be89d-116">For more information about setting these values during create, see the [Azure Database for MySQL server quickstart](quickstart-create-mysql-server-database-using-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="be89d-116">For more information about setting these values during create, see the [Azure Database for MySQL server quickstart](quickstart-create-mysql-server-database-using-azure-portal.md).</span></span>

<span data-ttu-id="be89d-117">The backup retention period can be changed on a server through the following steps:</span><span class="sxs-lookup"><span data-stu-id="be89d-117">The backup retention period can be changed on a server through the following steps:</span></span>
1. <span data-ttu-id="be89d-118">Sign into the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="be89d-118">Sign into the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="be89d-119">Select your Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="be89d-119">Select your Azure Database for MySQL server.</span></span> <span data-ttu-id="be89d-120">This action opens the **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="be89d-120">This action opens the **Overview** page.</span></span>
3. <span data-ttu-id="be89d-121">Select **Pricing Tier** from the menu, under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="be89d-121">Select **Pricing Tier** from the menu, under **SETTINGS**.</span></span> <span data-ttu-id="be89d-122">Using the slider you can change the **Backup Retention Period** to your preference between 7 and 35 days.</span><span class="sxs-lookup"><span data-stu-id="be89d-122">Using the slider you can change the **Backup Retention Period** to your preference between 7 and 35 days.</span></span>
<span data-ttu-id="be89d-123">In the screenshot below it has been increased to 34 days.</span><span class="sxs-lookup"><span data-stu-id="be89d-123">In the screenshot below it has been increased to 34 days.</span></span>
<span data-ttu-id="be89d-124">![Backup retention period increased](./media/howto-restore-server-portal/3-increase-backup-days.png)</span><span class="sxs-lookup"><span data-stu-id="be89d-124">![Backup retention period increased](./media/howto-restore-server-portal/3-increase-backup-days.png)</span></span>

4. <span data-ttu-id="be89d-125">Click **OK** to confirm the change.</span><span class="sxs-lookup"><span data-stu-id="be89d-125">Click **OK** to confirm the change.</span></span>

<span data-ttu-id="be89d-126">The backup retention period governs how far back in time a point-in-time restore can be retrieved, since it's based on backups available.</span><span class="sxs-lookup"><span data-stu-id="be89d-126">The backup retention period governs how far back in time a point-in-time restore can be retrieved, since it's based on backups available.</span></span> <span data-ttu-id="be89d-127">Point-in-time restore is described further in the following section.</span><span class="sxs-lookup"><span data-stu-id="be89d-127">Point-in-time restore is described further in the following section.</span></span> 

## <a name="point-in-time-restore"></a><span data-ttu-id="be89d-128">Point-in-time restore</span><span class="sxs-lookup"><span data-stu-id="be89d-128">Point-in-time restore</span></span>
<span data-ttu-id="be89d-129">Azure Database for MySQL allows you to restore the server back to a point-in-time and into to a new copy of the server.</span><span class="sxs-lookup"><span data-stu-id="be89d-129">Azure Database for MySQL allows you to restore the server back to a point-in-time and into to a new copy of the server.</span></span> <span data-ttu-id="be89d-130">You can use this new server to recover your data, or have your client applications point to this new server.</span><span class="sxs-lookup"><span data-stu-id="be89d-130">You can use this new server to recover your data, or have your client applications point to this new server.</span></span>

<span data-ttu-id="be89d-131">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span><span class="sxs-lookup"><span data-stu-id="be89d-131">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span> <span data-ttu-id="be89d-132">Point-in-time restore is at the server level, not at the database level.</span><span class="sxs-lookup"><span data-stu-id="be89d-132">Point-in-time restore is at the server level, not at the database level.</span></span>

<span data-ttu-id="be89d-133">The following steps restore the sample server to a point-in-time:</span><span class="sxs-lookup"><span data-stu-id="be89d-133">The following steps restore the sample server to a point-in-time:</span></span>
1. <span data-ttu-id="be89d-134">In the Azure portal, select your Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="be89d-134">In the Azure portal, select your Azure Database for MySQL server.</span></span> 

2. <span data-ttu-id="be89d-135">In the toolbar of the server's **Overview** page, select **Restore**.</span><span class="sxs-lookup"><span data-stu-id="be89d-135">In the toolbar of the server's **Overview** page, select **Restore**.</span></span>

   ![Azure Database for MySQL - Overview - Restore button](./media/howto-restore-server-portal/2-server.png)

3. <span data-ttu-id="be89d-137">Fill out the Restore form with the required information:</span><span class="sxs-lookup"><span data-stu-id="be89d-137">Fill out the Restore form with the required information:</span></span>

   ![<span data-ttu-id="be89d-138">Azure Database for MySQL - Restore information</span><span class="sxs-lookup"><span data-stu-id="be89d-138">Azure Database for MySQL - Restore information</span></span> ](./media/howto-restore-server-portal/3-restore.png)
  - <span data-ttu-id="be89d-139">**Restore point**: Select the point-in-time you want to restore to.</span><span class="sxs-lookup"><span data-stu-id="be89d-139">**Restore point**: Select the point-in-time you want to restore to.</span></span>
  - <span data-ttu-id="be89d-140">**Target server**: Provide a name for the new server.</span><span class="sxs-lookup"><span data-stu-id="be89d-140">**Target server**: Provide a name for the new server.</span></span>
  - <span data-ttu-id="be89d-141">**Location**: You cannot select the region.</span><span class="sxs-lookup"><span data-stu-id="be89d-141">**Location**: You cannot select the region.</span></span> <span data-ttu-id="be89d-142">By default it is same as the source server.</span><span class="sxs-lookup"><span data-stu-id="be89d-142">By default it is same as the source server.</span></span>
  - <span data-ttu-id="be89d-143">**Pricing tier**: You cannot change these parameters when doing a point-in-time restore.</span><span class="sxs-lookup"><span data-stu-id="be89d-143">**Pricing tier**: You cannot change these parameters when doing a point-in-time restore.</span></span> <span data-ttu-id="be89d-144">It is same as the source server.</span><span class="sxs-lookup"><span data-stu-id="be89d-144">It is same as the source server.</span></span> 

4. <span data-ttu-id="be89d-145">Click **OK** to restore the server to restore to a point-in-time.</span><span class="sxs-lookup"><span data-stu-id="be89d-145">Click **OK** to restore the server to restore to a point-in-time.</span></span> 

5. <span data-ttu-id="be89d-146">Once the restore finishes, locate the new server that is created to verify the data was restored as expected.</span><span class="sxs-lookup"><span data-stu-id="be89d-146">Once the restore finishes, locate the new server that is created to verify the data was restored as expected.</span></span>

>[!Note]
><span data-ttu-id="be89d-147">Note the new server created by point-in-time restore has the same server admin login name and password that was valid for the existing server at the point-in-time chose.</span><span class="sxs-lookup"><span data-stu-id="be89d-147">Note the new server created by point-in-time restore has the same server admin login name and password that was valid for the existing server at the point-in-time chose.</span></span> <span data-ttu-id="be89d-148">You can change the password from the new server's **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="be89d-148">You can change the password from the new server's **Overview** page.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="be89d-149">Geo restore</span><span class="sxs-lookup"><span data-stu-id="be89d-149">Geo restore</span></span>
<span data-ttu-id="be89d-150">If you configured your server for geographically redundant backups, a new server can be created from the backup of that existing server.</span><span class="sxs-lookup"><span data-stu-id="be89d-150">If you configured your server for geographically redundant backups, a new server can be created from the backup of that existing server.</span></span> <span data-ttu-id="be89d-151">This new server can be created in any region that Azure Database for MySQL is available.</span><span class="sxs-lookup"><span data-stu-id="be89d-151">This new server can be created in any region that Azure Database for MySQL is available.</span></span>  

1. <span data-ttu-id="be89d-152">Select the **Create a resource** button (+) in the upper-left corner of the portal.</span><span class="sxs-lookup"><span data-stu-id="be89d-152">Select the **Create a resource** button (+) in the upper-left corner of the portal.</span></span> <span data-ttu-id="be89d-153">Select **Databases** > **Azure Database for MySQL**.</span><span class="sxs-lookup"><span data-stu-id="be89d-153">Select **Databases** > **Azure Database for MySQL**.</span></span>

   ![The "Azure Database for MySQL" option](./media/howto-restore-server-portal/2_navigate-to-mysql.png)

2. <span data-ttu-id="be89d-155">In the form's **Select Source** dropdown, choose **Backup**.</span><span class="sxs-lookup"><span data-stu-id="be89d-155">In the form's **Select Source** dropdown, choose **Backup**.</span></span> <span data-ttu-id="be89d-156">This action loads a list of servers that have geo redundant backups enabled.</span><span class="sxs-lookup"><span data-stu-id="be89d-156">This action loads a list of servers that have geo redundant backups enabled.</span></span> <span data-ttu-id="be89d-157">Select one of these backups to be the source of your new server.</span><span class="sxs-lookup"><span data-stu-id="be89d-157">Select one of these backups to be the source of your new server.</span></span>
   <span data-ttu-id="be89d-158">![Select Source: Backup and list of geo redundant backups](./media/howto-restore-server-portal/2-georestore.png)</span><span class="sxs-lookup"><span data-stu-id="be89d-158">![Select Source: Backup and list of geo redundant backups](./media/howto-restore-server-portal/2-georestore.png)</span></span>

   > [!NOTE]
   > <span data-ttu-id="be89d-159">When a server is first created it may not be immediately available for geo restore.</span><span class="sxs-lookup"><span data-stu-id="be89d-159">When a server is first created it may not be immediately available for geo restore.</span></span> <span data-ttu-id="be89d-160">It may take a few hours for the necessary metadata to be populated.</span><span class="sxs-lookup"><span data-stu-id="be89d-160">It may take a few hours for the necessary metadata to be populated.</span></span>
   >

3. <span data-ttu-id="be89d-161">Fill out the rest of the form with your preferences.</span><span class="sxs-lookup"><span data-stu-id="be89d-161">Fill out the rest of the form with your preferences.</span></span> <span data-ttu-id="be89d-162">You can select any **Location**.</span><span class="sxs-lookup"><span data-stu-id="be89d-162">You can select any **Location**.</span></span> <span data-ttu-id="be89d-163">After selecting the location, you can select **Pricing Tier**.</span><span class="sxs-lookup"><span data-stu-id="be89d-163">After selecting the location, you can select **Pricing Tier**.</span></span> <span data-ttu-id="be89d-164">By default the parameters for the existing server you are restoring from are displayed.</span><span class="sxs-lookup"><span data-stu-id="be89d-164">By default the parameters for the existing server you are restoring from are displayed.</span></span> <span data-ttu-id="be89d-165">You can click **OK** without making any changes to inherit those settings.</span><span class="sxs-lookup"><span data-stu-id="be89d-165">You can click **OK** without making any changes to inherit those settings.</span></span> <span data-ttu-id="be89d-166">Or you can change **Compute Generation** (if available in the region you have chosen), number of **vCores**, **Backup Retention Period**, and **Backup Redundancy Option**.</span><span class="sxs-lookup"><span data-stu-id="be89d-166">Or you can change **Compute Generation** (if available in the region you have chosen), number of **vCores**, **Backup Retention Period**, and **Backup Redundancy Option**.</span></span> <span data-ttu-id="be89d-167">Changing **Pricing Tier** (Basic, General Purpose, or Memory Optimized) or **Storage** size during restore is not supported.</span><span class="sxs-lookup"><span data-stu-id="be89d-167">Changing **Pricing Tier** (Basic, General Purpose, or Memory Optimized) or **Storage** size during restore is not supported.</span></span>

>[!Note]
><span data-ttu-id="be89d-168">The new server created by geo restore has the same server admin login name and password that was valid for the existing server at the time the restore was initiated.</span><span class="sxs-lookup"><span data-stu-id="be89d-168">The new server created by geo restore has the same server admin login name and password that was valid for the existing server at the time the restore was initiated.</span></span> <span data-ttu-id="be89d-169">The password can be changed from the new server's **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="be89d-169">The password can be changed from the new server's **Overview** page.</span></span>


## <a name="next-steps"></a><span data-ttu-id="be89d-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="be89d-170">Next steps</span></span>
- <span data-ttu-id="be89d-171">Learn more about the service's [backups](concepts-backup.md).</span><span class="sxs-lookup"><span data-stu-id="be89d-171">Learn more about the service's [backups](concepts-backup.md).</span></span>
- <span data-ttu-id="be89d-172">Learn more about [business continuity](concepts-business-continuity.md) options.</span><span class="sxs-lookup"><span data-stu-id="be89d-172">Learn more about [business continuity](concepts-business-continuity.md) options.</span></span>
