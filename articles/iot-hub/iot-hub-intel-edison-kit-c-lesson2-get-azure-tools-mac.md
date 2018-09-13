---
title: 'Connect Intel Edison (C) to Azure IoT - Lesson 2: Azure tools (macOS) | Microsoft Docs'
description: Install Python and Azure command-line interface (Azure CLI) on macOS.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: azure cli, iot cloud service, arduino cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: d561680f-69cc-427a-820d-24f710ba05a8
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 317a7bebd58dfb6b9ad4d2d4a5a7b2999d87e702
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550037"
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="80b8b-104">Get Azure tools (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="80b8b-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [Windows 7 and later][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a><span data-ttu-id="80b8b-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="80b8b-108">What you will do</span></span>
<span data-ttu-id="80b8b-109">Install the Azure command-line interface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="80b8b-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="80b8b-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="80b8b-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="80b8b-111">What you will learn</span><span class="sxs-lookup"><span data-stu-id="80b8b-111">What you will learn</span></span>
<span data-ttu-id="80b8b-112">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="80b8b-112">In this article, you will learn:</span></span>
* <span data-ttu-id="80b8b-113">How to install Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="80b8b-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="80b8b-114">How to add an IoT subgroup of the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="80b8b-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="80b8b-115">What you need</span><span class="sxs-lookup"><span data-stu-id="80b8b-115">What you need</span></span>
* <span data-ttu-id="80b8b-116">A Mac with an Internet connection.</span><span class="sxs-lookup"><span data-stu-id="80b8b-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="80b8b-117">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="80b8b-117">An active Azure subscription.</span></span> <span data-ttu-id="80b8b-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="80b8b-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="80b8b-119">Install Python</span><span class="sxs-lookup"><span data-stu-id="80b8b-119">Install Python</span></span>
<span data-ttu-id="80b8b-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span><span class="sxs-lookup"><span data-stu-id="80b8b-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="80b8b-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="80b8b-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="80b8b-122">Install Python and pip by running the following command:</span><span class="sxs-lookup"><span data-stu-id="80b8b-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="80b8b-123">Install the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="80b8b-123">Install the Azure CLI</span></span>
<span data-ttu-id="80b8b-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span><span class="sxs-lookup"><span data-stu-id="80b8b-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="80b8b-125">You work directly from your command line to provision and manage resources.</span><span class="sxs-lookup"><span data-stu-id="80b8b-125">You work directly from your command line to provision and manage resources.</span></span> 

<span data-ttu-id="80b8b-126">To install the latest Azure CLI, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="80b8b-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="80b8b-127">Run the following commands in a terminal window.</span><span class="sxs-lookup"><span data-stu-id="80b8b-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="80b8b-128">It might take five minutes to install the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="80b8b-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="80b8b-129">Verify the installation by running the following command:</span><span class="sxs-lookup"><span data-stu-id="80b8b-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="80b8b-130">You should see the following output if the installation is successful.</span><span class="sxs-lookup"><span data-stu-id="80b8b-130">You should see the following output if the installation is successful.</span></span>

![Output that indicates success](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="80b8b-132">Summary</span><span class="sxs-lookup"><span data-stu-id="80b8b-132">Summary</span></span>
<span data-ttu-id="80b8b-133">You've installed the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="80b8b-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="80b8b-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="80b8b-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80b8b-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="80b8b-135">Next steps</span></span>
<span data-ttu-id="80b8b-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]
<!-- Images and links --></span><span class="sxs-lookup"><span data-stu-id="80b8b-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]
<!-- Images and links --></span></span>

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md

