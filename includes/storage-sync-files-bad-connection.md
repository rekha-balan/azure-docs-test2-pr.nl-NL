---
title: include file
description: include file
services: storage
author: wmgries
ms.service: storage
ms.topic: include
ms.date: 07/08/2018
ms.author: wgries
ms.custom: include file
ms.openlocfilehash: f17fe2b5d2b636fd51b51f45d6381bcbe14bc1f5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965681"
---
<span data-ttu-id="c30ab-103">This error can occur whenever the Azure File Sync service is inaccessible from the server.</span><span class="sxs-lookup"><span data-stu-id="c30ab-103">This error can occur whenever the Azure File Sync service is inaccessible from the server.</span></span> <span data-ttu-id="c30ab-104">You can troubleshoot this error by working through the following steps:</span><span class="sxs-lookup"><span data-stu-id="c30ab-104">You can troubleshoot this error by working through the following steps:</span></span>

1. <span data-ttu-id="c30ab-105">Verify the Windows service `FileSyncSvc.exe` is not blocked by your firewall.</span><span class="sxs-lookup"><span data-stu-id="c30ab-105">Verify the Windows service `FileSyncSvc.exe` is not blocked by your firewall.</span></span>
2. <span data-ttu-id="c30ab-106">Verify that port 443 is open to outgoing connections to the Azure File Sync service.</span><span class="sxs-lookup"><span data-stu-id="c30ab-106">Verify that port 443 is open to outgoing connections to the Azure File Sync service.</span></span> <span data-ttu-id="c30ab-107">You can do this with the `Test-NetConnection` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c30ab-107">You can do this with the `Test-NetConnection` cmdlet.</span></span> <span data-ttu-id="c30ab-108">The URL for the `<azure-file-sync-endpoint>` placeholder below can found in the [Azure File Sync proxy and firewall settings](../articles/storage/files/storage-sync-files-firewall-and-proxy.md#firewall) document.</span><span class="sxs-lookup"><span data-stu-id="c30ab-108">The URL for the `<azure-file-sync-endpoint>` placeholder below can found in the [Azure File Sync proxy and firewall settings](../articles/storage/files/storage-sync-files-firewall-and-proxy.md#firewall) document.</span></span> 

    ```PowerShell
    Test-NetConnection -ComputerName <azure-file-sync-endpoint> -Port 443
    ```

3. <span data-ttu-id="c30ab-109">Ensure that the proxy configuration is set as anticipated.</span><span class="sxs-lookup"><span data-stu-id="c30ab-109">Ensure that the proxy configuration is set as anticipated.</span></span> <span data-ttu-id="c30ab-110">This can be done with the `Get-StorageSyncProxyConfiguration` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c30ab-110">This can be done with the `Get-StorageSyncProxyConfiguration` cmdlet.</span></span> <span data-ttu-id="c30ab-111">More information on configuring the proxy configuration for Azure File Sync can be found in the [Azure File Sync proxy and firewall settings](../articles/storage/files/storage-sync-files-firewall-and-proxy.md#firewall).</span><span class="sxs-lookup"><span data-stu-id="c30ab-111">More information on configuring the proxy configuration for Azure File Sync can be found in the [Azure File Sync proxy and firewall settings](../articles/storage/files/storage-sync-files-firewall-and-proxy.md#firewall).</span></span>

    ```PowerShell
    $agentPath = "C:\Program Files\Azure\StorageSyncAgent"
    Import-Module "$agentPath\StorageSync.Management.ServerCmdlets.dll"
    Get-StorageSyncProxyConfiguration
    ```
    
4. <span data-ttu-id="c30ab-112">Contact your network administrator for additional assistance troubleshooting network connectivity.</span><span class="sxs-lookup"><span data-stu-id="c30ab-112">Contact your network administrator for additional assistance troubleshooting network connectivity.</span></span>