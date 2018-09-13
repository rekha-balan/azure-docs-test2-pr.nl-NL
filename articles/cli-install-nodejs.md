---
title: Install the Azure CLI 1.0 | Microsoft Docs
description: Install the Azure CLI 1.0 for Mac, Linux, and Windows to start using Azure services
editor: ''
manager: timlt
documentationcenter: ''
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: fd85384d0724d53d21fdeeb0ed24d058205a097a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552318"
---
# <a name="install-the-azure-cli-10"></a><span data-ttu-id="60c9e-103">Install the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="60c9e-103">Install the Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs)
> * [Azure CLI 1.0](cli-install-nodejs.md)
> * [Azure CLI 2.0](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> This topic describes how to install the Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities. You should use the [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.

<span data-ttu-id="60c9e-109">Quickly install the Azure Command-Line Interface (Azure CLI 1.0) to use a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="60c9e-109">Quickly install the Azure Command-Line Interface (Azure CLI 1.0) to use a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="60c9e-110">You have several options to install these cross-platform tools on your computer:</span><span class="sxs-lookup"><span data-stu-id="60c9e-110">You have several options to install these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="60c9e-111">**npm package** - Run npm (the package manager for JavaScript) to install the latest Azure CLI 1.0 package on your Linux distribution or OS.</span><span class="sxs-lookup"><span data-stu-id="60c9e-111">**npm package** - Run npm (the package manager for JavaScript) to install the latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="60c9e-112">Requires node.js and npm on your computer.</span><span class="sxs-lookup"><span data-stu-id="60c9e-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="60c9e-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span><span class="sxs-lookup"><span data-stu-id="60c9e-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="60c9e-114">**Docker container** - Start using the latest CLI in a ready-to-run Docker container.</span><span class="sxs-lookup"><span data-stu-id="60c9e-114">**Docker container** - Start using the latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="60c9e-115">Requires Docker host on your computer.</span><span class="sxs-lookup"><span data-stu-id="60c9e-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="60c9e-116">For more options and background, see the project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="60c9e-116">For more options and background, see the project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="60c9e-117">Once the Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run the **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) to work with your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="60c9e-117">Once the Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run the **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) to work with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="60c9e-118">Option 1: Install an npm package</span><span class="sxs-lookup"><span data-stu-id="60c9e-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="60c9e-119">To install the CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="60c9e-119">To install the CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="60c9e-120">Then, run **npm install** to install the azure-cli package:</span><span class="sxs-lookup"><span data-stu-id="60c9e-120">Then, run **npm install** to install the azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="60c9e-121">On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:</span><span class="sxs-lookup"><span data-stu-id="60c9e-121">On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> If you need to install or update Node.js and npm on your Linux distribution or OS, we recommend that you install the most recent Node.js LTS version (4.x). If you use an older version, you might get installation errors.

<span data-ttu-id="60c9e-124">If you prefer, download the latest Linux [tar file][linux-installer] for the npm package locally.</span><span class="sxs-lookup"><span data-stu-id="60c9e-124">If you prefer, download the latest Linux [tar file][linux-installer] for the npm package locally.</span></span> <span data-ttu-id="60c9e-125">Then, install the downloaded npm package as follows (on Linux distributions you might need to use **sudo**):</span><span class="sxs-lookup"><span data-stu-id="60c9e-125">Then, install the downloaded npm package as follows (on Linux distributions you might need to use **sudo**):</span></span>

```bash
npm install -g <path to downloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="60c9e-126">Option 2: Use an installer</span><span class="sxs-lookup"><span data-stu-id="60c9e-126">Option 2: Use an installer</span></span>
<span data-ttu-id="60c9e-127">If you use a Mac or Windows computer, the following CLI installers are available for download:</span><span class="sxs-lookup"><span data-stu-id="60c9e-127">If you use a Mac or Windows computer, the following CLI installers are available for download:</span></span>

* <span data-ttu-id="60c9e-128">[Mac OS X installer][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="60c9e-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="60c9e-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="60c9e-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> On Windows, you can also download the [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) to install the CLI. This installer gives you the option to install additional Azure SDK and command-line tools after installing the CLI.

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="60c9e-132">Option 3: Use a Docker container</span><span class="sxs-lookup"><span data-stu-id="60c9e-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="60c9e-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run the latest Azure CLI 1.0 in a Docker container.</span><span class="sxs-lookup"><span data-stu-id="60c9e-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run the latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="60c9e-134">Run the following command (on Linux distributions you might need to use **sudo**):</span><span class="sxs-lookup"><span data-stu-id="60c9e-134">Run the following command (on Linux distributions you might need to use **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="60c9e-135">Run Azure CLI 1.0 commands</span><span class="sxs-lookup"><span data-stu-id="60c9e-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="60c9e-136">After the Azure CLI 1.0 is installed, run the **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span><span class="sxs-lookup"><span data-stu-id="60c9e-136">After the Azure CLI 1.0 is installed, run the **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="60c9e-137">For example, to run the help command, type the following:</span><span class="sxs-lookup"><span data-stu-id="60c9e-137">For example, to run the help command, type the following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> On some Linux distributions, you may receive an error similar to `/usr/bin/env: ‘node’: No such file or directory`. This error comes from recent installations of Node.js being installed at /usr/bin/nodejs. To fix it, create a symbolic link to /usr/bin/node by running this command:

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="60c9e-141">To see the version of the Azure CLI 1.0 you installed, type the following:</span><span class="sxs-lookup"><span data-stu-id="60c9e-141">To see the version of the Azure CLI 1.0 you installed, type the following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="60c9e-142">Now you are ready!</span><span class="sxs-lookup"><span data-stu-id="60c9e-142">Now you are ready!</span></span> <span data-ttu-id="60c9e-143">To access all the CLI commands to work with your own resources, [connect to your Azure subscription from the Azure CLI](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="60c9e-143">To access all the CLI commands to work with your own resources, [connect to your Azure subscription from the Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> When you first use Azure CLI, you see a message asking if you want to allow Microsoft to collect usage information. Participation is voluntary. If you choose to participate, you can stop at any time by running `azure telemetry --disable`. To enable participation at any time, run `azure telemetry --enable`.

## <a name="update-the-cli"></a><span data-ttu-id="60c9e-148">Update the CLI</span><span class="sxs-lookup"><span data-stu-id="60c9e-148">Update the CLI</span></span>
<span data-ttu-id="60c9e-149">Microsoft frequently releases updated versions of the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="60c9e-149">Microsoft frequently releases updated versions of the Azure CLI.</span></span> <span data-ttu-id="60c9e-150">Reinstall the CLI using the installer for your operating system, or run the latest Docker container.</span><span class="sxs-lookup"><span data-stu-id="60c9e-150">Reinstall the CLI using the installer for your operating system, or run the latest Docker container.</span></span> <span data-ttu-id="60c9e-151">Or, if you have the latest Node.js and npm installed, update by typing the following (on Linux distributions you might need to use **sudo**).</span><span class="sxs-lookup"><span data-stu-id="60c9e-151">Or, if you have the latest Node.js and npm installed, update by typing the following (on Linux distributions you might need to use **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="60c9e-152">Enable tab completion</span><span class="sxs-lookup"><span data-stu-id="60c9e-152">Enable tab completion</span></span>
<span data-ttu-id="60c9e-153">Tab completion of CLI commands is supported for Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="60c9e-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="60c9e-154">To enable it in zsh, run:</span><span class="sxs-lookup"><span data-stu-id="60c9e-154">To enable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="60c9e-155">To enable it in bash, run:</span><span class="sxs-lookup"><span data-stu-id="60c9e-155">To enable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="60c9e-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="60c9e-156">Next steps</span></span>
* <span data-ttu-id="60c9e-157">[Connect from the CLI to your Azure subscription](xplat-cli-connect.md) to create and manage Azure resources.</span><span class="sxs-lookup"><span data-stu-id="60c9e-157">[Connect from the CLI to your Azure subscription](xplat-cli-connect.md) to create and manage Azure resources.</span></span>
* <span data-ttu-id="60c9e-158">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="60c9e-158">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="60c9e-159">If you have questions about using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="60c9e-159">If you have questions about using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
