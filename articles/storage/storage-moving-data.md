---
title: Moving large amounts of data to/from cloud storage in Azure | Microsoft Docs
description: An overview of the different methods for moving data to and from Azure Storage.
services: storage
documentationcenter: ''
author: JarrettRenshaw
manager: msmets
editor: tysonn
ms.assetid: 5e3947a9-d99b-4108-9d57-3eb67c03e7ba
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: jarrettr
ms.openlocfilehash: 538a43e549f47709616dd93e7eab9c8cb7d99dc6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555697"
---
# <a name="moving-data-to-and-from-azure-storage"></a>Moving data to and from Azure Storage
If you want to move on-premises data to Azure Storage (or vice versa), there are a variety of ways to do this. The approach that works best for you will depend on your scenario. This article will provide a quick overview of different scenarios and appropriate offerings for each one.

## <a name="building-applications"></a>Building Applications
If you're building an application, developing against the REST API or one of our many client libraries is a great way to move data to and from Azure Storage.

Azure Storage provides rich client libraries for .NET, iOS, Java, Android, Universal Windows Platform (UWP), Xamarin, C++, Node.JS, PHP, Ruby, and Python. The client libraries offer advanced capabilities such as retry logic, logging, and parallel uploads. You can also develop directly against the REST API, which can be called by any language that makes HTTP/HTTPS requests.

See [Get Started with Azure Blob Storage](storage-dotnet-how-to-use-blobs.md) to learn more.

In addition, we also offer the [Azure Storage Data Movement Library](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) which is a library designed for high-performance copying of data to and from Azure. Please refer to our Data Movement Library [documentation](https://github.com/Azure/azure-storage-net-data-movement) to learn more. 

## <a name="quickly-viewinginteracting-with-your-data"></a>Quickly viewing/interacting with your data
If you want an easy way to view your Azure Storage data while also having the ability to upload and download your data, then consider using an Azure Storage Explorer.

Check out our list of [Azure Storage Explorers](storage-explorers.md) to learn more.

## <a name="system-administration"></a>System Administration
If you require or are more comfortable with a command-line utility (e.g. System Administrators), here are a few options for you to consider:

### <a name="azcopy"></a>AzCopy
AzCopy is a Windows command-line utility designed for high-performance copying of data to and from Azure Storage. You can also copy data within a storage account, or between different storage accounts.

See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md) to learn more.

### <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell is a module that provides cmdlets for managing services on Azure. It's a task-based command-line shell and scripting language designed especially for system administration.

See [Using Azure PowerShell with Azure Storage](storage-powershell-guide-full.md) to learn more.

### <a name="azure-cli"></a>Azure CLI
Azure CLI provides a set of open source, cross-platform commands for working with Azure services. Azure CLI is available on Windows, OSX, and Linux.

See [Using the Azure CLI with Azure Storage](storage-azure-cli.md) to learn more.

## <a name="moving-large-amounts-of-data-with-a-slow-network"></a>Moving large amounts of data with a slow network
One of the biggest challenges associated with moving large amounts of data is the transfer time. If you want to get data to/from Azure Storage without worrying about networks costs or writing code, then Azure Import/Export is an appropriate solution.

See [Azure Import/Export](storage-import-export-service.md) to learn more.

## <a name="backing-up-your-data"></a>Backing up your data
If you simply need to backup your data to Azure Storage, Azure Backup is the way to go. This is a powerful solution for backing up on-premises data and Azure VMs.

See [Azure Backup](../backup/backup-introduction-to-azure-backup.md) to learn more.

## <a name="accessing-your-data-on-premises-and-from-the-cloud"></a>Accessing your data on-premises and from the cloud
If you need a solution for accessing your data on-premises and from the cloud, then you should consider using Azure's hybrid cloud storage solution, StorSimple. This solution consists of a physical StorSimple device that intelligently stores frequently used data on SSDs, occasionally used data on HDDs, and inactive/backup/archival data on Azure Storage.

See [StorSimple](../storsimple/storsimple-overview.md) to learn more.

## <a name="recovering-your-data"></a>Recovering your data
When you have on-premises workloads and applications, you'll need a solution that allows your business to continue running in the event of a disaster. Azure Site Recovery handles replication, failover, and recovery of virtual machines and physical servers. Replicated data is stored in Azure Storage, allowing you to eliminate the need for a secondary on-site datacenter.

See [Azure Site Recovery](../site-recovery/site-recovery-overview.md) to learn more.
### <a name="moving-data-faq"></a>Moving Data FAQ:
## <a name="can-i-migrate-vhds-from-one-region-to-another-without-copying"></a>Can I migrate VHDs from one region to another without copying?
The only way to copy VHDs between region is to copy the data between storage accounts on each region. You can use AZCopy for this. See Transfer data with the AzCopy Command-Line Utility to learn more. For very large amounts of data, you can also Azure Import/Export. See [Azure Import/Export](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) to learn more.
