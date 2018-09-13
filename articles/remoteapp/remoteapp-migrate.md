---
title: Migrate user data from Azure RemoteApp | Microsoft Docs
description: Learn how to migrate your user data in and out of Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 39dd726078c4dcc55063300bdca998ad822feadd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662566"
---
# <a name="how-to-migrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="80384-103">How to migrate data into and out of Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="80384-103">How to migrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="80384-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="80384-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="80384-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="80384-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="80384-106">You can use many different tools and methods to transfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="80384-106">You can use many different tools and methods to transfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="80384-107">Here are a few methods:</span><span class="sxs-lookup"><span data-stu-id="80384-107">Here are a few methods:</span></span>

* <span data-ttu-id="80384-108">Copy and paste using clipboard sharing</span><span class="sxs-lookup"><span data-stu-id="80384-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="80384-109">Copy files and data to a file server</span><span class="sxs-lookup"><span data-stu-id="80384-109">Copy files and data to a file server</span></span>
* <span data-ttu-id="80384-110">Copy files to OneDrive for Business through a browser</span><span class="sxs-lookup"><span data-stu-id="80384-110">Copy files to OneDrive for Business through a browser</span></span>
* <span data-ttu-id="80384-111">Copy files using redirection</span><span class="sxs-lookup"><span data-stu-id="80384-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="80384-112">You cannot enable the OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="80384-112">You cannot enable the OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="80384-113">Use copy and paste in File Explorer</span><span class="sxs-lookup"><span data-stu-id="80384-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="80384-114">Copy and paste using the clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span><span class="sxs-lookup"><span data-stu-id="80384-114">Copy and paste using the clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="80384-115">This lets users copy files between their local PC and RemoteApp apps.</span><span class="sxs-lookup"><span data-stu-id="80384-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="80384-116">Often, through the normal course of using apps in RemoteApp, users have saved files to their UPDs - moving that data out of RemoteApp is easy:</span><span class="sxs-lookup"><span data-stu-id="80384-116">Often, through the normal course of using apps in RemoteApp, users have saved files to their UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="80384-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span><span class="sxs-lookup"><span data-stu-id="80384-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="80384-118">(Note that this is an administrative task.)</span><span class="sxs-lookup"><span data-stu-id="80384-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="80384-119">Direct your users to launch the File Explorer app you published and to use that to copy and paste files both into their UPD and out of it.</span><span class="sxs-lookup"><span data-stu-id="80384-119">Direct your users to launch the File Explorer app you published and to use that to copy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-to-a-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="80384-120">Upload files and data to a file server by using standard network file copy</span><span class="sxs-lookup"><span data-stu-id="80384-120">Upload files and data to a file server by using standard network file copy</span></span>
<span data-ttu-id="80384-121">Often organizations use file servers to store general data.</span><span class="sxs-lookup"><span data-stu-id="80384-121">Often organizations use file servers to store general data.</span></span> <span data-ttu-id="80384-122">If you know the server name or location, your users can browse the local network for the server and then copy their files there, much like they did above.</span><span class="sxs-lookup"><span data-stu-id="80384-122">If you know the server name or location, your users can browse the local network for the server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="80384-123">Again you'll want to publish File Explorer to RemoteApp and then share it with your users.</span><span class="sxs-lookup"><span data-stu-id="80384-123">Again you'll want to publish File Explorer to RemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="80384-124">The file server must be on the routable network that RemoteApp was deployed into.</span><span class="sxs-lookup"><span data-stu-id="80384-124">The file server must be on the routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-to-onedrive-for-business"></a><span data-ttu-id="80384-125">Copy files to OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="80384-125">Copy files to OneDrive for Business</span></span>
<span data-ttu-id="80384-126">Although you cannot enable the OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD to OneDrive for Business through a browser.</span><span class="sxs-lookup"><span data-stu-id="80384-126">Although you cannot enable the OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD to OneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="80384-127">Publish File Explorer to RemoteApp and then tell users to access the files through that app.</span><span class="sxs-lookup"><span data-stu-id="80384-127">Publish File Explorer to RemoteApp and then tell users to access the files through that app.</span></span> 
2. <span data-ttu-id="80384-128">It's easiest to transfer files if they are compressed, so users should create a .zip file that contains all of the files to move to OneDrive for Business.</span><span class="sxs-lookup"><span data-stu-id="80384-128">It's easiest to transfer files if they are compressed, so users should create a .zip file that contains all of the files to move to OneDrive for Business.</span></span>
3. <span data-ttu-id="80384-129">Ask users to go to the Office 365 portal, and then go to OneDrive and upload the .zip file.</span><span class="sxs-lookup"><span data-stu-id="80384-129">Ask users to go to the Office 365 portal, and then go to OneDrive and upload the .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="80384-130">Copy files by using drive redirection</span><span class="sxs-lookup"><span data-stu-id="80384-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="80384-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span><span class="sxs-lookup"><span data-stu-id="80384-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="80384-132">In this case, they can zip their files on the redirected drive and then save them to their local PC.</span><span class="sxs-lookup"><span data-stu-id="80384-132">In this case, they can zip their files on the redirected drive and then save them to their local PC.</span></span>

