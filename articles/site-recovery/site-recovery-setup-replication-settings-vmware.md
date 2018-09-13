---
title: Set up replication settings for Azure Site Recovery| Microsoft Docs
description: Describes how to deploy Site Recovery to orchestrate replication, failover, and recovery of Hyper-V VMs in VMM clouds to Azure.
services: site-recovery
documentationcenter: ''
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/19/2017
ms.author: sutalasi
ms.openlocfilehash: a265d5c51f3eb8f12d78e082464b5a2d7971fb2f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563344"
---
# <a name="manage-replication-policy-for-vmware-to-azure"></a>Manage replication policy for VMware to Azure


## <a name="create-a-replication-policy"></a>Create a replication policy

1. Select **Manage** > **Site Recovery Infrastructure**.
2. Select **Replication policies** under **For VMware and Physical machines**.
3. Select **+Replication policy**.

    ![Create replication policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Createpolicy.png)

4. Enter the policy name.

5. In **RPO threshold**, specify the RPO limit. Alerts will be generated when continuous replication exceeds this limit.
6. In **Recovery point retention**, specify (in hours) the duration of the retention window for each recovery point. Protected machines can be recovered to any point within a retention window.

    > [!NOTE]
    > Up to 24 hours of retention is supported for machines replicated to premium storage. Up to 72 hours of retention is supported for machines replicated to standard storage.

    > [!NOTE]
    > A replication policy for failback is automatically created.

7. In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.

8. Click **OK**. The policy should be created in 30 to 60 seconds.

![Replication policy generation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a>Associate a configuration server with a replication policy
1. Choose the replication policy to which you want to associate the configuration server.
2. Click **Associate**.
![Associate configuration server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)

3. Select the configuration server from the list of servers.
4. Click **OK**. The configuration server should be associated in one to two minutes.

![Configuration server association](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.PNG)

## <a name="edit-a-replication-policy"></a>Edit a replication policy
1. Choose the replication policy for which you want to edit replication settings.
![Edit replication policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Select-Policy.PNG)

2. Click **Edit Settings**.
![Edit replication policy settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Edit-policy.PNG)

3. Change the settings based on your need.
4. Click **Save**. The policy should be saved in two to five minutes, depending on how many VMs are using that replication policy.

![Save replication policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Save-Policy.PNG)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a>Dissociate a configuration server from a replication policy
1. Choose the replication policy to which you want to associate the configuration server.
2. Click **Dissociate**.
3. Select the configuration server from the list of servers.
4. Click **OK**. The configuration server should be dissociated in one to two minutes.

    > [!NOTE]
    > You cannot dissociate a configuration server if there is at least one replicated item using the policy. Make sure there are no replicated items using the policy before you dissociate the configuration server.

## <a name="delete-a-replication-policy"></a>Delete a replication policy

1. Choose the replication policy that you want to delete.
2. Click **Delete**. The policy should be deleted in 30 to 60 seconds.

    > [!NOTE]
    > You cannot delete a replication policy if it has at least one configuration server associated to it. Make sure there are no replicated items using the policy and delete all the associated configuration servers before you delete the policy.







