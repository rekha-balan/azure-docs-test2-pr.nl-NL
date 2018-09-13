---
title: Use root privileges on Linux virtual machines | Microsoft Docs
description: Learn how to use root privileges on a Linux virtual machine in Azure.
services: virtual-machines-linux
documentationcenter: ''
author: szarkos
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: ea8d4b0915d647fd1fccd5fd541838fcc941934c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563082"
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="80c6c-103">Using root privileges on Linux virtual machines in Azure</span><span class="sxs-lookup"><span data-stu-id="80c6c-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="80c6c-104">By default, the `root` user is disabled on Linux virtual machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="80c6c-104">By default, the `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="80c6c-105">Users can run commands with elevated privileges by using the `sudo` command.</span><span class="sxs-lookup"><span data-stu-id="80c6c-105">Users can run commands with elevated privileges by using the `sudo` command.</span></span> <span data-ttu-id="80c6c-106">However, the experience may vary depending on how the system was provisioned.</span><span class="sxs-lookup"><span data-stu-id="80c6c-106">However, the experience may vary depending on how the system was provisioned.</span></span>

1. <span data-ttu-id="80c6c-107">**SSH key and password OR password only** - the virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span><span class="sxs-lookup"><span data-stu-id="80c6c-107">**SSH key and password OR password only** - the virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="80c6c-108">In this case `sudo` will prompt for the user's password before executing the command.</span><span class="sxs-lookup"><span data-stu-id="80c6c-108">In this case `sudo` will prompt for the user's password before executing the command.</span></span>
2. <span data-ttu-id="80c6c-109">**SSH key only** - the virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span><span class="sxs-lookup"><span data-stu-id="80c6c-109">**SSH key only** - the virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="80c6c-110">In this case `sudo` **will not** prompt for the user's password before executing the command.</span><span class="sxs-lookup"><span data-stu-id="80c6c-110">In this case `sudo` **will not** prompt for the user's password before executing the command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="80c6c-111">SSH Key and Password, or Password Only</span><span class="sxs-lookup"><span data-stu-id="80c6c-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="80c6c-112">Log into the Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span><span class="sxs-lookup"><span data-stu-id="80c6c-112">Log into the Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="80c6c-113">In this case the user will be prompted for a password.</span><span class="sxs-lookup"><span data-stu-id="80c6c-113">In this case the user will be prompted for a password.</span></span> <span data-ttu-id="80c6c-114">After entering the password `sudo` will run the command with `root` privileges.</span><span class="sxs-lookup"><span data-stu-id="80c6c-114">After entering the password `sudo` will run the command with `root` privileges.</span></span>

<span data-ttu-id="80c6c-115">You can also enable passwordless sudo by editing the `/etc/sudoers.d/waagent` file, for example:</span><span class="sxs-lookup"><span data-stu-id="80c6c-115">You can also enable passwordless sudo by editing the `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="80c6c-116">This change will allow for passwordless sudo by the user "azureuser".</span><span class="sxs-lookup"><span data-stu-id="80c6c-116">This change will allow for passwordless sudo by the user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="80c6c-117">SSH Key Only</span><span class="sxs-lookup"><span data-stu-id="80c6c-117">SSH Key Only</span></span>
<span data-ttu-id="80c6c-118">Log into the Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span><span class="sxs-lookup"><span data-stu-id="80c6c-118">Log into the Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="80c6c-119">In this case the user will **not** be prompted for a password.</span><span class="sxs-lookup"><span data-stu-id="80c6c-119">In this case the user will **not** be prompted for a password.</span></span> <span data-ttu-id="80c6c-120">After pressing `<enter>`, `sudo` will run the command with `root` privileges.</span><span class="sxs-lookup"><span data-stu-id="80c6c-120">After pressing `<enter>`, `sudo` will run the command with `root` privileges.</span></span>

