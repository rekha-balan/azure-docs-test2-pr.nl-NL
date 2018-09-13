---
title: Use the Azure Data Lake Tools for Visual Studio Code | Microsoft Docs
description: 'Learn how to use the Azure Data Lake Tools for Visual Studio Code to create, test, and run U-SQL scripts. '
services: data-lake-analytics
documentationcenter: ''
author: jejiang
manager: jhubbard
editor: cgronlun
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: bb65e49d4e8f12c33f9a50ee0bc0adbcaa179fa6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552901"
---
# <a name="use-the-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="a0926-103">Use the Azure Data Lake Tools for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a0926-103">Use the Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="a0926-104">Learn how to use the Azure Data Lake Tools for Visual Studio Code (VSCode) to create, test, and run U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="a0926-104">Learn how to use the Azure Data Lake Tools for Visual Studio Code (VSCode) to create, test, and run U-SQL scripts.</span></span>  <span data-ttu-id="a0926-105">The information is also covered in the following video:</span><span class="sxs-lookup"><span data-stu-id="a0926-105">The information is also covered in the following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="a0926-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a0926-106">Prerequisites</span></span>

<span data-ttu-id="a0926-107">The Data Lake Tools can be installed on the platforms supported by VSCode that include Windows, Linux, and MacOS.</span><span class="sxs-lookup"><span data-stu-id="a0926-107">The Data Lake Tools can be installed on the platforms supported by VSCode that include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="a0926-108">You can find the prerequisites for different platforms</span><span class="sxs-lookup"><span data-stu-id="a0926-108">You can find the prerequisites for different platforms</span></span>

- <span data-ttu-id="a0926-109">Windows</span><span class="sxs-lookup"><span data-stu-id="a0926-109">Windows</span></span>

    - <span data-ttu-id="a0926-110">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0926-110">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="a0926-111">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="a0926-111">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="a0926-112">You must add the java.exe path to the system environment variable path.</span><span class="sxs-lookup"><span data-stu-id="a0926-112">You must add the java.exe path to the system environment variable path.</span></span>  <span data-ttu-id="a0926-113">For the instructions, see [how do I set or change the Path system variable?]( https://www.java.com/download/help/path.xml)</span><span class="sxs-lookup"><span data-stu-id="a0926-113">For the instructions, see [how do I set or change the Path system variable?]( https://www.java.com/download/help/path.xml)</span></span> <span data-ttu-id="a0926-114">The path is similar to C:\Program Files\Java\jdk1.8.0_77\jre\bin</span><span class="sxs-lookup"><span data-stu-id="a0926-114">The path is similar to C:\Program Files\Java\jdk1.8.0_77\jre\bin</span></span>
    - <span data-ttu-id="a0926-115">[.NET Core SDK 1.0.1-preview 2 or .NET Core 1.0.1 runtime]( https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="a0926-115">[.NET Core SDK 1.0.1-preview 2 or .NET Core 1.0.1 runtime]( https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="a0926-116">Linux (We recommend Ubuntu 14.04 LTS)</span><span class="sxs-lookup"><span data-stu-id="a0926-116">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="a0926-117">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0926-117">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="a0926-118">Use the following command to install:</span><span class="sxs-lookup"><span data-stu-id="a0926-118">Use the following command to install:</span></span>

        <span data-ttu-id="a0926-119">sudo dpkg -i code_<version_number>_amd64.deb</span><span class="sxs-lookup"><span data-stu-id="a0926-119">sudo dpkg -i code_<version_number>_amd64.deb</span></span>

    - <span data-ttu-id="a0926-120">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="a0926-120">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="a0926-121">Update the deb package source by executing following commands:</span><span class="sxs-lookup"><span data-stu-id="a0926-121">Update the deb package source by executing following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="a0926-122">Install mono by running the command:</span><span class="sxs-lookup"><span data-stu-id="a0926-122">Install mono by running the command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="a0926-123">Mono 4.6 is not supported.</span><span class="sxs-lookup"><span data-stu-id="a0926-123">Mono 4.6 is not supported.</span></span>  <span data-ttu-id="a0926-124">You must uninstall version 4.6 entirely before installing 4.2.x.</span><span class="sxs-lookup"><span data-stu-id="a0926-124">You must uninstall version 4.6 entirely before installing 4.2.x.</span></span>  

        - <span data-ttu-id="a0926-125">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="a0926-125">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="a0926-126">The instruction can be found [here]( https://java.com/en/download/help/linux_x64_install.xml).</span><span class="sxs-lookup"><span data-stu-id="a0926-126">The instruction can be found [here]( https://java.com/en/download/help/linux_x64_install.xml).</span></span>
        - <span data-ttu-id="a0926-127">[.NET Core SDK 1.0.1-preview 2 or .NET Core 1.0.1 runtime]( https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="a0926-127">[.NET Core SDK 1.0.1-preview 2 or .NET Core 1.0.1 runtime]( https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="a0926-128">MacOS</span><span class="sxs-lookup"><span data-stu-id="a0926-128">MacOS</span></span>

    - <span data-ttu-id="a0926-129">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0926-129">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="a0926-130">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="a0926-130">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="a0926-131">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="a0926-131">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="a0926-132">The instruction can be found [here](https://java.com/en/download/help/mac_install.xml).</span><span class="sxs-lookup"><span data-stu-id="a0926-132">The instruction can be found [here](https://java.com/en/download/help/mac_install.xml).</span></span>
    - <span data-ttu-id="a0926-133">[.NET Core SDK 1.0.1-preview 2 or .NET Core 1.0.1 runtime]( https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="a0926-133">[.NET Core SDK 1.0.1-preview 2 or .NET Core 1.0.1 runtime]( https://www.microsoft.com/net/download).</span></span>

## <a name="install-the-data-lake-tools"></a><span data-ttu-id="a0926-134">Install the Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="a0926-134">Install the Data Lake Tools</span></span>

<span data-ttu-id="a0926-135">After you have installed the prerequisites, you can install the Data Lake Tools for VSCode.</span><span class="sxs-lookup"><span data-stu-id="a0926-135">After you have installed the prerequisites, you can install the Data Lake Tools for VSCode.</span></span>

<span data-ttu-id="a0926-136">**To install the Data Lake Tools**</span><span class="sxs-lookup"><span data-stu-id="a0926-136">**To install the Data Lake Tools**</span></span>

1. <span data-ttu-id="a0926-137">Open **Visual Studio Code**.</span><span class="sxs-lookup"><span data-stu-id="a0926-137">Open **Visual Studio Code**.</span></span>
2. <span data-ttu-id="a0926-138">Press **CTRL+P**, and then enter:</span><span class="sxs-lookup"><span data-stu-id="a0926-138">Press **CTRL+P**, and then enter:</span></span>

        ext install usql-vscode-ext
    <span data-ttu-id="a0926-139">You can see a list of Visual Studio code extensions.</span><span class="sxs-lookup"><span data-stu-id="a0926-139">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="a0926-140">One of them is **Azure Data Lake Tool (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="a0926-140">One of them is **Azure Data Lake Tool (Preview)**.</span></span>
3. <span data-ttu-id="a0926-141">Click **Install** next to **Azure Data Lake Tool (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="a0926-141">Click **Install** next to **Azure Data Lake Tool (Preview)**.</span></span> <span data-ttu-id="a0926-142">After a few seconds, the Install button will be changed to Reload.</span><span class="sxs-lookup"><span data-stu-id="a0926-142">After a few seconds, the Install button will be changed to Reload.</span></span>
4. <span data-ttu-id="a0926-143">Click **Reload** to activate the extension.</span><span class="sxs-lookup"><span data-stu-id="a0926-143">Click **Reload** to activate the extension.</span></span>
5. <span data-ttu-id="a0926-144">Click **OK** to confirm.</span><span class="sxs-lookup"><span data-stu-id="a0926-144">Click **OK** to confirm.</span></span> <span data-ttu-id="a0926-145">You can see Azure Data Lake Tools in the Extensions pane.</span><span class="sxs-lookup"><span data-stu-id="a0926-145">You can see Azure Data Lake Tools in the Extensions pane.</span></span>

    ![Data Lake Tools for Visual Studio Code install](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)


## <a name="connect-to-azure"></a><span data-ttu-id="a0926-147">Connect to Azure</span><span class="sxs-lookup"><span data-stu-id="a0926-147">Connect to Azure</span></span>

<span data-ttu-id="a0926-148">Before you can compile and run U-SQL scripts, you must connect to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="a0926-148">Before you can compile and run U-SQL scripts, you must connect to your Azure account.</span></span>

<span data-ttu-id="a0926-149">**To connect to Azure**</span><span class="sxs-lookup"><span data-stu-id="a0926-149">**To connect to Azure**</span></span>

1.  <span data-ttu-id="a0926-150">Open the command palette by pressing **CTRL+SHIFT+P**.</span><span class="sxs-lookup"><span data-stu-id="a0926-150">Open the command palette by pressing **CTRL+SHIFT+P**.</span></span> 
2.  <span data-ttu-id="a0926-151">Enter **ADL:Login**.</span><span class="sxs-lookup"><span data-stu-id="a0926-151">Enter **ADL:Login**.</span></span>

    ![Data Lake Tools for Visual Studio Code command palette](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)

2.  <span data-ttu-id="a0926-153">Follow the instructions to sign in from the web page.</span><span class="sxs-lookup"><span data-stu-id="a0926-153">Follow the instructions to sign in from the web page.</span></span> <span data-ttu-id="a0926-154">Once connected, your account name is shown on the status bar on the bottom of the window.</span><span class="sxs-lookup"><span data-stu-id="a0926-154">Once connected, your account name is shown on the status bar on the bottom of the window.</span></span>

> [!NOTE] 
> <span data-ttu-id="a0926-155">If your account has two factors enabled, it is recommended to use phone authentication instead of Pin.</span><span class="sxs-lookup"><span data-stu-id="a0926-155">If your account has two factors enabled, it is recommended to use phone authentication instead of Pin.</span></span>

<span data-ttu-id="a0926-156">To sign off, use the command **ADL:Logout**</span><span class="sxs-lookup"><span data-stu-id="a0926-156">To sign off, use the command **ADL:Logout**</span></span>

## <a name="list-data-lake-analytics-accounts"></a><span data-ttu-id="a0926-157">List Data Lake Analytics accounts</span><span class="sxs-lookup"><span data-stu-id="a0926-157">List Data Lake Analytics accounts</span></span>

<span data-ttu-id="a0926-158">To test the connection, you can list your Data Lake Analytics accounts:</span><span class="sxs-lookup"><span data-stu-id="a0926-158">To test the connection, you can list your Data Lake Analytics accounts:</span></span>

<span data-ttu-id="a0926-159">**To list the Data Lake Analytics accounts under your Azure subscription**</span><span class="sxs-lookup"><span data-stu-id="a0926-159">**To list the Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="a0926-160">Open the command palette by pressing **CTRL+SHIFT+P**.</span><span class="sxs-lookup"><span data-stu-id="a0926-160">Open the command palette by pressing **CTRL+SHIFT+P**.</span></span>
2. <span data-ttu-id="a0926-161">Type **ADL:List Accounts**.</span><span class="sxs-lookup"><span data-stu-id="a0926-161">Type **ADL:List Accounts**.</span></span>  <span data-ttu-id="a0926-162">The accounts appear in the **Output** pane.</span><span class="sxs-lookup"><span data-stu-id="a0926-162">The accounts appear in the **Output** pane.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="a0926-163">Work with U-SQL</span><span class="sxs-lookup"><span data-stu-id="a0926-163">Work with U-SQL</span></span>

<span data-ttu-id="a0926-164">You need open either a U-SQL file or a folder to work with U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a0926-164">You need open either a U-SQL file or a folder to work with U-SQL.</span></span>

<span data-ttu-id="a0926-165">**To open a folder for your U-SQL project**</span><span class="sxs-lookup"><span data-stu-id="a0926-165">**To open a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="a0926-166">From Visual Studio Code, Click the **File** menu, and then click **Open Folder**.</span><span class="sxs-lookup"><span data-stu-id="a0926-166">From Visual Studio Code, Click the **File** menu, and then click **Open Folder**.</span></span>
2. <span data-ttu-id="a0926-167">Specify a folder, and then click **Select Folder**.</span><span class="sxs-lookup"><span data-stu-id="a0926-167">Specify a folder, and then click **Select Folder**.</span></span>
3. <span data-ttu-id="a0926-168">Click the **File** menu, and then click **New**.</span><span class="sxs-lookup"><span data-stu-id="a0926-168">Click the **File** menu, and then click **New**.</span></span> <span data-ttu-id="a0926-169">An **Untilted-1** file is added to the project.</span><span class="sxs-lookup"><span data-stu-id="a0926-169">An **Untilted-1** file is added to the project.</span></span>
4. <span data-ttu-id="a0926-170">Copy and paste the following code into Untitled-1 file:</span><span class="sxs-lookup"><span data-stu-id="a0926-170">Copy and paste the following code into Untitled-1 file:</span></span>

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    <span data-ttu-id="a0926-171">The script creates a departments.csv file with some data in the /output folder.</span><span class="sxs-lookup"><span data-stu-id="a0926-171">The script creates a departments.csv file with some data in the /output folder.</span></span>

5. <span data-ttu-id="a0926-172">Save the file as **myUSQL.usql** in the openned folder.</span><span class="sxs-lookup"><span data-stu-id="a0926-172">Save the file as **myUSQL.usql** in the openned folder.</span></span> <span data-ttu-id="a0926-173">Notice an **adltools_settings.json** configuration file is also added to the project.</span><span class="sxs-lookup"><span data-stu-id="a0926-173">Notice an **adltools_settings.json** configuration file is also added to the project.</span></span>
4. <span data-ttu-id="a0926-174">Open and configure **adltools_settings.json** with the following properties:</span><span class="sxs-lookup"><span data-stu-id="a0926-174">Open and configure **adltools_settings.json** with the following properties:</span></span>

    - <span data-ttu-id="a0926-175">Account:  A Data Lake Analytics account under your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a0926-175">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="a0926-176">Optional settings:</span><span class="sxs-lookup"><span data-stu-id="a0926-176">Optional settings:</span></span>

        - <span data-ttu-id="a0926-177">Priority: The priority range is from 1 to 1000 with 1 the highest priority.</span><span class="sxs-lookup"><span data-stu-id="a0926-177">Priority: The priority range is from 1 to 1000 with 1 the highest priority.</span></span> <span data-ttu-id="a0926-178">The default value is 1000.</span><span class="sxs-lookup"><span data-stu-id="a0926-178">The default value is 1000.</span></span>
        - <span data-ttu-id="a0926-179">Parallelism: The parallelism range is from 1 to 150.</span><span class="sxs-lookup"><span data-stu-id="a0926-179">Parallelism: The parallelism range is from 1 to 150.</span></span> <span data-ttu-id="a0926-180">The default value is 150.</span><span class="sxs-lookup"><span data-stu-id="a0926-180">The default value is 150.</span></span> 

        > [!NOTE] 
        > <span data-ttu-id="a0926-181">If the settings are invalid, the default values are used.</span><span class="sxs-lookup"><span data-stu-id="a0926-181">If the settings are invalid, the default values are used.</span></span>

     ![Data Lake Tools for Visual Studio Code configuration file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="a0926-183">A compute Data Lake Analytics account is needed for compiling and running U-SQL jobs.</span><span class="sxs-lookup"><span data-stu-id="a0926-183">A compute Data Lake Analytics account is needed for compiling and running U-SQL jobs.</span></span>  <span data-ttu-id="a0926-184">You must configure the computer account before you can compile and run U-SQL jobs.</span><span class="sxs-lookup"><span data-stu-id="a0926-184">You must configure the computer account before you can compile and run U-SQL jobs.</span></span>

<span data-ttu-id="a0926-185">Comparing to openning a file, openning a folder allows you to:</span><span class="sxs-lookup"><span data-stu-id="a0926-185">Comparing to openning a file, openning a folder allows you to:</span></span>

- <span data-ttu-id="a0926-186">Use code-behind file.</span><span class="sxs-lookup"><span data-stu-id="a0926-186">Use code-behind file.</span></span>  <span data-ttu-id="a0926-187">In the single-file mode, code-behind is not supported.</span><span class="sxs-lookup"><span data-stu-id="a0926-187">In the single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="a0926-188">Use configuration file.</span><span class="sxs-lookup"><span data-stu-id="a0926-188">Use configuration file.</span></span> <span data-ttu-id="a0926-189">When you open a folder, the scripts in the working folder share one configuration file.</span><span class="sxs-lookup"><span data-stu-id="a0926-189">When you open a folder, the scripts in the working folder share one configuration file.</span></span>


<span data-ttu-id="a0926-190">The U-SQL script compilation is done remotely by the Data Lake Analytics service.</span><span class="sxs-lookup"><span data-stu-id="a0926-190">The U-SQL script compilation is done remotely by the Data Lake Analytics service.</span></span>  <span data-ttu-id="a0926-191">When you issue the compile command, the U-SQL script is sent to your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="a0926-191">When you issue the compile command, the U-SQL script is sent to your Data Lake Analytics account.</span></span> <span data-ttu-id="a0926-192">The compilation result is late received by the Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a0926-192">The compilation result is late received by the Visual Studio Code.</span></span> <span data-ttu-id="a0926-193">Because of the remote compilation, Visual Studio code requires the information to connect to your Data Lake Analytics account in the configuration file.</span><span class="sxs-lookup"><span data-stu-id="a0926-193">Because of the remote compilation, Visual Studio code requires the information to connect to your Data Lake Analytics account in the configuration file.</span></span>

<span data-ttu-id="a0926-194">**To compile a U-SQL script**</span><span class="sxs-lookup"><span data-stu-id="a0926-194">**To compile a U-SQL script**</span></span>

1. <span data-ttu-id="a0926-195">Open the command palette by pressing **CTRL+SHIFT+P**.</span><span class="sxs-lookup"><span data-stu-id="a0926-195">Open the command palette by pressing **CTRL+SHIFT+P**.</span></span> 
2. <span data-ttu-id="a0926-196">Enter **ADL: Compile Script**.</span><span class="sxs-lookup"><span data-stu-id="a0926-196">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="a0926-197">Compile results show in output window.</span><span class="sxs-lookup"><span data-stu-id="a0926-197">Compile results show in output window.</span></span> <span data-ttu-id="a0926-198">You can also right-click a script file, and then click **ADL: Compile Script** to compile a U-SQL job.</span><span class="sxs-lookup"><span data-stu-id="a0926-198">You can also right-click a script file, and then click **ADL: Compile Script** to compile a U-SQL job.</span></span> <span data-ttu-id="a0926-199">The compilation result is shown in the output pane.</span><span class="sxs-lookup"><span data-stu-id="a0926-199">The compilation result is shown in the output pane.</span></span>
 

<span data-ttu-id="a0926-200">**To submit a U-SQL script**</span><span class="sxs-lookup"><span data-stu-id="a0926-200">**To submit a U-SQL script**</span></span>

1. <span data-ttu-id="a0926-201">Open the command palette by pressing **CTRL+SHIFT+P**.</span><span class="sxs-lookup"><span data-stu-id="a0926-201">Open the command palette by pressing **CTRL+SHIFT+P**.</span></span> 
2. <span data-ttu-id="a0926-202">Enter **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="a0926-202">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="a0926-203">You can also right-click a script file, and then click **ADL: Submit Job** to submit a U-SQL job.</span><span class="sxs-lookup"><span data-stu-id="a0926-203">You can also right-click a script file, and then click **ADL: Submit Job** to submit a U-SQL job.</span></span> 

<span data-ttu-id="a0926-204">After submitting a U-SQL job, submission logs is shown in output window in VSCode.</span><span class="sxs-lookup"><span data-stu-id="a0926-204">After submitting a U-SQL job, submission logs is shown in output window in VSCode.</span></span> <span data-ttu-id="a0926-205">If the submission is successful, the job URL is shown as well.</span><span class="sxs-lookup"><span data-stu-id="a0926-205">If the submission is successful, the job URL is shown as well.</span></span> <span data-ttu-id="a0926-206">You can open the job URL in a web browser to track real-time job status.</span><span class="sxs-lookup"><span data-stu-id="a0926-206">You can open the job URL in a web browser to track real-time job status.</span></span>

<span data-ttu-id="a0926-207">To enable output job details: set ‘jobInformationOutputPath’ in the **vscode for u-sql_settings.json** file.</span><span class="sxs-lookup"><span data-stu-id="a0926-207">To enable output job details: set ‘jobInformationOutputPath’ in the **vscode for u-sql_settings.json** file.</span></span>
 
## <a name="use-code-behind-file"></a><span data-ttu-id="a0926-208">Use code-behind file</span><span class="sxs-lookup"><span data-stu-id="a0926-208">Use code-behind file</span></span>

<span data-ttu-id="a0926-209">Code-behind file is a CSharp file associate with one U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="a0926-209">Code-behind file is a CSharp file associate with one U-SQL script.</span></span> <span data-ttu-id="a0926-210">You can define script dedicated UDO/UDA/UDT/UDF in the code-behind file.</span><span class="sxs-lookup"><span data-stu-id="a0926-210">You can define script dedicated UDO/UDA/UDT/UDF in the code-behind file.</span></span> <span data-ttu-id="a0926-211">The UDO/UDA/UDT/UDF can be directly used in the script without register the assembly first.</span><span class="sxs-lookup"><span data-stu-id="a0926-211">The UDO/UDA/UDT/UDF can be directly used in the script without register the assembly first.</span></span> <span data-ttu-id="a0926-212">Code-behind file is put in the same folder as its peering U-SQL script file.</span><span class="sxs-lookup"><span data-stu-id="a0926-212">Code-behind file is put in the same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="a0926-213">If the script is named xxx.usql, the code-behind is named as xxx.usql.cs.</span><span class="sxs-lookup"><span data-stu-id="a0926-213">If the script is named xxx.usql, the code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="a0926-214">Deleting the code-behind file manually disables the code-behind feature for its associated U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="a0926-214">Deleting the code-behind file manually disables the code-behind feature for its associated U-SQL script.</span></span> <span data-ttu-id="a0926-215">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL – User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span><span class="sxs-lookup"><span data-stu-id="a0926-215">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL – User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="a0926-216">To support code-behind, a working folder must be opened.</span><span class="sxs-lookup"><span data-stu-id="a0926-216">To support code-behind, a working folder must be opened.</span></span> 

<span data-ttu-id="a0926-217">**To generate a code-behind file**</span><span class="sxs-lookup"><span data-stu-id="a0926-217">**To generate a code-behind file**</span></span>

1. <span data-ttu-id="a0926-218">Open a soucre file.</span><span class="sxs-lookup"><span data-stu-id="a0926-218">Open a soucre file.</span></span> 
2. <span data-ttu-id="a0926-219">Open the command palette by pressing **CTRL+SHIFT+P**.</span><span class="sxs-lookup"><span data-stu-id="a0926-219">Open the command palette by pressing **CTRL+SHIFT+P**.</span></span>
3. <span data-ttu-id="a0926-220">Enter **ADL: Generate Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="a0926-220">Enter **ADL: Generate Code Behind**.</span></span>  <span data-ttu-id="a0926-221">A code-behind file is created in the same folder.</span><span class="sxs-lookup"><span data-stu-id="a0926-221">A code-behind file is created in the same folder.</span></span> 

<span data-ttu-id="a0926-222">You can also right-click a script file, and then click **ADL: Generate Code Behind** to generate a code-behind file.</span><span class="sxs-lookup"><span data-stu-id="a0926-222">You can also right-click a script file, and then click **ADL: Generate Code Behind** to generate a code-behind file.</span></span> 

<span data-ttu-id="a0926-223">Compile and submit a U-SQL script with code-behind is the same as the standalone U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="a0926-223">Compile and submit a U-SQL script with code-behind is the same as the standalone U-SQL script.</span></span>

<span data-ttu-id="a0926-224">The following two screenshots show a code-behind file and its associated U-SQL script file:</span><span class="sxs-lookup"><span data-stu-id="a0926-224">The following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Data Lake Tools for Visual Studio Code code behind](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Data Lake Tools for Visual Studio Code code behind](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="a0926-227">Use assemblies</span><span class="sxs-lookup"><span data-stu-id="a0926-227">Use assemblies</span></span>

<span data-ttu-id="a0926-228">For the information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="a0926-228">For the information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="a0926-229">Using the Data Lake Tools, you can register custom code assemblies to the Data Lake Analytics catalog.</span><span class="sxs-lookup"><span data-stu-id="a0926-229">Using the Data Lake Tools, you can register custom code assemblies to the Data Lake Analytics catalog.</span></span>

<span data-ttu-id="a0926-230">**To register an assembly**</span><span class="sxs-lookup"><span data-stu-id="a0926-230">**To register an assembly**</span></span>

1.  <span data-ttu-id="a0926-231">Press **CTRL+SHIFT+P** to open Command Palette.</span><span class="sxs-lookup"><span data-stu-id="a0926-231">Press **CTRL+SHIFT+P** to open Command Palette.</span></span>
2.  <span data-ttu-id="a0926-232">Enter **ADL:Register Assembly**.</span><span class="sxs-lookup"><span data-stu-id="a0926-232">Enter **ADL:Register Assembly**.</span></span>
3.  <span data-ttu-id="a0926-233">Select a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="a0926-233">Select a Data Lake Analytics account.</span></span>
4.  <span data-ttu-id="a0926-234">Select a database.</span><span class="sxs-lookup"><span data-stu-id="a0926-234">Select a database.</span></span>
5.  <span data-ttu-id="a0926-235">Specify the local assembly path.</span><span class="sxs-lookup"><span data-stu-id="a0926-235">Specify the local assembly path.</span></span>

<span data-ttu-id="a0926-236">The following U-SQL code demonstrates how to call an assembly.</span><span class="sxs-lookup"><span data-stu-id="a0926-236">The following U-SQL code demonstrates how to call an assembly.</span></span> <span data-ttu-id="a0926-237">In the sample, the assemly name is *test*.</span><span class="sxs-lookup"><span data-stu-id="a0926-237">In the sample, the assemly name is *test*.</span></span>

    REFERENCE ASSEMBLY [test];
    @a=EXTRACT Iid int,Starts DateTime,Region string,Query string,DwellTime int,Results string,ClickedUrls string 
    FROM @"ruoxin/SearchLog.txt" USING Extractors.Tsv();
    
    @d=SELECT DISTINCT Region FROM @a;
    
    @d1=PROCESS @d
        PRODUCE Region string,
                Mkt string
                USING new USQLApplication_codebehind.MyProcessor();
    
    OUTPUT @d1 TO @"ruoxin/SearchLogtest.txt" USING Outputters.Tsv();



## <a name="access-data-lake-analytics-catalog"></a><span data-ttu-id="a0926-238">Access Data Lake Analytics catalog</span><span class="sxs-lookup"><span data-stu-id="a0926-238">Access Data Lake Analytics catalog</span></span>

<span data-ttu-id="a0926-239">After you have connected to Azure, you can use the following steps to access the U-SQL catalog:</span><span class="sxs-lookup"><span data-stu-id="a0926-239">After you have connected to Azure, you can use the following steps to access the U-SQL catalog:</span></span>

<span data-ttu-id="a0926-240">**To access U-SQL metadata**</span><span class="sxs-lookup"><span data-stu-id="a0926-240">**To access U-SQL metadata**</span></span>

1.  <span data-ttu-id="a0926-241">Press **CTRL+SHIFT+P**, and then type **ADL:List Tables**.</span><span class="sxs-lookup"><span data-stu-id="a0926-241">Press **CTRL+SHIFT+P**, and then type **ADL:List Tables**.</span></span>
2.  <span data-ttu-id="a0926-242">Click one of the Data Lake Analytics accounts.</span><span class="sxs-lookup"><span data-stu-id="a0926-242">Click one of the Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="a0926-243">Click one of the Data Lake Analytics databases.</span><span class="sxs-lookup"><span data-stu-id="a0926-243">Click one of the Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="a0926-244">Click one of the schemas.</span><span class="sxs-lookup"><span data-stu-id="a0926-244">Click one of the schemas.</span></span> <span data-ttu-id="a0926-245">You can see the tables.</span><span class="sxs-lookup"><span data-stu-id="a0926-245">You can see the tables.</span></span>

## <a name="additional-features"></a><span data-ttu-id="a0926-246">Additional features</span><span class="sxs-lookup"><span data-stu-id="a0926-246">Additional features</span></span>

<span data-ttu-id="a0926-247">The Data Lake Tools for VSCode supports the following features:</span><span class="sxs-lookup"><span data-stu-id="a0926-247">The Data Lake Tools for VSCode supports the following features:</span></span>

-   <span data-ttu-id="a0926-248">IntelliSense auto-complete.</span><span class="sxs-lookup"><span data-stu-id="a0926-248">IntelliSense auto-complete.</span></span> <span data-ttu-id="a0926-249">Suggestions are popped up around keyword, method, variables, etc. Different icons represent different types of the objects:</span><span class="sxs-lookup"><span data-stu-id="a0926-249">Suggestions are popped up around keyword, method, variables, etc. Different icons represent different types of the objects:</span></span>

    - <span data-ttu-id="a0926-250">Scala Data Type</span><span class="sxs-lookup"><span data-stu-id="a0926-250">Scala Data Type</span></span>
    - <span data-ttu-id="a0926-251">Complex Data Type</span><span class="sxs-lookup"><span data-stu-id="a0926-251">Complex Data Type</span></span>
    - <span data-ttu-id="a0926-252">Built-in UDTs</span><span class="sxs-lookup"><span data-stu-id="a0926-252">Built-in UDTs</span></span>
    - <span data-ttu-id="a0926-253">.Net Collection & Classes</span><span class="sxs-lookup"><span data-stu-id="a0926-253">.Net Collection & Classes</span></span>
    - <span data-ttu-id="a0926-254">C# Expressions</span><span class="sxs-lookup"><span data-stu-id="a0926-254">C# Expressions</span></span>
    - <span data-ttu-id="a0926-255">Built-in C# UDFs, UDOs, and UDAAGs</span><span class="sxs-lookup"><span data-stu-id="a0926-255">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="a0926-256">U-SQL Functions</span><span class="sxs-lookup"><span data-stu-id="a0926-256">U-SQL Functions</span></span>
    - <span data-ttu-id="a0926-257">U-SQL Windowing Function</span><span class="sxs-lookup"><span data-stu-id="a0926-257">U-SQL Windowing Function</span></span>
 
    ![Data Lake Tools for Visual Studio Code IntelliSense object types](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="a0926-259">IntelliSense auto-complete on the Data Lake Analytics Metadata.</span><span class="sxs-lookup"><span data-stu-id="a0926-259">IntelliSense auto-complete on the Data Lake Analytics Metadata.</span></span> <span data-ttu-id="a0926-260">The Data Lake Tools download Data Lake Analytics metadata information locally.</span><span class="sxs-lookup"><span data-stu-id="a0926-260">The Data Lake Tools download Data Lake Analytics metadata information locally.</span></span>  <span data-ttu-id="a0926-261">The IntelliSense feature automatically populates objects, including Database, Schema, Table, View, TVF, Procedures, C# Assemblies, from the Data Lake Analytics metadata.</span><span class="sxs-lookup"><span data-stu-id="a0926-261">The IntelliSense feature automatically populates objects, including Database, Schema, Table, View, TVF, Procedures, C# Assemblies, from the Data Lake Analytics metadata.</span></span>
 
    ![Data Lake Tools for Visual Studio Code IntelliSense metadata](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="a0926-263">IntelliSense error marker.</span><span class="sxs-lookup"><span data-stu-id="a0926-263">IntelliSense error marker.</span></span> <span data-ttu-id="a0926-264">The Data Lake Tools underline the editing errors for U-SQL and C#.</span><span class="sxs-lookup"><span data-stu-id="a0926-264">The Data Lake Tools underline the editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="a0926-265">Syntax highlights.</span><span class="sxs-lookup"><span data-stu-id="a0926-265">Syntax highlights.</span></span> <span data-ttu-id="a0926-266">The Data Lake Tools use different color to differentiate variables, keywords, data type, functions, etc.</span><span class="sxs-lookup"><span data-stu-id="a0926-266">The Data Lake Tools use different color to differentiate variables, keywords, data type, functions, etc.</span></span> 

    ![Data Lake Tools for Visual Studio Code syntax highlights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

##<a name="next-steps"></a><span data-ttu-id="a0926-268">Next steps:</span><span class="sxs-lookup"><span data-stu-id="a0926-268">Next steps:</span></span>

- <span data-ttu-id="a0926-269">For the getting started information on Data Lake Analytics, see [Tutorial: get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a0926-269">For the getting started information on Data Lake Analytics, see [Tutorial: get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="a0926-270">For information on using Data Lake Tools for Visual Studio, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a0926-270">For information on using Data Lake Tools for Visual Studio, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="a0926-271">For the information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="a0926-271">For the information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>












