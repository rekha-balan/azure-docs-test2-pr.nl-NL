---
title: 'Connect Intel Edison (Node) to Azure IoT - Lesson 2: Azure tools (Ubuntu) | Microsoft Docs'
description: Install Python and Azure command-line interface (Azure CLI) on Ubuntu.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: azure cli, iot cloud service, arduino cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 6dcb34bf-54a3-4af0-ba89-95d5cfafceff
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b65a7fd318869eaa339e592e272ec6269a8c6802
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549996"
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="8300d-104">Get Azure tools (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="8300d-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [Windows 7 and later][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a><span data-ttu-id="8300d-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="8300d-108">What you will do</span></span>
<span data-ttu-id="8300d-109">Install the Azure command-line interface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="8300d-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="8300d-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="8300d-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8300d-111">What you will learn</span><span class="sxs-lookup"><span data-stu-id="8300d-111">What you will learn</span></span>
<span data-ttu-id="8300d-112">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="8300d-112">In this article, you will learn:</span></span>
* <span data-ttu-id="8300d-113">How to install the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8300d-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="8300d-114">How to add an IoT subgroup of the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8300d-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8300d-115">What you need</span><span class="sxs-lookup"><span data-stu-id="8300d-115">What you need</span></span>
* <span data-ttu-id="8300d-116">An Ubuntu computer with an Internet connection.</span><span class="sxs-lookup"><span data-stu-id="8300d-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="8300d-117">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="8300d-117">An active Azure subscription.</span></span> <span data-ttu-id="8300d-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="8300d-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="8300d-119">Install the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8300d-119">Install the Azure CLI</span></span>
<span data-ttu-id="8300d-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span><span class="sxs-lookup"><span data-stu-id="8300d-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="8300d-121">To install the latest Azure CLI, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="8300d-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="8300d-122">Run the following commands in a terminal window.</span><span class="sxs-lookup"><span data-stu-id="8300d-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="8300d-123">It might take five minutes to install the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8300d-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="8300d-124">Verify the installation by running the following command:</span><span class="sxs-lookup"><span data-stu-id="8300d-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="8300d-125">You should see the following output if the installation is successful.</span><span class="sxs-lookup"><span data-stu-id="8300d-125">You should see the following output if the installation is successful.</span></span>

![Output that indicates success](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="8300d-127">Summary</span><span class="sxs-lookup"><span data-stu-id="8300d-127">Summary</span></span>
<span data-ttu-id="8300d-128">You've installed the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8300d-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="8300d-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8300d-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8300d-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="8300d-130">Next steps</span></span>
<span data-ttu-id="8300d-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="8300d-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md

