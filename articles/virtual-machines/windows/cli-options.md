---
title: Using the Azure CLI on Windows | Microsoft Docs
description: Using the Azure CLI on Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: 72d9979d109f72e3950410eab3af760fec228d17
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551457"
---
# <a name="using-the-azure-cli-on-windows"></a><span data-ttu-id="8e32b-103">Using the Azure CLI on Windows</span><span class="sxs-lookup"><span data-stu-id="8e32b-103">Using the Azure CLI on Windows</span></span>

<span data-ttu-id="8e32b-104">The Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span><span class="sxs-lookup"><span data-stu-id="8e32b-104">The Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="8e32b-105">The Azure CLI is available for macOS, Linux, and Windows operating systems.</span><span class="sxs-lookup"><span data-stu-id="8e32b-105">The Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="8e32b-106">Across these operating systems, the CLI commands are identical, however operating system specific scripting syntax can differ.</span><span class="sxs-lookup"><span data-stu-id="8e32b-106">Across these operating systems, the CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="8e32b-107">This document details the ways that the Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span><span class="sxs-lookup"><span data-stu-id="8e32b-107">This document details the ways that the Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="8e32b-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8e32b-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="8e32b-109">Windows Subsystem for Linux</span><span class="sxs-lookup"><span data-stu-id="8e32b-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="8e32b-110">The Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span><span class="sxs-lookup"><span data-stu-id="8e32b-110">The Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="8e32b-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span><span class="sxs-lookup"><span data-stu-id="8e32b-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="8e32b-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span><span class="sxs-lookup"><span data-stu-id="8e32b-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="8e32b-113">To use the Azure CLI in WSL, complete the following.</span><span class="sxs-lookup"><span data-stu-id="8e32b-113">To use the Azure CLI in WSL, complete the following.</span></span>

|<span data-ttu-id="8e32b-114">Task</span><span class="sxs-lookup"><span data-stu-id="8e32b-114">Task</span></span> | <span data-ttu-id="8e32b-115">Instructions</span><span class="sxs-lookup"><span data-stu-id="8e32b-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="8e32b-116">Enable WSL</span><span class="sxs-lookup"><span data-stu-id="8e32b-116">Enable WSL</span></span> | [<span data-ttu-id="8e32b-117">Install WSL documentation </span><span class="sxs-lookup"><span data-stu-id="8e32b-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="8e32b-118">Install the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8e32b-118">Install the Azure CLI</span></span> |[<span data-ttu-id="8e32b-119">Install the CLI on WSL/Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="8e32b-119">Install the CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="8e32b-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e32b-120">PowerShell</span></span>

<span data-ttu-id="8e32b-121">The Azure CLI can be run natively in Windows.</span><span class="sxs-lookup"><span data-stu-id="8e32b-121">The Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="8e32b-122">In this configuration, the Azure CLI package is installed on the Windows operating system, and commands can be run from PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8e32b-122">In this configuration, the Azure CLI package is installed on the Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="8e32b-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span><span class="sxs-lookup"><span data-stu-id="8e32b-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="8e32b-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span><span class="sxs-lookup"><span data-stu-id="8e32b-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="8e32b-125">To use the Azure CLI on Windows, install the package using these instructions, [Install the CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="8e32b-125">To use the Azure CLI on Windows, install the package using these instructions, [Install the CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="8e32b-126">Docker Image</span><span class="sxs-lookup"><span data-stu-id="8e32b-126">Docker Image</span></span>

<span data-ttu-id="8e32b-127">When using Docker for Windows, a Docker image can be started that includes the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8e32b-127">When using Docker for Windows, a Docker image can be started that includes the Azure CLI.</span></span> <span data-ttu-id="8e32b-128">This image is based off of Linux, and includes a native Bash experience.</span><span class="sxs-lookup"><span data-stu-id="8e32b-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="8e32b-129">When using Docker for Windows and the Azure CLI image, scripts to be shared between macOS, Linux, and Windows.</span><span class="sxs-lookup"><span data-stu-id="8e32b-129">When using Docker for Windows and the Azure CLI image, scripts to be shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="8e32b-130">To use the Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run the following command.</span><span class="sxs-lookup"><span data-stu-id="8e32b-130">To use the Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run the following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="8e32b-131">Once completed, a Bash session will start that is preloaded with the Azure CLI tools.</span><span class="sxs-lookup"><span data-stu-id="8e32b-131">Once completed, a Bash session will start that is preloaded with the Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e32b-132">Next Steps</span><span class="sxs-lookup"><span data-stu-id="8e32b-132">Next Steps</span></span>

[<span data-ttu-id="8e32b-133">CLI sample for Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="8e32b-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="8e32b-134">CLI samples for Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="8e32b-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="8e32b-135">CLI samples for Azure SQL</span><span class="sxs-lookup"><span data-stu-id="8e32b-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
