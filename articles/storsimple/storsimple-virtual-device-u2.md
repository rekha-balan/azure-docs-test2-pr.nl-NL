---
title: StorSimple virtual device Update 2| Microsoft Docs
description: Learn how to create, deploy, and manage a StorSimple virtual device in a Microsoft Azure virtual network. (Applies to StorSimple Update 2).
services: storsimple
documentationcenter: ''
author: alkohli
manager: timlt
editor: ''
ms.assetid: f37752a5-cd0c-479b-bef2-ac2c724bcc37
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.openlocfilehash: d9ba200dba2b1460a9d3c9ba07e2bca54c30b53a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661143"
---
# <a name="deploy-and-manage-a-storsimple-virtual-device-in-azure"></a>Deploy and manage a StorSimple virtual device in Azure
## <a name="overview"></a>Overview
The StorSimple 8000 series virtual device is an additional capability that comes with your Microsoft Azure StorSimple solution. The StorSimple virtual device runs on a virtual machine in a Microsoft Azure virtual network, and you can use it to back up and clone data from your hosts. This tutorial describes how to deploy and manage a virtual device in Azure and is applicable to all the virtual devices running software version Update 2 and lower.

#### <a name="virtual-device-model-comparison"></a>Virtual device model comparison
The StorSimple virtual device is available in two models, a standard 8010 (formerly known as the 1100) and a premium 8020 (introduced in Update 2). A comparison of the two models is tabulated below.

| Device model | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Maximum capacity** |30 TB |64 TB |
| **Azure VM** |Standard_A3 (4 cores, 7 GB memory) |Standard_DS3 (4 cores, 14 GB memory) |
| **Version compatibility** |Versions running pre-Update 2 or later |Versions running Update 2 or later |
| **Region availability** |All Azure regions |All Azure regions that support Premium Storage and DS3 Azure VMs<br></br> Use [this list](https://azure.microsoft.com/en-us/regions/services) to see if both *Virtual Machines > DS-series* and *Storage > Disk storage* are available in your region. |
| **Storage type** |Uses Azure Standard Storage for local disks<br></br> Learn how to [create a Standard Storage account](../storage/storage-create-storage-account.md) |Uses Azure Premium Storage for local disks<sup>2</sup> <br></br>Learn how to [create a Premium Storage account](../storage/storage-premium-storage.md) |
| **Workload guidance** |Item level retrieval of files from backups |Cloud dev and test scenarios, low latency, higher performance workloads <br></br>Secondary device for disaster recovery |

<sup>1</sup> *Formerly known as the 1100*.

<sup>2</sup> *Both the 8010 and 8020 use Azure Standard Storage for the cloud tier. The difference only exists in the local tier within the device*.

This article describes the step-by-step process of deploying a StorSimple virtual device in Azure. After reading this article, you will:

* Understand how the virtual device differs from the physical device.
* Be able to create and configure the virtual device.
* Connect to the virtual device.
* Learn how to work with the virtual device.

This tutorial applies to all the StorSimple virtual devices running Update 2 and higher.

## <a name="how-the-virtual-device-differs-from-the-physical-device"></a>How the virtual device differs from the physical device
The StorSimple virtual device is a software-only version of StorSimple that runs on a single node in a Microsoft Azure Virtual Machine. The virtual device supports disaster recovery scenarios in which your physical device is not available, and is appropriate for use in item-level retrieval from backups, on-premises disaster recovery, and cloud dev and test scenarios.

#### <a name="differences-from-the-physical-device"></a>Differences from the physical device
The following table shows some key differences between the StorSimple virtual device and the StorSimple physical device.

|  | Physical device | Virtual device |
| --- | --- | --- |
| **Location** |Resides in the datacenter. |Runs in Azure. |
| **Network interfaces** |Has six network interfaces: DATA 0 through DATA 5. |Has only one network interface: DATA 0. |
| **Registration** |Registered during the configuration step. |Registration is a separate task. |
| **Service data encryption key** |Regenerate on the physical device and then update the virtual device with the new key. |Cannot regenerate from the virtual device. |

## <a name="prerequisites-for-the-virtual-device"></a>Prerequisites for the virtual device
The following sections explain the configuration prerequisites for your StorSimple virtual device. Prior to deploying a virtual device, review the [security considerations for using a virtual device](storsimple-security.md#storsimple-virtual-device-security).

#### <a name="azure-requirements"></a>Azure requirements
Before you provision the virtual device, you need to make the following preparations in your Azure environment:

* For the virtual device, [configure a virtual network on Azure](../virtual-network/virtual-networks-create-vnet-classic-portal.md). If using Premium Storage, you must create a virtual network in an Azure region that supports Premium Storage. The Premium storage regions are regions that correspond to the row for *Disk storage* in the list of [Azure Services by Region](https://azure.microsoft.com/en-us/regions/services).
* It is advisable to use the default DNS server provided by Azure instead of specifying your own DNS server name. If your DNS server name is not valid or if the DNS server is not able to resolve IP addresses correctly, the creation of the virtual device will fail.
* Point-to-site and site-to-site are optional, but not required. If you wish, you can configure these options for more advanced scenarios.
* You can create [Azure Virtual Machines](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (host servers) in the virtual network that can use the volumes exposed by the virtual device. These servers must meet the following requirements:                             

  * Be Windows or Linux VMs with iSCSI Initiator software installed.
  * Be running in the same virtual network as the virtual device.
  * Be able to connect to the iSCSI target of the virtual device through the internal IP address of the virtual device.
* Make sure you have configured support for iSCSI and cloud traffic on the same virtual network.

#### <a name="storsimple-requirements"></a>StorSimple requirements
Make the following updates to your Azure StorSimple service before you create a virtual device:

* Add [access control records](storsimple-manage-acrs.md) for the VMs that are going to be host servers for your virtual device.
* Use a [storage account](storsimple-manage-storage-accounts.md#add-a-storage-account) in the same region as the virtual device. Storage accounts in different regions may result in poor performance. You can use a Standard or Premium Storage account with the virtual device. More information on how to create a [Standard Storage account](../storage/storage-create-storage-account.md) or a [Premium Storage account](../storage/storage-premium-storage.md)
* Use a different storage account for virtual device creation from the one used for your data. Using the same storage account may result in poor performance.

Make sure that you have the following information before you begin:

* Your Azure classic portal account with access credentials.
* A copy of the service data encryption key from your physical device.

## <a name="create-and-configure-the-virtual-device"></a>Create and configure the virtual device
Before performing these procedures, make sure that you have met the [Prerequisites for the virtual device](#prerequisites-for-the-virtual-device).

After you have created a virtual network, configured a StorSimple Manager service, and registered your physical StorSimple device with the service, you can use the following steps to create and configure a StorSimple virtual device.

### <a name="step-1-create-a-virtual-device"></a>Step 1: Create a virtual device
Perform the following steps to create the StorSimple virtual device.

[!INCLUDE [Create a virtual device](../../includes/storsimple-create-virtual-device-u2.md)]

If the creation of the virtual device fails in this step, you may not have connectivity to the Internet. For more information, go to [troubleshoot Internet connectivity failures](#troubleshoot-internet-connectivity-errors) when creating a virtual device.

### <a name="step-2-configure-and-register-the-virtual-device"></a>Step 2: Configure and register the virtual device
Before starting this procedure, make sure that you have a copy of the service data encryption key. The service data encryption key was created when you configured your first StorSimple device and you were instructed to save it in a secure location. If you do not have a copy of the service data encryption key, you must contact Microsoft Support for assistance.

Perform the following steps to configure and register your StorSimple virtual device.

[!INCLUDE [Configure and register a virtual device](../../includes/storsimple-configure-register-virtual-device.md)]

### <a name="step-3-optional-modify-the-device-configuration-settings"></a>Step 3: (Optional) Modify the device configuration settings
The following section describes the device configuration settings needed for the StorSimple virtual device if you want to use CHAP, StorSimple Snapshot Manager or change the Device Administrator password.

#### <a name="configure-the-chap-initiator"></a>Configure the CHAP initiator
This parameter contains the credentials that your virtual device (target) expects from the initiators (servers) that are attempting to access the volumes. The initiators will provide a CHAP user name and a CHAP password to identify themselves to your device during this authentication. For detailed steps, go to [Configure CHAP for your device](storsimple-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-the-chap-target"></a>Configure the CHAP target
This parameter contains the credentials that your virtual device uses when a CHAP-enabled initiator requests mutual or bi-directional authentication. Your virtual device will use a Reverse CHAP user name and Reverse CHAP password to identify itself to the initiator during this authentication process. Note that CHAP target settings are global settings. When these are applied, all the volumes connected to the storage virtual device will use CHAP authentication. For detailed steps, go to [Configure CHAP for your device](storsimple-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-the-storsimple-snapshot-manager-password"></a>Configure the StorSimple Snapshot Manager password
StorSimple Snapshot Manager software resides on your Windows host and allows administrators to manage backups of your StorSimple device in the form of local and cloud snapshots.

> [!NOTE]
> For the virtual device, your Windows host is an Azure virtual machine.
>
>

When configuring a device in the StorSimple Snapshot Manager, you will be prompted to provide the StorSimple device IP address and password to authenticate your storage device. For detailed steps, go to [Configure StorSimple Snapshot Manager password](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

#### <a name="change-the-device-administrator-password"></a>Change the device administrator password
When you use the Windows PowerShell interface to access the virtual device, you will be required to enter a device administrator password. For the security of your data, you are required to change this password before the virtual device can be used. For detailed steps, go to [Configure device administrator password](storsimple-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-to-the-virtual-device"></a>Connect remotely to the virtual device
Remote access to your virtual device via the Windows PowerShell interface is not enabled by default. You need to enable remote management on the virtual device first, and then enable it on the client that will be used to access your virtual device.

The two-step process to connect remotely is detailed below.

### <a name="step-1-configure-remote-management"></a>Step 1: Configure remote management
Perform the following steps to configure remote management for your StorSimple virtual device.

[!INCLUDE [Configure remote management via HTTP for virtual device](../../includes/storsimple-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-the-virtual-device"></a>Step 2: Remotely access the virtual device
After you have enabled remote management on the StorSimple device configuration page, you can use Windows PowerShell remoting to connect to the virtual device from another virtual machine inside the same virtual network; for example, you can connect from the host VM that you configured and used to connect iSCSI. In most deployments, you will have already opened a public endpoint to access your host VM that you can use for accessing the virtual device.

> [!WARNING]
> **For enhanced security, we strongly recommend that you use HTTPS when connecting to the endpoints and then delete the endpoints after you have completed your PowerShell remote session.**
>
>

You should follow the procedures in [Connecting remotely to your StorSimple device](storsimple-remote-connect.md) to set up remoting for your virtual device.

## <a name="connect-directly-to-the-virtual-device"></a>Connect directly to the virtual device
You can also connect directly to the virtual device. If you want to connect directly to the virtual device from another computer outside the virtual network or outside the Microsoft Azure environment, you need to create additional endpoints as described in the following procedure.

Perform the following steps to create a public endpoint on the virtual device.

[!INCLUDE [Create public endpoints on a virtual device](../../includes/storsimple-create-public-endpoints-virtual-device.md)]

We recommend that you connect from another virtual machine inside the same virtual network because this practice minimizes the number of public endpoints on your virtual network. When you use this method, you simply connect to the virtual machine through a Remote Desktop session and then configure that virtual machine for use as you would any other Windows client on a local network. You do not need to append the public port number because the port will already be known.

## <a name="work-with-the-storsimple-virtual-device"></a>Work with the StorSimple virtual device
Now that you have created and configured the StorSimple virtual device, you are ready to start working with it. You can work with volume containers, volumes, and backup policies on a virtual device just as you would on a physical StorSimple device; the only difference is that you need to make sure that you select the virtual device from your device list. Refer to [use the StorSimple Manager service to manage a virtual device](storsimple-manager-service-administration.md) for step-by-step procedures of the various management tasks for the virtual device.

The following sections discuss some of the differences you will encounter when working with the virtual device.

### <a name="maintain-a-storsimple-virtual-device"></a>Maintain a StorSimple virtual device
Because it is a software-only device, maintenance for the virtual device is minimal when compared to maintenance for the physical device. You have the following options:

* **Software updates** – You can view the date that the software was last updated, together with any update status messages. You can use the **Scan updates** button at the bottom of the page to perform a manual scan if you want to check for new updates. If updates are available, click **Install Updates** to install. Because there is only a single interface on the virtual device, this means that there will be a slight service interruption when updates are applied. The virtual device will shut down and restart (if necessary) to apply any updates that have been released. For a step-by-step procedure, go to [update your device](storsimple-update-device.md#install-regular-updates-via-the-azure-classic-portal).
* **Support package** – You can create and upload a support package to help Microsoft Support troubleshoot issues with your virtual device. For a step-by-step procedure, go to [create and manage a support package](storsimple-create-manage-support-package.md).

### <a name="storage-accounts-for-a-virtual-device"></a>Storage accounts for a virtual device
Storage accounts are created for use by the StorSimple Manager service, by the virtual device, and by the physical device. When you create your storage accounts, we recommend that you use a region identifier in the friendly name to help ensure that the region is consistent throughout all of the system components. For a virtual device, it is important that all of the components be in the same region to prevent performance issues.

For a step-by-step procedure, go to [add a storage account](storsimple-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-virtual-device"></a>Deactivate a StorSimple virtual device
Deactivating a virtual device deletes the VM and the resources created when it was provisioned. After the virtual device is deactivated, it cannot be restored to its previous state. Before you deactivate the virtual device, make sure to stop or delete clients and hosts that depend on it.

Deactivating a virtual device results in the following actions:

* The virtual device is removed.
* The OS disk and data disks created for the virtual device are removed.
* The hosted service and virtual network created during provisioning are retained. If you are not using them, you should delete them manually.
* Cloud snapshots created for the virtual device are retained.

For a step-by-step procedure, go to [Deactivate and delete your StorSimple device](storsimple-deactivate-and-delete-device.md).

As soon as the virtual device is shown as deactivated on the StorSimple Manager service page, you can delete the virtual device from device list on the **Devices** page.

### <a name="start-stop-and-restart-a-virtual-device"></a>Start, stop and restart a virtual device
Unlike the StorSimple physical device, there is no power on or power off button to push on a StorSimple virtual device. However, there may be occasions where you need to stop and restart the virtual device. For example, some updates might require that the VM be restarted to finish the update process. The easiest way for you to start, stop, and restart a virtual device is to use the Virtual Machines Management Console.

When you look at the Management Console, the virtual device status is **Running** because it is started by default after it is created. You can start, stop, and restart a virtual machine at any time.

[!INCLUDE [Stop and restart virtual device](../../includes/storsimple-stop-restart-virtual-device.md)]

### <a name="reset-to-factory-defaults"></a>Reset to factory defaults
If you decide that you just want to start over with your virtual device, simply deactivate and delete it and then create a new one. Just like when your physical device is reset, your new virtual device will not have any updates installed; therefore, make sure to check for updates before using it.

## <a name="fail-over-to-the-virtual-device"></a>Fail over to the virtual device
Disaster recovery (DR) is one of the key scenarios that the StorSimple virtual device was designed for. In this scenario, the physical StorSimple device or entire datacenter might not be available. Fortunately, you can use a virtual device to restore operations in an alternate location. During DR, the volume containers from the source device change ownership and are transferred to the virtual device. The prerequisites for DR are that the virtual device has been created and configured, all the volumes within the volume container have been taken offline, and the volume container has an associated cloud snapshot.

> [!NOTE]
> * When using a virtual device as the secondary device for DR, keep in mind that the 8010 has 30 TB of Standard Storage and 8020 has 64 TB of Premium Storage. The higher capacity 8020 virtual device may be more suited for a DR scenario.
> * You cannot failover or clone from a device running Update 2 to a device running pre-Update 1 software. You can however fail over a device running Update 2 to a device running Update 1 (1.1 or 1.2)
>
>

For a step-by-step procedure, go to [failover to a virtual device](storsimple-device-failover-disaster-recovery.md#fail-over-to-a-storsimple-virtual-device).

## <a name="shut-down-or-delete-the-virtual-device"></a>Shut down or delete the virtual device
If you previously configured and used a StorSimple virtual device but now want to stop accruing compute charges for its use, you can shut down the virtual device. Shutting down the virtual device doesn’t delete its operating system or data disks in storage. It does stop charges accruing on your subscription, but storage charges for the OS and data disks will continue.

If you delete or shut down the virtual device, it will appear as **Offline** on the Devices page of the StorSimple Manager service. You can choose to deactivate or delete the device if you also wish to delete the backups created by the virtual device. For more information, see [Deactivate and delete a StorSimple device](storsimple-deactivate-and-delete-device.md).

[!INCLUDE [Shut down a virtual device](../../includes/storsimple-shutdown-virtual-device.md)]

[!INCLUDE [Delete a virtual device](../../includes/storsimple-delete-virtual-device.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>Troubleshoot Internet connectivity errors
During the creation of a virtual device, if there is no connectivity to the Internet, the creation step will fail. To troubleshoot if the failure is because of Internet connectivity, perform the following steps in the Azure classic portal:

1. Create a Windows server 2012 virtual machine in Azure. This virtual machine should use the same storage account, VNet and subnet as used by your virtual device. If you already have an existing Windows Server host in Azure using the same storage account, Vnet and subnet, you can also use it to troubleshoot the Internet connectivity.
2. Remote log into the virtual machine created in the preceding step.
3. Open a command window inside the virtual machine (Win + R and then type `cmd`).
4. Run the following cmd at the prompt.

    `nslookup windows.net`
5. If `nslookup` fails, then Internet connectivity failure is preventing the virtual device from registering to the StorSimple Manager service.
6. Make the required changes to your virtual network to ensure that the virtual device is able to access Azure sites such as “windows.net”.

## <a name="next-steps"></a>Next steps
* Learn how to [use the StorSimple Manager service to manage a virtual device](storsimple-manager-service-administration.md).
* Understand how to [restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set.md).