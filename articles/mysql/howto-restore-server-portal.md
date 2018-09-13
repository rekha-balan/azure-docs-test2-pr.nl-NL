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
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a>How to backup and restore a server in Azure Database for MySQL using the Azure portal

## <a name="backup-happens-automatically"></a>Backup happens automatically
Azure Database for MySQL servers are backed up periodically to enable Restore features. Using this feature you may restore the server and all its databases to an earlier point-in-time, on a new server.

## <a name="prerequisites"></a>Prerequisites
To complete this how-to guide, you need:
- An [Azure Database for MySQL server and database](quickstart-create-mysql-server-database-using-azure-portal.md)

## <a name="set-backup-configuration"></a>Set backup configuration

You make the choice between configuring your server for either locally redundant backups or geographically redundant backups at server creation, in the **Pricing Tier** window.

> [!NOTE]
> After a server is created, the kind of redundancy it has, geographically redundant vs locally redundant, can't be switched.
>

While creating a server through the Azure portal, the **Pricing Tier** window is where you select either **Locally Redundant** or **Geographically Redundant** backups for your server. This window is also where you select the **Backup Retention Period** - how long (in number of days) you want the server backups stored for.

   ![Pricing Tier - Choose Backup Redundancy](./media/howto-restore-server-portal/pricing-tier.png)

For more information about setting these values during create, see the [Azure Database for MySQL server quickstart](quickstart-create-mysql-server-database-using-azure-portal.md).

The backup retention period can be changed on a server through the following steps:
1. Sign into the [Azure portal](https://portal.azure.com/).
2. Select your Azure Database for MySQL server. This action opens the **Overview** page.
3. Select **Pricing Tier** from the menu, under **SETTINGS**. Using the slider you can change the **Backup Retention Period** to your preference between 7 and 35 days.
In the screenshot below it has been increased to 34 days.
![Backup retention period increased](./media/howto-restore-server-portal/3-increase-backup-days.png)

4. Click **OK** to confirm the change.

The backup retention period governs how far back in time a point-in-time restore can be retrieved, since it's based on backups available. Point-in-time restore is described further in the following section. 

## <a name="point-in-time-restore"></a>Point-in-time restore
Azure Database for MySQL allows you to restore the server back to a point-in-time and into to a new copy of the server. You can use this new server to recover your data, or have your client applications point to this new server.

For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server. Point-in-time restore is at the server level, not at the database level.

The following steps restore the sample server to a point-in-time:
1. In the Azure portal, select your Azure Database for MySQL server. 

2. In the toolbar of the server's **Overview** page, select **Restore**.

   ![Azure Database for MySQL - Overview - Restore button](./media/howto-restore-server-portal/2-server.png)

3. Fill out the Restore form with the required information:

   ![Azure Database for MySQL - Restore information ](./media/howto-restore-server-portal/3-restore.png)
  - **Restore point**: Select the point-in-time you want to restore to.
  - **Target server**: Provide a name for the new server.
  - **Location**: You cannot select the region. By default it is same as the source server.
  - **Pricing tier**: You cannot change these parameters when doing a point-in-time restore. It is same as the source server. 

4. Click **OK** to restore the server to restore to a point-in-time. 

5. Once the restore finishes, locate the new server that is created to verify the data was restored as expected.

>[!Note]
>Note the new server created by point-in-time restore has the same server admin login name and password that was valid for the existing server at the point-in-time chose. You can change the password from the new server's **Overview** page.

## <a name="geo-restore"></a>Geo restore
If you configured your server for geographically redundant backups, a new server can be created from the backup of that existing server. This new server can be created in any region that Azure Database for MySQL is available.  

1. Select the **Create a resource** button (+) in the upper-left corner of the portal. Select **Databases** > **Azure Database for MySQL**.

   ![The "Azure Database for MySQL" option](./media/howto-restore-server-portal/2_navigate-to-mysql.png)

2. In the form's **Select Source** dropdown, choose **Backup**. This action loads a list of servers that have geo redundant backups enabled. Select one of these backups to be the source of your new server.
   ![Select Source: Backup and list of geo redundant backups](./media/howto-restore-server-portal/2-georestore.png)

   > [!NOTE]
   > When a server is first created it may not be immediately available for geo restore. It may take a few hours for the necessary metadata to be populated.
   >

3. Fill out the rest of the form with your preferences. You can select any **Location**. After selecting the location, you can select **Pricing Tier**. By default the parameters for the existing server you are restoring from are displayed. You can click **OK** without making any changes to inherit those settings. Or you can change **Compute Generation** (if available in the region you have chosen), number of **vCores**, **Backup Retention Period**, and **Backup Redundancy Option**. Changing **Pricing Tier** (Basic, General Purpose, or Memory Optimized) or **Storage** size during restore is not supported.

>[!Note]
>The new server created by geo restore has the same server admin login name and password that was valid for the existing server at the time the restore was initiated. The password can be changed from the new server's **Overview** page.


## <a name="next-steps"></a>Next steps
- Learn more about the service's [backups](concepts-backup.md).
- Learn more about [business continuity](concepts-business-continuity.md) options.