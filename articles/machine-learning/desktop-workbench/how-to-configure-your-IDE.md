---
title: How to configure Azure Machine Learning Workbench to work with an IDE?  | Microsoft Docs
description: A guide to configuring Azure Machine Learning Workbench to work with your IDE.
services: machine-learning
author: svankam
ms.author: svankam
manager: mwinkle
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 02/01/2018
ms.openlocfilehash: 18692fe631a7e1349ead6bc68a87934e6d030913
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857738"
---
# <a name="how-to-configure-azure-machine-learning-workbench-to-work-with-an-ide"></a><span data-ttu-id="f3798-104">How to configure Azure Machine Learning Workbench to work with an IDE</span><span class="sxs-lookup"><span data-stu-id="f3798-104">How to configure Azure Machine Learning Workbench to work with an IDE</span></span> 

<span data-ttu-id="f3798-105">Azure Machine Learning Workbench can be configured to work with popular Python IDEs (Integrated Development Environment).</span><span class="sxs-lookup"><span data-stu-id="f3798-105">Azure Machine Learning Workbench can be configured to work with popular Python IDEs (Integrated Development Environment).</span></span> <span data-ttu-id="f3798-106">It enables a smooth data science development experience moving between data preparation, code authoring, run tracking and operationalization.</span><span class="sxs-lookup"><span data-stu-id="f3798-106">It enables a smooth data science development experience moving between data preparation, code authoring, run tracking and operationalization.</span></span> <span data-ttu-id="f3798-107">Currently the supported IDEs are:</span><span class="sxs-lookup"><span data-stu-id="f3798-107">Currently the supported IDEs are:</span></span>
- <span data-ttu-id="f3798-108">Microsoft Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f3798-108">Microsoft Visual Studio Code</span></span> 
- <span data-ttu-id="f3798-109">JetBrain PyCharm</span><span class="sxs-lookup"><span data-stu-id="f3798-109">JetBrain PyCharm</span></span> 

## <a name="configure-workbench"></a><span data-ttu-id="f3798-110">Configure workbench</span><span class="sxs-lookup"><span data-stu-id="f3798-110">Configure workbench</span></span>
1. <span data-ttu-id="f3798-111">Click on the **File** menu in the top left corner of the app.</span><span class="sxs-lookup"><span data-stu-id="f3798-111">Click on the **File** menu in the top left corner of the app.</span></span> 
2. <span data-ttu-id="f3798-112">Select the **Configure Project IDE** option from the flyout</span><span class="sxs-lookup"><span data-stu-id="f3798-112">Select the **Configure Project IDE** option from the flyout</span></span> 
3. <span data-ttu-id="f3798-113">Type in `VS Code` or `PyCharm` in the **Name** field (the name is arbitrary)</span><span class="sxs-lookup"><span data-stu-id="f3798-113">Type in `VS Code` or `PyCharm` in the **Name** field (the name is arbitrary)</span></span>
4. <span data-ttu-id="f3798-114">Enter the location to the IDE executable (complete with the executable name and extension) in **Execution Path**</span><span class="sxs-lookup"><span data-stu-id="f3798-114">Enter the location to the IDE executable (complete with the executable name and extension) in **Execution Path**</span></span>

### <a name="default-install-path-for-visual-studio-code"></a><span data-ttu-id="f3798-115">Default install path for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f3798-115">Default install path for Visual Studio Code</span></span>  

* <span data-ttu-id="f3798-116">Windows 32-bit - `C:\Program Files (x86)\Microsoft VS Code\Code.exe`</span><span class="sxs-lookup"><span data-stu-id="f3798-116">Windows 32-bit - `C:\Program Files (x86)\Microsoft VS Code\Code.exe`</span></span>
* <span data-ttu-id="f3798-117">Windows 64-bit - `C:\Program Files\Microsoft VS Code\Code.exe`</span><span class="sxs-lookup"><span data-stu-id="f3798-117">Windows 64-bit - `C:\Program Files\Microsoft VS Code\Code.exe`</span></span>
* <span data-ttu-id="f3798-118">macOS - select the .app path, for example `/Applications/Visual Studio Code.app`, and the app appends the rest of the path for you.</span><span class="sxs-lookup"><span data-stu-id="f3798-118">macOS - select the .app path, for example `/Applications/Visual Studio Code.app`, and the app appends the rest of the path for you.</span></span> <span data-ttu-id="f3798-119">The full path to the executable by default is `/Applications/Visual Studio Code.app/Contents/Resources/app/bin/code`.</span><span class="sxs-lookup"><span data-stu-id="f3798-119">The full path to the executable by default is `/Applications/Visual Studio Code.app/Contents/Resources/app/bin/code`.</span></span> <span data-ttu-id="f3798-120">If you have executed the `Shell Command: Install 'code' command in PATH` command in VS Code, then you can also reference the VS Code script at `/usr/local/bin/code`</span><span class="sxs-lookup"><span data-stu-id="f3798-120">If you have executed the `Shell Command: Install 'code' command in PATH` command in VS Code, then you can also reference the VS Code script at `/usr/local/bin/code`</span></span>

### <a name="default-install-path-for-pycharm"></a><span data-ttu-id="f3798-121">Default install path for PyCharm</span><span class="sxs-lookup"><span data-stu-id="f3798-121">Default install path for PyCharm</span></span> 

* <span data-ttu-id="f3798-122">Windows 32-bit - `C:\Program Files (x86)\JetBrains\PyCharm Community Edition 2017.2.1\bin\pycharm.exe`.</span><span class="sxs-lookup"><span data-stu-id="f3798-122">Windows 32-bit - `C:\Program Files (x86)\JetBrains\PyCharm Community Edition 2017.2.1\bin\pycharm.exe`.</span></span> 
* <span data-ttu-id="f3798-123">Windows 64-bit - `C:\Program Files\JetBrains\PyCharm Community Edition 2017.2.1\bin\pycharm64.exe`.</span><span class="sxs-lookup"><span data-stu-id="f3798-123">Windows 64-bit - `C:\Program Files\JetBrains\PyCharm Community Edition 2017.2.1\bin\pycharm64.exe`.</span></span>
* <span data-ttu-id="f3798-124">macOS - select the .app path, for example “/Applications/PyCharm CE.app”, and the app appends the rest of the path for you.</span><span class="sxs-lookup"><span data-stu-id="f3798-124">macOS - select the .app path, for example “/Applications/PyCharm CE.app”, and the app appends the rest of the path for you.</span></span> <span data-ttu-id="f3798-125">The full path to the executable by default is `/Applications/PyCharm CE.app/Contents/MacOS/pycharm`.</span><span class="sxs-lookup"><span data-stu-id="f3798-125">The full path to the executable by default is `/Applications/PyCharm CE.app/Contents/MacOS/pycharm`.</span></span> <span data-ttu-id="f3798-126">You may also find PyCharm at the bin folder, `/usr/local/bin/charm`</span><span class="sxs-lookup"><span data-stu-id="f3798-126">You may also find PyCharm at the bin folder, `/usr/local/bin/charm`</span></span>

## <a name="open-project-in-ide"></a><span data-ttu-id="f3798-127">Open project in IDE</span><span class="sxs-lookup"><span data-stu-id="f3798-127">Open project in IDE</span></span> 
<span data-ttu-id="f3798-128">Once the configuration is complete, you can open an Azure Machine Learning project by opening the **File** menu in Azure Machine Learning Workbench, then click **Open Project (<IDE_Name>)**.</span><span class="sxs-lookup"><span data-stu-id="f3798-128">Once the configuration is complete, you can open an Azure Machine Learning project by opening the **File** menu in Azure Machine Learning Workbench, then click **Open Project (<IDE_Name>)**.</span></span> <span data-ttu-id="f3798-129">This action opens the current active project in the configured IDE.</span><span class="sxs-lookup"><span data-stu-id="f3798-129">This action opens the current active project in the configured IDE.</span></span> <span data-ttu-id="f3798-130">_Note: If you are not in a project, the **Open Project (<IDE_Name>)** will be disabled._</span><span class="sxs-lookup"><span data-stu-id="f3798-130">_Note: If you are not in a project, the **Open Project (<IDE_Name>)** will be disabled._</span></span>

## <a name="configuring-the-integrated-terminal-in-visual-studio-code"></a><span data-ttu-id="f3798-131">Configuring the integrated terminal in Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f3798-131">Configuring the integrated terminal in Visual Studio Code</span></span>

### <a name="windows"></a><span data-ttu-id="f3798-132">Windows</span><span class="sxs-lookup"><span data-stu-id="f3798-132">Windows</span></span> 
<span data-ttu-id="f3798-133">We have overridden the default shell to be cmd instead of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3798-133">We have overridden the default shell to be cmd instead of PowerShell.</span></span> <span data-ttu-id="f3798-134">On clicking on **Open Project (<IDE_Name>)**, you see a prompt:</span><span class="sxs-lookup"><span data-stu-id="f3798-134">On clicking on **Open Project (<IDE_Name>)**, you see a prompt:</span></span> 

<span data-ttu-id="f3798-135">_Do you allow shell: `C:\windows\System32\cmd.exe` (defined as a workspace setting) to be launched in the terminal?_</span><span class="sxs-lookup"><span data-stu-id="f3798-135">_Do you allow shell: `C:\windows\System32\cmd.exe` (defined as a workspace setting) to be launched in the terminal?_</span></span>

<span data-ttu-id="f3798-136">Answer `yes` to allow configuring the shell to work seamlessly with Azure ML Workbench command-line interface.</span><span class="sxs-lookup"><span data-stu-id="f3798-136">Answer `yes` to allow configuring the shell to work seamlessly with Azure ML Workbench command-line interface.</span></span>

### <a name="mac"></a><span data-ttu-id="f3798-137">Mac</span><span class="sxs-lookup"><span data-stu-id="f3798-137">Mac</span></span>
<span data-ttu-id="f3798-138">To run an `az` command using Visual Studio Code's integrated terminal on Mac, you need to manually set the `PATH` to be the same value as `PATH` in the project's `.vscode/settings.json` file under the key `terminal.integrated.env.osx`.</span><span class="sxs-lookup"><span data-stu-id="f3798-138">To run an `az` command using Visual Studio Code's integrated terminal on Mac, you need to manually set the `PATH` to be the same value as `PATH` in the project's `.vscode/settings.json` file under the key `terminal.integrated.env.osx`.</span></span> <span data-ttu-id="f3798-139">You can do so by running the following command in the terminal: `PATH=<PATH in .vscode/settings>`</span><span class="sxs-lookup"><span data-stu-id="f3798-139">You can do so by running the following command in the terminal: `PATH=<PATH in .vscode/settings>`</span></span>
