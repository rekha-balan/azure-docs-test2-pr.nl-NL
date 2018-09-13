---
title: Known Issues and Troubleshooting Guide | Microsoft Docs
description: List of known issues and a guide to help troubleshoot
services: machine-learning
author: svankam
ms.author: svankam
manager: mwinkle
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 01/12/2018
ms.openlocfilehash: dc57509475634b6a8038179dbb205533c3ea9d99
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871725"
---
# <a name="azure-machine-learning-workbench---known-issues-and-troubleshooting-guide"></a><span data-ttu-id="bffb1-103">Azure Machine Learning Workbench - Known Issues And Troubleshooting Guide</span><span class="sxs-lookup"><span data-stu-id="bffb1-103">Azure Machine Learning Workbench - Known Issues And Troubleshooting Guide</span></span> 
<span data-ttu-id="bffb1-104">This article helps you find and correct errors or failures encountered as a part of using the Azure Machine Learning Workbench application.</span><span class="sxs-lookup"><span data-stu-id="bffb1-104">This article helps you find and correct errors or failures encountered as a part of using the Azure Machine Learning Workbench application.</span></span> 

## <a name="find-the-workbench-build-number"></a><span data-ttu-id="bffb1-105">Find the Workbench build number</span><span class="sxs-lookup"><span data-stu-id="bffb1-105">Find the Workbench build number</span></span>
<span data-ttu-id="bffb1-106">When communicating with the support team, it is important to include the build number of the Workbench app.</span><span class="sxs-lookup"><span data-stu-id="bffb1-106">When communicating with the support team, it is important to include the build number of the Workbench app.</span></span> <span data-ttu-id="bffb1-107">On Windows, you can find out the build number by clicking on the **Help** menu and choose **About Azure ML Workbench**.</span><span class="sxs-lookup"><span data-stu-id="bffb1-107">On Windows, you can find out the build number by clicking on the **Help** menu and choose **About Azure ML Workbench**.</span></span> <span data-ttu-id="bffb1-108">On macOS, you can click on the **Azure ML Workbench** menu and choose **About Azure ML Workbench**.</span><span class="sxs-lookup"><span data-stu-id="bffb1-108">On macOS, you can click on the **Azure ML Workbench** menu and choose **About Azure ML Workbench**.</span></span>

## <a name="machine-learning-msdn-forum"></a><span data-ttu-id="bffb1-109">Machine Learning MSDN Forum</span><span class="sxs-lookup"><span data-stu-id="bffb1-109">Machine Learning MSDN Forum</span></span>
<span data-ttu-id="bffb1-110">We have an MSDN Forum that you can post questions.</span><span class="sxs-lookup"><span data-stu-id="bffb1-110">We have an MSDN Forum that you can post questions.</span></span> <span data-ttu-id="bffb1-111">The product team monitors the forum actively.</span><span class="sxs-lookup"><span data-stu-id="bffb1-111">The product team monitors the forum actively.</span></span> <span data-ttu-id="bffb1-112">The forum URL is [https://aka.ms/azureml-forum](https://aka.ms/azureml-forum).</span><span class="sxs-lookup"><span data-stu-id="bffb1-112">The forum URL is [https://aka.ms/azureml-forum](https://aka.ms/azureml-forum).</span></span> 

## <a name="gather-diagnostics-information"></a><span data-ttu-id="bffb1-113">Gather diagnostics information</span><span class="sxs-lookup"><span data-stu-id="bffb1-113">Gather diagnostics information</span></span>
<span data-ttu-id="bffb1-114">Sometimes it can be helpful if you can provide diagnostic information when asking for help.</span><span class="sxs-lookup"><span data-stu-id="bffb1-114">Sometimes it can be helpful if you can provide diagnostic information when asking for help.</span></span> <span data-ttu-id="bffb1-115">Here is where the log files live:</span><span class="sxs-lookup"><span data-stu-id="bffb1-115">Here is where the log files live:</span></span>

### <a name="installer-log"></a><span data-ttu-id="bffb1-116">Installer log</span><span class="sxs-lookup"><span data-stu-id="bffb1-116">Installer log</span></span>
<span data-ttu-id="bffb1-117">If you run into issue during installation, the installer log files are here:</span><span class="sxs-lookup"><span data-stu-id="bffb1-117">If you run into issue during installation, the installer log files are here:</span></span>

```
# Windows:
%TEMP%\amlinstaller\logs\*

# macOS:
/tmp/amlinstaller/logs/*
```
<span data-ttu-id="bffb1-118">You can zip up the contents of these directories and send it to us for diagnostics.</span><span class="sxs-lookup"><span data-stu-id="bffb1-118">You can zip up the contents of these directories and send it to us for diagnostics.</span></span>

### <a name="workbench-desktop-app-log"></a><span data-ttu-id="bffb1-119">Workbench desktop app log</span><span class="sxs-lookup"><span data-stu-id="bffb1-119">Workbench desktop app log</span></span>
<span data-ttu-id="bffb1-120">If you have trouble logging in, or if the Workbench desktop crashes, you can find log files here:</span><span class="sxs-lookup"><span data-stu-id="bffb1-120">If you have trouble logging in, or if the Workbench desktop crashes, you can find log files here:</span></span>
```
# Windows
%APPDATA%\AmlWorkbench

# macOS
~/Library/Application Support/AmlWorkbench
``` 
<span data-ttu-id="bffb1-121">You can zip up the contents of these directories and send it to us for diagnostics.</span><span class="sxs-lookup"><span data-stu-id="bffb1-121">You can zip up the contents of these directories and send it to us for diagnostics.</span></span>

### <a name="experiment-execution-log"></a><span data-ttu-id="bffb1-122">Experiment execution log</span><span class="sxs-lookup"><span data-stu-id="bffb1-122">Experiment execution log</span></span>
<span data-ttu-id="bffb1-123">If a particular script fails during submission from the desktop app, try to resubmit it through CLI using `az ml experiment submit` command.</span><span class="sxs-lookup"><span data-stu-id="bffb1-123">If a particular script fails during submission from the desktop app, try to resubmit it through CLI using `az ml experiment submit` command.</span></span> <span data-ttu-id="bffb1-124">This should give you full error message in JSON format, and most importantly it contains an **operation ID** value.</span><span class="sxs-lookup"><span data-stu-id="bffb1-124">This should give you full error message in JSON format, and most importantly it contains an **operation ID** value.</span></span> <span data-ttu-id="bffb1-125">Send us the JSON file including the **operation ID** and we can help diagnose.</span><span class="sxs-lookup"><span data-stu-id="bffb1-125">Send us the JSON file including the **operation ID** and we can help diagnose.</span></span> 

<span data-ttu-id="bffb1-126">If a particular script succeeds in submission but fails in execution, it should print out the **Run ID** to identify that particular run.</span><span class="sxs-lookup"><span data-stu-id="bffb1-126">If a particular script succeeds in submission but fails in execution, it should print out the **Run ID** to identify that particular run.</span></span> <span data-ttu-id="bffb1-127">You can package up the relevant log files using the following command:</span><span class="sxs-lookup"><span data-stu-id="bffb1-127">You can package up the relevant log files using the following command:</span></span>

```azurecli
# Create a ZIP file that contains all the diagnostics information
$ az ml experiment diagnostics -r <run_id> -t <target_name>
```

<span data-ttu-id="bffb1-128">The `az ml experiment diagnostics` command generates a `diagnostics.zip` file in the project root folder.</span><span class="sxs-lookup"><span data-stu-id="bffb1-128">The `az ml experiment diagnostics` command generates a `diagnostics.zip` file in the project root folder.</span></span> <span data-ttu-id="bffb1-129">The ZIP package contains the entire project folder in the state at the time it was executed, plus logging information.</span><span class="sxs-lookup"><span data-stu-id="bffb1-129">The ZIP package contains the entire project folder in the state at the time it was executed, plus logging information.</span></span> <span data-ttu-id="bffb1-130">Be sure to remove any sensitive information you don't want to include before sending us the diagnostics file.</span><span class="sxs-lookup"><span data-stu-id="bffb1-130">Be sure to remove any sensitive information you don't want to include before sending us the diagnostics file.</span></span>

## <a name="send-us-a-frown-or-a-smile"></a><span data-ttu-id="bffb1-131">Send us a frown (or a smile)</span><span class="sxs-lookup"><span data-stu-id="bffb1-131">Send us a frown (or a smile)</span></span>

<span data-ttu-id="bffb1-132">When you are working in Azure ML Workbench, you can also send us a frown (or a smile) by clicking on the smiley face icon at the lower left corner of the application shell.</span><span class="sxs-lookup"><span data-stu-id="bffb1-132">When you are working in Azure ML Workbench, you can also send us a frown (or a smile) by clicking on the smiley face icon at the lower left corner of the application shell.</span></span> <span data-ttu-id="bffb1-133">You can optionally choose to include your email address (so we can get back to you), and/or a screenshot of the current state.</span><span class="sxs-lookup"><span data-stu-id="bffb1-133">You can optionally choose to include your email address (so we can get back to you), and/or a screenshot of the current state.</span></span> 

## <a name="known-service-limits"></a><span data-ttu-id="bffb1-134">Known service limits</span><span class="sxs-lookup"><span data-stu-id="bffb1-134">Known service limits</span></span>
- <span data-ttu-id="bffb1-135">Max allowed project folder size: 25 MB.</span><span class="sxs-lookup"><span data-stu-id="bffb1-135">Max allowed project folder size: 25 MB.</span></span>
    >[!NOTE]
    ><span data-ttu-id="bffb1-136">This limit doesn't apply to `.git`, `docs` and `outputs` folders.</span><span class="sxs-lookup"><span data-stu-id="bffb1-136">This limit doesn't apply to `.git`, `docs` and `outputs` folders.</span></span> <span data-ttu-id="bffb1-137">These folder names are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="bffb1-137">These folder names are case-sensitive.</span></span> <span data-ttu-id="bffb1-138">If you are working with large files, refer to [Persisting Changes and Deal with Large Files](../desktop-workbench/how-to-read-write-files.md).</span><span class="sxs-lookup"><span data-stu-id="bffb1-138">If you are working with large files, refer to [Persisting Changes and Deal with Large Files](../desktop-workbench/how-to-read-write-files.md).</span></span>

- <span data-ttu-id="bffb1-139">Max allowed experiment execution time: seven days</span><span class="sxs-lookup"><span data-stu-id="bffb1-139">Max allowed experiment execution time: seven days</span></span>

- <span data-ttu-id="bffb1-140">Max size of tracked file in `outputs` folder after a run: 512 MB</span><span class="sxs-lookup"><span data-stu-id="bffb1-140">Max size of tracked file in `outputs` folder after a run: 512 MB</span></span>
  - <span data-ttu-id="bffb1-141">This means if your script produces a file larger than 512 MB in the outputs folder, it is not collected there.</span><span class="sxs-lookup"><span data-stu-id="bffb1-141">This means if your script produces a file larger than 512 MB in the outputs folder, it is not collected there.</span></span> <span data-ttu-id="bffb1-142">If you are working with large files, refer to [Persisting Changes and Deal with Large Files](../desktop-workbench/how-to-read-write-files.md).</span><span class="sxs-lookup"><span data-stu-id="bffb1-142">If you are working with large files, refer to [Persisting Changes and Deal with Large Files](../desktop-workbench/how-to-read-write-files.md).</span></span>

- <span data-ttu-id="bffb1-143">SSH keys are not supported when connecting to a remote machine or Spark cluster over SSH.</span><span class="sxs-lookup"><span data-stu-id="bffb1-143">SSH keys are not supported when connecting to a remote machine or Spark cluster over SSH.</span></span> <span data-ttu-id="bffb1-144">Only username/password mode is currently supported.</span><span class="sxs-lookup"><span data-stu-id="bffb1-144">Only username/password mode is currently supported.</span></span>

- <span data-ttu-id="bffb1-145">When using HDInsight cluster as compute target, it must use Azure blob as primary storage.</span><span class="sxs-lookup"><span data-stu-id="bffb1-145">When using HDInsight cluster as compute target, it must use Azure blob as primary storage.</span></span> <span data-ttu-id="bffb1-146">Using Azure Data Lake Storage is not supported.</span><span class="sxs-lookup"><span data-stu-id="bffb1-146">Using Azure Data Lake Storage is not supported.</span></span>

- <span data-ttu-id="bffb1-147">Text clustering transforms are not supported on Mac.</span><span class="sxs-lookup"><span data-stu-id="bffb1-147">Text clustering transforms are not supported on Mac.</span></span>

- <span data-ttu-id="bffb1-148">RevoScalePy library is only supported on Windows and Linux (in Docker containers).</span><span class="sxs-lookup"><span data-stu-id="bffb1-148">RevoScalePy library is only supported on Windows and Linux (in Docker containers).</span></span> <span data-ttu-id="bffb1-149">It is not supported on macOS.</span><span class="sxs-lookup"><span data-stu-id="bffb1-149">It is not supported on macOS.</span></span>

- <span data-ttu-id="bffb1-150">Jupyter Notebooks have a max size limit of 5 MB when opening them from the Workbench app.</span><span class="sxs-lookup"><span data-stu-id="bffb1-150">Jupyter Notebooks have a max size limit of 5 MB when opening them from the Workbench app.</span></span> <span data-ttu-id="bffb1-151">You can open large notebooks from CLI using 'az ml notebook start' command, and clean cell outputs to reduce the file size.</span><span class="sxs-lookup"><span data-stu-id="bffb1-151">You can open large notebooks from CLI using 'az ml notebook start' command, and clean cell outputs to reduce the file size.</span></span>

## <a name="cant-update-workbench"></a><span data-ttu-id="bffb1-152">Can't update Workbench</span><span class="sxs-lookup"><span data-stu-id="bffb1-152">Can't update Workbench</span></span>
<span data-ttu-id="bffb1-153">When a new update is available, the Workbench app homepage displays a message informing you about the new update.</span><span class="sxs-lookup"><span data-stu-id="bffb1-153">When a new update is available, the Workbench app homepage displays a message informing you about the new update.</span></span> <span data-ttu-id="bffb1-154">You should see an update badge appearing on the lower left corner of the app on the bell icon.</span><span class="sxs-lookup"><span data-stu-id="bffb1-154">You should see an update badge appearing on the lower left corner of the app on the bell icon.</span></span> <span data-ttu-id="bffb1-155">Click on the badge and follow the installer wizard to install the update.</span><span class="sxs-lookup"><span data-stu-id="bffb1-155">Click on the badge and follow the installer wizard to install the update.</span></span> 

![update image](./media/known-issues-and-troubleshooting-guide/update.png)

<span data-ttu-id="bffb1-157">If you don't see the notification, try to restart the app.</span><span class="sxs-lookup"><span data-stu-id="bffb1-157">If you don't see the notification, try to restart the app.</span></span> <span data-ttu-id="bffb1-158">If you still don't see the update notification after restart, there might be a few causes.</span><span class="sxs-lookup"><span data-stu-id="bffb1-158">If you still don't see the update notification after restart, there might be a few causes.</span></span>

### <a name="you-are-launching-workbench-from-a-pinned-shortcut-on-the-task-bar"></a><span data-ttu-id="bffb1-159">You are launching Workbench from a pinned shortcut on the task bar</span><span class="sxs-lookup"><span data-stu-id="bffb1-159">You are launching Workbench from a pinned shortcut on the task bar</span></span>
<span data-ttu-id="bffb1-160">You may have already installed the update.</span><span class="sxs-lookup"><span data-stu-id="bffb1-160">You may have already installed the update.</span></span> <span data-ttu-id="bffb1-161">But your pinned shortcut is still pointing to the old bits on disk.</span><span class="sxs-lookup"><span data-stu-id="bffb1-161">But your pinned shortcut is still pointing to the old bits on disk.</span></span> <span data-ttu-id="bffb1-162">You can verify this by browsing to the `%localappdata%/AmlWorkbench` folder and see if you have latest version installed there, and examine the property of the pinned shortcut to see where it is pointing to.</span><span class="sxs-lookup"><span data-stu-id="bffb1-162">You can verify this by browsing to the `%localappdata%/AmlWorkbench` folder and see if you have latest version installed there, and examine the property of the pinned shortcut to see where it is pointing to.</span></span> <span data-ttu-id="bffb1-163">If verified, simply remove the old shortcut, launch Workbench from Start menu, and optionally create a new pinned shortcut on the task bar.</span><span class="sxs-lookup"><span data-stu-id="bffb1-163">If verified, simply remove the old shortcut, launch Workbench from Start menu, and optionally create a new pinned shortcut on the task bar.</span></span>

### <a name="you-installed-workbench-using-the-install-azure-ml-workbench-link-on-a-windows-dsvm"></a><span data-ttu-id="bffb1-164">You installed Workbench using the "install Azure ML Workbench" link on a Windows DSVM</span><span class="sxs-lookup"><span data-stu-id="bffb1-164">You installed Workbench using the "install Azure ML Workbench" link on a Windows DSVM</span></span>
<span data-ttu-id="bffb1-165">Unfortunately there is no easy fix on this one.</span><span class="sxs-lookup"><span data-stu-id="bffb1-165">Unfortunately there is no easy fix on this one.</span></span> <span data-ttu-id="bffb1-166">You have to perform the following steps to remove the installed bits, and download the latest installer to fresh-install the Workbench:</span><span class="sxs-lookup"><span data-stu-id="bffb1-166">You have to perform the following steps to remove the installed bits, and download the latest installer to fresh-install the Workbench:</span></span> 
   - <span data-ttu-id="bffb1-167">remove the folder `C:\Users\<Username>\AppData\Local\amlworkbench`</span><span class="sxs-lookup"><span data-stu-id="bffb1-167">remove the folder `C:\Users\<Username>\AppData\Local\amlworkbench`</span></span>
   - <span data-ttu-id="bffb1-168">remove script `C:\dsvm\tools\setup\InstallAMLFromLocal.ps1`</span><span class="sxs-lookup"><span data-stu-id="bffb1-168">remove script `C:\dsvm\tools\setup\InstallAMLFromLocal.ps1`</span></span>
   - <span data-ttu-id="bffb1-169">remove desktop shortcut that launches the above script</span><span class="sxs-lookup"><span data-stu-id="bffb1-169">remove desktop shortcut that launches the above script</span></span>
   - <span data-ttu-id="bffb1-170">download the installer https://aka.ms/azureml-wb-msi and reinstall.</span><span class="sxs-lookup"><span data-stu-id="bffb1-170">download the installer https://aka.ms/azureml-wb-msi and reinstall.</span></span>

## <a name="stuck-at-checking-experimentation-account-screen-after-logging-in"></a><span data-ttu-id="bffb1-171">Stuck at "Checking experimentation account" screen after logging in</span><span class="sxs-lookup"><span data-stu-id="bffb1-171">Stuck at "Checking experimentation account" screen after logging in</span></span>
<span data-ttu-id="bffb1-172">After logging in, the Workbench app might get stuck on a blank screen with a message showing "Checking experimentation account" with a spinning wheel.</span><span class="sxs-lookup"><span data-stu-id="bffb1-172">After logging in, the Workbench app might get stuck on a blank screen with a message showing "Checking experimentation account" with a spinning wheel.</span></span> <span data-ttu-id="bffb1-173">To resolve this issue, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="bffb1-173">To resolve this issue, take the following steps:</span></span>
1. <span data-ttu-id="bffb1-174">Shutdown the app</span><span class="sxs-lookup"><span data-stu-id="bffb1-174">Shutdown the app</span></span>
2. <span data-ttu-id="bffb1-175">Delete the following file:</span><span class="sxs-lookup"><span data-stu-id="bffb1-175">Delete the following file:</span></span>
  ```
  # on Windows
  %appdata%\AmlWorkbench\AmlWb.settings

  # on macOS
  ~/Library/Application Support/AmlWorkbench/AmlWb.settings
  ```
3. <span data-ttu-id="bffb1-176">Restart the app.</span><span class="sxs-lookup"><span data-stu-id="bffb1-176">Restart the app.</span></span>

## <a name="cant-delete-experimentation-account"></a><span data-ttu-id="bffb1-177">Can't delete Experimentation Account</span><span class="sxs-lookup"><span data-stu-id="bffb1-177">Can't delete Experimentation Account</span></span>
<span data-ttu-id="bffb1-178">You can use CLI to delete an Experimentation Account, but you must delete the child workspaces and the child projects within those child workspaces first.</span><span class="sxs-lookup"><span data-stu-id="bffb1-178">You can use CLI to delete an Experimentation Account, but you must delete the child workspaces and the child projects within those child workspaces first.</span></span> <span data-ttu-id="bffb1-179">Otherwise, you see the error "Can not delete resource before nested resources are deleted."</span><span class="sxs-lookup"><span data-stu-id="bffb1-179">Otherwise, you see the error "Can not delete resource before nested resources are deleted."</span></span>

```azure-cli
# delete a project
$ az ml project delete -g <resource group name> -a <experimentation account name> -w <workspace name> -n <project name>

# delete a workspace 
$ az ml workspace delete -g <resource group name> -a <experimentation account name> -n <workspace name>

# delete an experimentation account
$ az ml account experimentation delete -g <resource group name> -n <experimentation account name>
```

<span data-ttu-id="bffb1-180">You can also delete the projects and workspaces from within the Workbench app.</span><span class="sxs-lookup"><span data-stu-id="bffb1-180">You can also delete the projects and workspaces from within the Workbench app.</span></span>

## <a name="cant-open-file-if-project-is-in-onedrive"></a><span data-ttu-id="bffb1-181">Can't open file if project is in OneDrive</span><span class="sxs-lookup"><span data-stu-id="bffb1-181">Can't open file if project is in OneDrive</span></span>
<span data-ttu-id="bffb1-182">If you have Windows 10 Fall Creators Update, and your project is created in a local folder mapped to OneDrive, you might find that you cannot open any file in Workbench.</span><span class="sxs-lookup"><span data-stu-id="bffb1-182">If you have Windows 10 Fall Creators Update, and your project is created in a local folder mapped to OneDrive, you might find that you cannot open any file in Workbench.</span></span> <span data-ttu-id="bffb1-183">This is due to a bug introduced by the Fall Creators Update that causes node.js code to fail in a OneDrive folder.</span><span class="sxs-lookup"><span data-stu-id="bffb1-183">This is due to a bug introduced by the Fall Creators Update that causes node.js code to fail in a OneDrive folder.</span></span> <span data-ttu-id="bffb1-184">The bug will be fixed soon by Windows update, but until then, please do not create projects in a OneDrive folder.</span><span class="sxs-lookup"><span data-stu-id="bffb1-184">The bug will be fixed soon by Windows update, but until then, please do not create projects in a OneDrive folder.</span></span>

## <a name="file-name-too-long-on-windows"></a><span data-ttu-id="bffb1-185">File name too long on Windows</span><span class="sxs-lookup"><span data-stu-id="bffb1-185">File name too long on Windows</span></span>
<span data-ttu-id="bffb1-186">If you use Workbench on Windows, you might run into the default maximum 260-character file name length limit, which could surface as a "system cannot find the path specified" error.</span><span class="sxs-lookup"><span data-stu-id="bffb1-186">If you use Workbench on Windows, you might run into the default maximum 260-character file name length limit, which could surface as a "system cannot find the path specified" error.</span></span> <span data-ttu-id="bffb1-187">You can modify a registry key setting to allow much longer file path name.</span><span class="sxs-lookup"><span data-stu-id="bffb1-187">You can modify a registry key setting to allow much longer file path name.</span></span> <span data-ttu-id="bffb1-188">Review [this article](https://msdn.microsoft.com/library/windows/desktop/aa365247%28v=vs.85%29.aspx?#maxpath) for more details on how to set the _MAX_PATH_ registry key.</span><span class="sxs-lookup"><span data-stu-id="bffb1-188">Review [this article](https://msdn.microsoft.com/library/windows/desktop/aa365247%28v=vs.85%29.aspx?#maxpath) for more details on how to set the _MAX_PATH_ registry key.</span></span>

## <a name="interrupt-cli-execution-output"></a><span data-ttu-id="bffb1-189">Interrupt CLI execution output</span><span class="sxs-lookup"><span data-stu-id="bffb1-189">Interrupt CLI execution output</span></span>
<span data-ttu-id="bffb1-190">If you kick off an experimentation run using `az ml experiment submit` or `az ml notebook start` and you'd like to interrupt the output:</span><span class="sxs-lookup"><span data-stu-id="bffb1-190">If you kick off an experimentation run using `az ml experiment submit` or `az ml notebook start` and you'd like to interrupt the output:</span></span> 
- <span data-ttu-id="bffb1-191">On Windows use Ctrl-Break key combination from the keyboard</span><span class="sxs-lookup"><span data-stu-id="bffb1-191">On Windows use Ctrl-Break key combination from the keyboard</span></span>
- <span data-ttu-id="bffb1-192">On macOS, use Ctrl-C.</span><span class="sxs-lookup"><span data-stu-id="bffb1-192">On macOS, use Ctrl-C.</span></span>

<span data-ttu-id="bffb1-193">Please note that this only interrupts the output stream in the CLI window.</span><span class="sxs-lookup"><span data-stu-id="bffb1-193">Please note that this only interrupts the output stream in the CLI window.</span></span> <span data-ttu-id="bffb1-194">It does not actually stop a job that's being executed.</span><span class="sxs-lookup"><span data-stu-id="bffb1-194">It does not actually stop a job that's being executed.</span></span> <span data-ttu-id="bffb1-195">If you want to cancel an ongoing job, use `az ml experiment cancel -r <run_id> -t <target name>` command.</span><span class="sxs-lookup"><span data-stu-id="bffb1-195">If you want to cancel an ongoing job, use `az ml experiment cancel -r <run_id> -t <target name>` command.</span></span>

<span data-ttu-id="bffb1-196">On Windows computers with keyboards that do not have Break key, possible alternatives include Fn-B, Ctrl-Fn-B or Fn+Esc. Consult your hardware vendor's documentation for a specific key combination.</span><span class="sxs-lookup"><span data-stu-id="bffb1-196">On Windows computers with keyboards that do not have Break key, possible alternatives include Fn-B, Ctrl-Fn-B or Fn+Esc. Consult your hardware vendor's documentation for a specific key combination.</span></span>

## <a name="docker-error-read-connection-refused"></a><span data-ttu-id="bffb1-197">Docker error "read: connection refused"</span><span class="sxs-lookup"><span data-stu-id="bffb1-197">Docker error "read: connection refused"</span></span>
<span data-ttu-id="bffb1-198">When executing against a local Docker container, sometimes you might see the following error:</span><span class="sxs-lookup"><span data-stu-id="bffb1-198">When executing against a local Docker container, sometimes you might see the following error:</span></span> 
```
Get https://registry-1.docker.io/v2/: 
dial tcp: 
lookup registry-1.docker.io on [::1]:53: read udp [::1]:49385->[::1]:53: 
read: connection refused
```

<span data-ttu-id="bffb1-199">You can fix it by changing the Docker DNS Server from `automatic` to a fixed value of `8.8.8.8`.</span><span class="sxs-lookup"><span data-stu-id="bffb1-199">You can fix it by changing the Docker DNS Server from `automatic` to a fixed value of `8.8.8.8`.</span></span>

## <a name="remove-vm-execution-error-no-tty-present"></a><span data-ttu-id="bffb1-200">Remove VM execution error "no tty present"</span><span class="sxs-lookup"><span data-stu-id="bffb1-200">Remove VM execution error "no tty present"</span></span>
<span data-ttu-id="bffb1-201">When executing against a Docker container on a remote Linux machine, you might encounter the following error message:</span><span class="sxs-lookup"><span data-stu-id="bffb1-201">When executing against a Docker container on a remote Linux machine, you might encounter the following error message:</span></span>
```
sudo: no tty present and no askpass program specified.
``` 
<span data-ttu-id="bffb1-202">This can happen if you use Azure portal to change the root password of an Ubuntu Linux VM.</span><span class="sxs-lookup"><span data-stu-id="bffb1-202">This can happen if you use Azure portal to change the root password of an Ubuntu Linux VM.</span></span> 

<span data-ttu-id="bffb1-203">Azure Machine Learning Workbench requires password-less sudoers access to run on remote hosts.</span><span class="sxs-lookup"><span data-stu-id="bffb1-203">Azure Machine Learning Workbench requires password-less sudoers access to run on remote hosts.</span></span> <span data-ttu-id="bffb1-204">The simplest way to do that is to use _visudo_ to edit the following file (you may create the file if it does not exist):</span><span class="sxs-lookup"><span data-stu-id="bffb1-204">The simplest way to do that is to use _visudo_ to edit the following file (you may create the file if it does not exist):</span></span>

```
$ sudo visudo -f /etc/sudoers
```

>[!IMPORTANT]
><span data-ttu-id="bffb1-205">It is important to edit the file with _visudo_ and not another command.</span><span class="sxs-lookup"><span data-stu-id="bffb1-205">It is important to edit the file with _visudo_ and not another command.</span></span> <span data-ttu-id="bffb1-206">_visudo_ automatically syntax checks all sudo config files, and failure to produce a syntactically correct sudoers file can lock you out of sudo.</span><span class="sxs-lookup"><span data-stu-id="bffb1-206">_visudo_ automatically syntax checks all sudo config files, and failure to produce a syntactically correct sudoers file can lock you out of sudo.</span></span>

<span data-ttu-id="bffb1-207">Insert the following line at the end of the file:</span><span class="sxs-lookup"><span data-stu-id="bffb1-207">Insert the following line at the end of the file:</span></span>

```
username ALL=(ALL) NOPASSWD:ALL
```

<span data-ttu-id="bffb1-208">Where _username_ is the name of Azure Machine Learning Workbench will use to log in to your remote host.</span><span class="sxs-lookup"><span data-stu-id="bffb1-208">Where _username_ is the name of Azure Machine Learning Workbench will use to log in to your remote host.</span></span>

<span data-ttu-id="bffb1-209">The line must be placed after #includedir "/etc/sudoers.d", otherwise it may be overridden by another rule.</span><span class="sxs-lookup"><span data-stu-id="bffb1-209">The line must be placed after #includedir "/etc/sudoers.d", otherwise it may be overridden by another rule.</span></span>

<span data-ttu-id="bffb1-210">If you have a more complicated sudo configuration, you may want to consult sudo documentation for Ubuntu available here: https://help.ubuntu.com/community/Sudoers</span><span class="sxs-lookup"><span data-stu-id="bffb1-210">If you have a more complicated sudo configuration, you may want to consult sudo documentation for Ubuntu available here: https://help.ubuntu.com/community/Sudoers</span></span>

<span data-ttu-id="bffb1-211">The above error can also happen if you are not using an Ubuntu-based Linux VM in Azure as an execution target.</span><span class="sxs-lookup"><span data-stu-id="bffb1-211">The above error can also happen if you are not using an Ubuntu-based Linux VM in Azure as an execution target.</span></span> <span data-ttu-id="bffb1-212">We only support Ubuntu-based Linux VM for remote execution.</span><span class="sxs-lookup"><span data-stu-id="bffb1-212">We only support Ubuntu-based Linux VM for remote execution.</span></span> 

## <a name="vm-disk-is-full"></a><span data-ttu-id="bffb1-213">VM disk is full</span><span class="sxs-lookup"><span data-stu-id="bffb1-213">VM disk is full</span></span>
<span data-ttu-id="bffb1-214">By default when you create a new Linux VM in Azure, you get a 30-GB disk for the operating system.</span><span class="sxs-lookup"><span data-stu-id="bffb1-214">By default when you create a new Linux VM in Azure, you get a 30-GB disk for the operating system.</span></span> <span data-ttu-id="bffb1-215">Docker engine by default uses the same disk for pulling down images and running containers.</span><span class="sxs-lookup"><span data-stu-id="bffb1-215">Docker engine by default uses the same disk for pulling down images and running containers.</span></span> <span data-ttu-id="bffb1-216">This can fill up the OS disk and you see a "VM Disk is Full" error when it happens.</span><span class="sxs-lookup"><span data-stu-id="bffb1-216">This can fill up the OS disk and you see a "VM Disk is Full" error when it happens.</span></span>

<span data-ttu-id="bffb1-217">A quick fix is to remove all Docker images you no longer use.</span><span class="sxs-lookup"><span data-stu-id="bffb1-217">A quick fix is to remove all Docker images you no longer use.</span></span> <span data-ttu-id="bffb1-218">The following Docker command does just that.</span><span class="sxs-lookup"><span data-stu-id="bffb1-218">The following Docker command does just that.</span></span> <span data-ttu-id="bffb1-219">(Of course you have to SSH into the VM in order to execute the Docker command from a bash shell.)</span><span class="sxs-lookup"><span data-stu-id="bffb1-219">(Of course you have to SSH into the VM in order to execute the Docker command from a bash shell.)</span></span>

```
$ docker system prune -a
```

<span data-ttu-id="bffb1-220">You can also add a data disk and configure Docker engine to use the data disk for storing images.</span><span class="sxs-lookup"><span data-stu-id="bffb1-220">You can also add a data disk and configure Docker engine to use the data disk for storing images.</span></span> <span data-ttu-id="bffb1-221">Here is [how to add a data disk](https://docs.microsoft.com/azure/virtual-machines/linux/add-disk).</span><span class="sxs-lookup"><span data-stu-id="bffb1-221">Here is [how to add a data disk](https://docs.microsoft.com/azure/virtual-machines/linux/add-disk).</span></span> <span data-ttu-id="bffb1-222">You can then [change where Docker stores images](https://forums.docker.com/t/how-do-i-change-the-docker-image-installation-directory/1169).</span><span class="sxs-lookup"><span data-stu-id="bffb1-222">You can then [change where Docker stores images](https://forums.docker.com/t/how-do-i-change-the-docker-image-installation-directory/1169).</span></span>

<span data-ttu-id="bffb1-223">Or, you can expand the OS disk, and you don't have to touch Docker engine configuration.</span><span class="sxs-lookup"><span data-stu-id="bffb1-223">Or, you can expand the OS disk, and you don't have to touch Docker engine configuration.</span></span> <span data-ttu-id="bffb1-224">Here is [how you can expand the OS disk](https://docs.microsoft.com/azure/virtual-machines/linux/expand-disks).</span><span class="sxs-lookup"><span data-stu-id="bffb1-224">Here is [how you can expand the OS disk](https://docs.microsoft.com/azure/virtual-machines/linux/expand-disks).</span></span>

```azure-cli
# Deallocate VM (stopping will not work)
$ az vm deallocate --resource-group myResourceGroup  --name myVM

# Get VM's Disc Name
az disk list --resource-group myResourceGroup --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table

# Update Disc Size using above name
$ az disk update --resource-group myResourceGroup --name myVMdisc --size-gb 250
    
# Start VM    
$ az vm start --resource-group myResourceGroup  --name myVM
```

## <a name="sharing-c-drive-on-windows"></a><span data-ttu-id="bffb1-225">Sharing C drive on Windows</span><span class="sxs-lookup"><span data-stu-id="bffb1-225">Sharing C drive on Windows</span></span>
<span data-ttu-id="bffb1-226">If you are executing in a local Docker container on Windows, setting `sharedVolumes` to `true` in the `docker.compute` file under `aml_config` can improve execution performance.</span><span class="sxs-lookup"><span data-stu-id="bffb1-226">If you are executing in a local Docker container on Windows, setting `sharedVolumes` to `true` in the `docker.compute` file under `aml_config` can improve execution performance.</span></span> <span data-ttu-id="bffb1-227">However, this requires you share C drive in the _Docker for Windows Tool_.</span><span class="sxs-lookup"><span data-stu-id="bffb1-227">However, this requires you share C drive in the _Docker for Windows Tool_.</span></span> <span data-ttu-id="bffb1-228">If you are not able to share C drive, try the following tips:</span><span class="sxs-lookup"><span data-stu-id="bffb1-228">If you are not able to share C drive, try the following tips:</span></span>

* <span data-ttu-id="bffb1-229">Check the sharing on C drive using file explorer</span><span class="sxs-lookup"><span data-stu-id="bffb1-229">Check the sharing on C drive using file explorer</span></span>
* <span data-ttu-id="bffb1-230">Open network adapter settings and uninstall/reinstall "File and Printer Sharing for Microsoft Networks" for vEthernet</span><span class="sxs-lookup"><span data-stu-id="bffb1-230">Open network adapter settings and uninstall/reinstall "File and Printer Sharing for Microsoft Networks" for vEthernet</span></span>
* <span data-ttu-id="bffb1-231">Open docker settings and share C drive from within docker settings</span><span class="sxs-lookup"><span data-stu-id="bffb1-231">Open docker settings and share C drive from within docker settings</span></span>
* <span data-ttu-id="bffb1-232">Changes to the Windows password affect the sharing.</span><span class="sxs-lookup"><span data-stu-id="bffb1-232">Changes to the Windows password affect the sharing.</span></span> <span data-ttu-id="bffb1-233">Open File explorer, reshare the C drive, and enter the new password.</span><span class="sxs-lookup"><span data-stu-id="bffb1-233">Open File explorer, reshare the C drive, and enter the new password.</span></span>
* <span data-ttu-id="bffb1-234">You might also encounter firewall issue when attempting to share your C drive with Docker.</span><span class="sxs-lookup"><span data-stu-id="bffb1-234">You might also encounter firewall issue when attempting to share your C drive with Docker.</span></span> <span data-ttu-id="bffb1-235">This [Stack Overflow post](http://stackoverflow.com/questions/42203488/settings-to-windows-firewall-to-allow-docker-for-windows-to-share-drive/43904051) can be helpful.</span><span class="sxs-lookup"><span data-stu-id="bffb1-235">This [Stack Overflow post](http://stackoverflow.com/questions/42203488/settings-to-windows-firewall-to-allow-docker-for-windows-to-share-drive/43904051) can be helpful.</span></span>
* <span data-ttu-id="bffb1-236">When sharing C drive using domain credentials, the sharing might stop working on networks where the domain controller is not reachable (for example, home network, public wifi etc.).</span><span class="sxs-lookup"><span data-stu-id="bffb1-236">When sharing C drive using domain credentials, the sharing might stop working on networks where the domain controller is not reachable (for example, home network, public wifi etc.).</span></span> <span data-ttu-id="bffb1-237">For more information, see [this post](https://blogs.msdn.microsoft.com/stevelasker/2016/06/14/configuring-docker-for-windows-volumes/).</span><span class="sxs-lookup"><span data-stu-id="bffb1-237">For more information, see [this post](https://blogs.msdn.microsoft.com/stevelasker/2016/06/14/configuring-docker-for-windows-volumes/).</span></span>

<span data-ttu-id="bffb1-238">You can also avoid the sharing problem, at a small performance cost, by setting `sharedVolumne` to `false` in the `docker.compute` file.</span><span class="sxs-lookup"><span data-stu-id="bffb1-238">You can also avoid the sharing problem, at a small performance cost, by setting `sharedVolumne` to `false` in the `docker.compute` file.</span></span>

## <a name="wipe-clean-workbench-installation"></a><span data-ttu-id="bffb1-239">Wipe clean Workbench installation</span><span class="sxs-lookup"><span data-stu-id="bffb1-239">Wipe clean Workbench installation</span></span>
<span data-ttu-id="bffb1-240">You generally don't need to do this.</span><span class="sxs-lookup"><span data-stu-id="bffb1-240">You generally don't need to do this.</span></span> <span data-ttu-id="bffb1-241">But in case you must wipe clean an installation, here are the steps:</span><span class="sxs-lookup"><span data-stu-id="bffb1-241">But in case you must wipe clean an installation, here are the steps:</span></span>

- <span data-ttu-id="bffb1-242">On Windows:</span><span class="sxs-lookup"><span data-stu-id="bffb1-242">On Windows:</span></span>
  - <span data-ttu-id="bffb1-243">First make sure you use _Add or Remove Programs_ applet in the _Control Panel_ to remove the _Azure Machine Learning Workbench_ application entry.</span><span class="sxs-lookup"><span data-stu-id="bffb1-243">First make sure you use _Add or Remove Programs_ applet in the _Control Panel_ to remove the _Azure Machine Learning Workbench_ application entry.</span></span>  
  - <span data-ttu-id="bffb1-244">Then you can download and run either one of the following scripts:</span><span class="sxs-lookup"><span data-stu-id="bffb1-244">Then you can download and run either one of the following scripts:</span></span>
    - <span data-ttu-id="bffb1-245">[Windows command line script](https://github.com/Azure/MachineLearning-Scripts/blob/master/cleanup/cleanup_win.cmd).</span><span class="sxs-lookup"><span data-stu-id="bffb1-245">[Windows command line script](https://github.com/Azure/MachineLearning-Scripts/blob/master/cleanup/cleanup_win.cmd).</span></span>
    - <span data-ttu-id="bffb1-246">[Windows PowerShell script](https://github.com/Azure/MachineLearning-Scripts/blob/master/cleanup/cleanup_win.ps1).</span><span class="sxs-lookup"><span data-stu-id="bffb1-246">[Windows PowerShell script](https://github.com/Azure/MachineLearning-Scripts/blob/master/cleanup/cleanup_win.ps1).</span></span> <span data-ttu-id="bffb1-247">(You may need to run `Set-ExecutionPolicy Unrestricted` in a privilege-elevated PowerShell window before you can run the script.)</span><span class="sxs-lookup"><span data-stu-id="bffb1-247">(You may need to run `Set-ExecutionPolicy Unrestricted` in a privilege-elevated PowerShell window before you can run the script.)</span></span>
- <span data-ttu-id="bffb1-248">On macOS:</span><span class="sxs-lookup"><span data-stu-id="bffb1-248">On macOS:</span></span>
  - <span data-ttu-id="bffb1-249">Just download and run the [macOS bash shell script](https://github.com/Azure/MachineLearning-Scripts/blob/master/cleanup/cleanup_mac.sh).</span><span class="sxs-lookup"><span data-stu-id="bffb1-249">Just download and run the [macOS bash shell script](https://github.com/Azure/MachineLearning-Scripts/blob/master/cleanup/cleanup_mac.sh).</span></span>

## <a name="azure-ml-using-a-different-python-location-than-the-azure-ml-installed-python-environment"></a><span data-ttu-id="bffb1-250">Azure ML using a different python location than the Azure ML installed python environment</span><span class="sxs-lookup"><span data-stu-id="bffb1-250">Azure ML using a different python location than the Azure ML installed python environment</span></span>
<span data-ttu-id="bffb1-251">Due to a recent change in Azure Machine Learning Workbench, users may notice that local runs may not point to the python environment installed by the Azure ML Workbench anymore.</span><span class="sxs-lookup"><span data-stu-id="bffb1-251">Due to a recent change in Azure Machine Learning Workbench, users may notice that local runs may not point to the python environment installed by the Azure ML Workbench anymore.</span></span> <span data-ttu-id="bffb1-252">This may happen if the user have another python environment installed on their computer and the "Python" path is set to point to that environment.</span><span class="sxs-lookup"><span data-stu-id="bffb1-252">This may happen if the user have another python environment installed on their computer and the "Python" path is set to point to that environment.</span></span> <span data-ttu-id="bffb1-253">In order to use Azure ML Workbench installed Python environment, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="bffb1-253">In order to use Azure ML Workbench installed Python environment, follow these steps:</span></span>
- <span data-ttu-id="bffb1-254">Go to local.compute file under your aml_config folder under your project root.</span><span class="sxs-lookup"><span data-stu-id="bffb1-254">Go to local.compute file under your aml_config folder under your project root.</span></span>
- <span data-ttu-id="bffb1-255">Change the "pythonLocation" variable to point to the physical path of Azure ML workbench installed python environment.</span><span class="sxs-lookup"><span data-stu-id="bffb1-255">Change the "pythonLocation" variable to point to the physical path of Azure ML workbench installed python environment.</span></span> <span data-ttu-id="bffb1-256">You can get this path in two ways:</span><span class="sxs-lookup"><span data-stu-id="bffb1-256">You can get this path in two ways:</span></span>
    - <span data-ttu-id="bffb1-257">Azure ML python location can be found at %localappdata%\AmlWorkbench\python\python.exe</span><span class="sxs-lookup"><span data-stu-id="bffb1-257">Azure ML python location can be found at %localappdata%\AmlWorkbench\python\python.exe</span></span>
    - <span data-ttu-id="bffb1-258">you can open cmd from Azure ML Workbench, type python on command prompt, import sys.exe, run sys.executable and get the path from there.</span><span class="sxs-lookup"><span data-stu-id="bffb1-258">you can open cmd from Azure ML Workbench, type python on command prompt, import sys.exe, run sys.executable and get the path from there.</span></span> 



## <a name="some-useful-docker-commands"></a><span data-ttu-id="bffb1-259">Some useful Docker commands</span><span class="sxs-lookup"><span data-stu-id="bffb1-259">Some useful Docker commands</span></span>

<span data-ttu-id="bffb1-260">Here are some useful Docker commands:</span><span class="sxs-lookup"><span data-stu-id="bffb1-260">Here are some useful Docker commands:</span></span>

```sh
# display all running containers
$ docker ps

# dislplay all containers (running or stopped)
$ docke ps -a

# display all images
$ docker images

# show Docker logs of a container
$ docker logs <container_id>

# create a new container and launch into a bash shell
$ docker run <image_id> /bin/bash

# launch into a bash shell on a running container
$ docker exec -it <container_id> /bin/bash

# stop an running container
$ docker stop <container_id>

# delete a container
$ docker rm <container_id>

# delete an image
$ docker rmi <image_id>

# delete all unussed Docker images 
$ docker system prune -a

```
