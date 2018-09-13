---
title: Troubleshooting Docker client errors on Windows by using Visual Studio | Microsoft Docs
description: Troubleshoot problems you encounter when using Visual Studio to create and deploy web apps to Docker on Windows by using Visual Studio.
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: ''
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 89fa04a1107b6abb49aefd68066443717ac9b731
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551006"
---
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="4afc2-103">Troubleshoot Visual Studio Docker development</span><span class="sxs-lookup"><span data-stu-id="4afc2-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="4afc2-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of the nature of the preview.</span><span class="sxs-lookup"><span data-stu-id="4afc2-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of the nature of the preview.</span></span>
<span data-ttu-id="4afc2-105">Following are some common issues and resolutions.</span><span class="sxs-lookup"><span data-stu-id="4afc2-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="4afc2-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="4afc2-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="4afc2-107">**Linux containers**</span><span class="sxs-lookup"><span data-stu-id="4afc2-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="4afc2-108">Build errors occur when debugging a .NET Core web or console application</span><span class="sxs-lookup"><span data-stu-id="4afc2-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="4afc2-109">This could be related to not sharing the drive where the project resides with Docker for Windows.</span><span class="sxs-lookup"><span data-stu-id="4afc2-109">This could be related to not sharing the drive where the project resides with Docker for Windows.</span></span>  <span data-ttu-id="4afc2-110">You may receive an error like the following:</span><span class="sxs-lookup"><span data-stu-id="4afc2-110">You may receive an error like the following:</span></span>

```
The "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with the default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="4afc2-111">To resolve this issue:</span><span class="sxs-lookup"><span data-stu-id="4afc2-111">To resolve this issue:</span></span>

1. <span data-ttu-id="4afc2-112">Right-click **Docker for Windows** in the notification area, and then select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="4afc2-112">Right-click **Docker for Windows** in the notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="4afc2-113">Select **Shared Drives** and share the drive where the project resides.</span><span class="sxs-lookup"><span data-stu-id="4afc2-113">Select **Shared Drives** and share the drive where the project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="4afc2-114">**Windows containers**</span><span class="sxs-lookup"><span data-stu-id="4afc2-114">**Windows containers**</span></span>

<span data-ttu-id="4afc2-115">The following issues are specific to debugging .NET Framework web and console applications in Windows containers.</span><span class="sxs-lookup"><span data-stu-id="4afc2-115">The following issues are specific to debugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="4afc2-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4afc2-116">Prerequisites</span></span>

1. <span data-ttu-id="4afc2-117">Visual Studio 2017 RC (or later) with the .NET Core and Docker Preview workload must be installed.</span><span class="sxs-lookup"><span data-stu-id="4afc2-117">Visual Studio 2017 RC (or later) with the .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="4afc2-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span><span class="sxs-lookup"><span data-stu-id="4afc2-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="4afc2-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span><span class="sxs-lookup"><span data-stu-id="4afc2-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="4afc2-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span><span class="sxs-lookup"><span data-stu-id="4afc2-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="4afc2-121">**Switch to Windows containers** must be selected.</span><span class="sxs-lookup"><span data-stu-id="4afc2-121">**Switch to Windows containers** must be selected.</span></span> <span data-ttu-id="4afc2-122">In the notification area, click **Docker for Windows**, and then select **Switch to Windows containers**.</span><span class="sxs-lookup"><span data-stu-id="4afc2-122">In the notification area, click **Docker for Windows**, and then select **Switch to Windows containers**.</span></span> <span data-ttu-id="4afc2-123">After the machine restarts, ensure that this setting is retained.</span><span class="sxs-lookup"><span data-stu-id="4afc2-123">After the machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="4afc2-124">Console output does not appear in Visual Studio's output window while debugging a console application</span><span class="sxs-lookup"><span data-stu-id="4afc2-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="4afc2-125">This is a known issue with the Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span><span class="sxs-lookup"><span data-stu-id="4afc2-125">This is a known issue with the Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="4afc2-126">Support for this scenario might be included in a future release.</span><span class="sxs-lookup"><span data-stu-id="4afc2-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="4afc2-127">To see output from the console application in Visual Studio, use **Docker: Start Project**, which is equivalent to **Start without Debugging**.</span><span class="sxs-lookup"><span data-stu-id="4afc2-127">To see output from the console application in Visual Studio, use **Docker: Start Project**, which is equivalent to **Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-the-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="4afc2-128">Debugging web applications with the release configuration fails with (403) Forbidden error</span><span class="sxs-lookup"><span data-stu-id="4afc2-128">Debugging web applications with the release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="4afc2-129">To work around this issue, open web.release.config in the solution and comment out or delete the following lines:</span><span class="sxs-lookup"><span data-stu-id="4afc2-129">To work around this issue, open web.release.config in the solution and comment out or delete the following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="4afc2-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="4afc2-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="4afc2-131">**Linux containers**</span><span class="sxs-lookup"><span data-stu-id="4afc2-131">**Linux containers**</span></span>

#### <a name="unable-to-validate-volume-mapping"></a><span data-ttu-id="4afc2-132">Unable to validate volume mapping</span><span class="sxs-lookup"><span data-stu-id="4afc2-132">Unable to validate volume mapping</span></span>
<span data-ttu-id="4afc2-133">Volume mapping is required to share the source code and binaries of your application with the app folder in the container.</span><span class="sxs-lookup"><span data-stu-id="4afc2-133">Volume mapping is required to share the source code and binaries of your application with the app folder in the container.</span></span>  <span data-ttu-id="4afc2-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span><span class="sxs-lookup"><span data-stu-id="4afc2-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="4afc2-135">As files are changed on your host machine, the containers reflect these changes in a similar folder structure.</span><span class="sxs-lookup"><span data-stu-id="4afc2-135">As files are changed on your host machine, the containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="4afc2-136">To enable volume mapping:</span><span class="sxs-lookup"><span data-stu-id="4afc2-136">To enable volume mapping:</span></span>

1. <span data-ttu-id="4afc2-137">Click **Moby** in the notification area and select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="4afc2-137">Click **Moby** in the notification area and select **Settings**.</span></span>
2. <span data-ttu-id="4afc2-138">Select **Shared Drives**.</span><span class="sxs-lookup"><span data-stu-id="4afc2-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="4afc2-139">Select the drive that hosts your project and the drive where %USERPROFILE% resides.</span><span class="sxs-lookup"><span data-stu-id="4afc2-139">Select the drive that hosts your project and the drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="4afc2-140">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="4afc2-140">Click **Apply**.</span></span>

<span data-ttu-id="4afc2-141">To test if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run the following code from a command prompt.</span><span class="sxs-lookup"><span data-stu-id="4afc2-141">To test if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run the following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="4afc2-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span><span class="sxs-lookup"><span data-stu-id="4afc2-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="4afc2-143">Revise as necessary if you have shared a different drive.</span><span class="sxs-lookup"><span data-stu-id="4afc2-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="4afc2-144">Run the following code in the Linux container.</span><span class="sxs-lookup"><span data-stu-id="4afc2-144">Run the following code in the Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="4afc2-145">You should see a directory listing from the Users/Public folder.</span><span class="sxs-lookup"><span data-stu-id="4afc2-145">You should see a directory listing from the Users/Public folder.</span></span> <span data-ttu-id="4afc2-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span><span class="sxs-lookup"><span data-stu-id="4afc2-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="4afc2-147">Change to the wormhole directory to see the contents of the `/c/Users/Public` directory:</span><span class="sxs-lookup"><span data-stu-id="4afc2-147">Change to the wormhole directory to see the contents of the `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="4afc2-148">When you're working with Linux VMs, the container file system is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="4afc2-148">When you're working with Linux VMs, the container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="4afc2-149">Build: "PrepareForBuild" task failed unexpectedly</span><span class="sxs-lookup"><span data-stu-id="4afc2-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="4afc2-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying to connect.</span><span class="sxs-lookup"><span data-stu-id="4afc2-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying to connect.</span></span>

<span data-ttu-id="4afc2-151">Verify that the default Docker host is running.</span><span class="sxs-lookup"><span data-stu-id="4afc2-151">Verify that the default Docker host is running.</span></span> <span data-ttu-id="4afc2-152">Open a command prompt and execute:</span><span class="sxs-lookup"><span data-stu-id="4afc2-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="4afc2-153">If this returns an error, then attempt to start the **Docker for Windows** desktop app.</span><span class="sxs-lookup"><span data-stu-id="4afc2-153">If this returns an error, then attempt to start the **Docker for Windows** desktop app.</span></span> <span data-ttu-id="4afc2-154">If the desktop app is running, then **Moby** should be visible in the notification area.</span><span class="sxs-lookup"><span data-stu-id="4afc2-154">If the desktop app is running, then **Moby** should be visible in the notification area.</span></span> <span data-ttu-id="4afc2-155">Right-click **Moby** and open **Settings**.</span><span class="sxs-lookup"><span data-stu-id="4afc2-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="4afc2-156">Click **Reset**, and then restart Docker.</span><span class="sxs-lookup"><span data-stu-id="4afc2-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-to-add-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="4afc2-157">An error dialog occurs when attempting to add Docker Support or debug (F5) an ASP.NET Core application in a container</span><span class="sxs-lookup"><span data-stu-id="4afc2-157">An error dialog occurs when attempting to add Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="4afc2-158">After uninstalling and installing extensions, the Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span><span class="sxs-lookup"><span data-stu-id="4afc2-158">After uninstalling and installing extensions, the Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="4afc2-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting to run or debug (F5) your ASP.NET Core application.</span><span class="sxs-lookup"><span data-stu-id="4afc2-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting to run or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="4afc2-160">As a temporary workaround, use the following steps to delete and regenerate the MEF cache.</span><span class="sxs-lookup"><span data-stu-id="4afc2-160">As a temporary workaround, use the following steps to delete and regenerate the MEF cache.</span></span>

1. <span data-ttu-id="4afc2-161">Close all instances of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4afc2-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="4afc2-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span><span class="sxs-lookup"><span data-stu-id="4afc2-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="4afc2-163">Delete the following folders:</span><span class="sxs-lookup"><span data-stu-id="4afc2-163">Delete the following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="4afc2-164">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4afc2-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="4afc2-165">Attempt the scenario again.</span><span class="sxs-lookup"><span data-stu-id="4afc2-165">Attempt the scenario again.</span></span>
