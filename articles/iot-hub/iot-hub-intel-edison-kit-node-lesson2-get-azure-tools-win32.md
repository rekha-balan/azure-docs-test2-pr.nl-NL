---
title: 'Connect Intel Edison (Node) to Azure IoT - Lesson 2: Azure tools (Windows) | Microsoft Docs'
description: Install Python and the Azure command-line interface (Azure CLI) on Windows 7 and later versions.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: azure cli, iot cloud service, arduino cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 60631b54-6d2e-4e8a-88bf-7c2f8e7e1f29
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9e071f2cbaac0fdde97cff7a3c564de30f4a4299
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552393"
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="fb69c-104">Get Azure tools (Windows 7 and later)</span><span class="sxs-lookup"><span data-stu-id="fb69c-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [Windows 7 and later][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a><span data-ttu-id="fb69c-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="fb69c-108">What you will do</span></span>
<span data-ttu-id="fb69c-109">Install Python and the Azure command-line interface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="fb69c-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="fb69c-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="fb69c-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fb69c-111">What you will learn</span><span class="sxs-lookup"><span data-stu-id="fb69c-111">What you will learn</span></span>
<span data-ttu-id="fb69c-112">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="fb69c-112">In this article, you will learn:</span></span>
* <span data-ttu-id="fb69c-113">How to install Python.</span><span class="sxs-lookup"><span data-stu-id="fb69c-113">How to install Python.</span></span>
* <span data-ttu-id="fb69c-114">How to install the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="fb69c-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fb69c-115">What you need</span><span class="sxs-lookup"><span data-stu-id="fb69c-115">What you need</span></span>
* <span data-ttu-id="fb69c-116">A Windows computer with an Internet connection.</span><span class="sxs-lookup"><span data-stu-id="fb69c-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="fb69c-117">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="fb69c-117">An active Azure subscription.</span></span> <span data-ttu-id="fb69c-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="fb69c-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="fb69c-119">Install Python</span><span class="sxs-lookup"><span data-stu-id="fb69c-119">Install Python</span></span>
<span data-ttu-id="fb69c-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span><span class="sxs-lookup"><span data-stu-id="fb69c-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="fb69c-121">You can install Python 2.7, 3.4 or 3.5.</span><span class="sxs-lookup"><span data-stu-id="fb69c-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="fb69c-122">This tutorial is based on Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="fb69c-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="fb69c-123">If you've already installed Python, go to the next section and install the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="fb69c-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="fb69c-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span><span class="sxs-lookup"><span data-stu-id="fb69c-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="fb69c-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="fb69c-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="fb69c-126">Install the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fb69c-126">Install the Azure CLI</span></span>
<span data-ttu-id="fb69c-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span><span class="sxs-lookup"><span data-stu-id="fb69c-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="fb69c-128">You work directly from your command line to provision and manage resources.</span><span class="sxs-lookup"><span data-stu-id="fb69c-128">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="fb69c-129">To install the Azure CLI, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="fb69c-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="fb69c-130">Open a Command Prompt window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="fb69c-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="fb69c-131">Run the following commands:</span><span class="sxs-lookup"><span data-stu-id="fb69c-131">Run the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="fb69c-132">Verify the installation by running the following command:</span><span class="sxs-lookup"><span data-stu-id="fb69c-132">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

<span data-ttu-id="fb69c-133">You see the following output if the installation is successful.</span><span class="sxs-lookup"><span data-stu-id="fb69c-133">You see the following output if the installation is successful.</span></span>

![Output that indicates success](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="fb69c-135">Summary</span><span class="sxs-lookup"><span data-stu-id="fb69c-135">Summary</span></span>
<span data-ttu-id="fb69c-136">You've installed the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="fb69c-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="fb69c-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="fb69c-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb69c-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="fb69c-138">Next steps</span></span>
<span data-ttu-id="fb69c-139">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]
<!-- Images and links --></span><span class="sxs-lookup"><span data-stu-id="fb69c-139">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]
<!-- Images and links --></span></span>

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md

