---
title: Set up a virtual machine as an IPython Notebook server | Microsoft Docs
description: Set up an Azure Virtual Machine for use in a data science environment with IPython Server for advanced analytics.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 818617c1-048e-49c2-b941-f9a983f93998
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 1a9bdc2e47df49cdd5e75b93c4e5408fd8ed7c5e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660626"
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Set up an Azure virtual machine as an IPython Notebook server for advanced analytics
This topic shows how to provision and configure an Azure virtual machine for advanced analytics that can be used as part of a data science environment. The Windows virtual machine is configured with supporting tools such as IPython Notebook, Azure Storage Explorer, AzCopy, as well as other utilities that are useful for advanced analytics projects. Azure Storage Explorer and AzCopy, for example, provide convenient ways to upload data to Azure blob storage from your local machine or to download it to your local machine from blob storage.

## <a name="create-vm"></a>Step 1: Create a general-purpose Azure virtual machine
If you already have an Azure virtual machine and just want to set up an IPython Notebook server on it, you can skip this step and proceed to [Step 2: Add an endpoint for IPython Notebooks to an existing virtual machine](#add-endpoint).

Before starting the process of creating a virtual machine on Azure, you need to determine the size of the machine that is needed to process the data for their project. Smaller machines have less memory and fewer CPU cores than larger machines, but they are also less expensive. For a list of machine types and prices, see the <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">Virtual Machines Pricing </a> page

1. Log in to <a href="https://manage.windowsazure.com" target="_blank">Azure classic portal</a>, and click **New** in the bottom left corner. A window will pop up. Select **COMPUTE** -> **VIRTUAL MACHINE** -> **FROM GALLERY**.
   
    ![Create workspace][24]
2. Choose one of the following images:
   
   * Windows Server 2012 R2 Datacenter
   * Windows Server Essentials Experience (Windows Server 2012 R2)
     
     Then, click the arrow pointing right at the lower right to go the next configuration page.
     
     ![Create workspace][25]
3. Enter a name for the virtual machine you want to create, select the size of the machine (Default: A3) based on the size of the data the machine is going to process and how powerful you want the machine to be (memory size and the number of compute cores), enter a user name and password for the machine. Then, click the arrow pointing right to go to the next configuration page.
   
    ![Create workspace][26]
4. Select the **REGION/AFFINITY GROUP/VIRTUAL NETWORK** that contains the **STORAGE ACCOUNT** that you are planning to use for this virtual machine, and then select that storage account. Add an endpoint at the bottom in the **ENDPOINTS**  field by entering the name of the endpoint ("IPython" here). You can choose any string as the **NAME** of the end point, and any integer between 0 and 65536 that is **available** as the **PUBLIC PORT**. The **PRIVATE PORT** has to be **9999**. You should **avoid** using public ports that have already been assigned for internet services. <a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">Ports for Internet Services</a> provides a list of ports that have been assigned and should be avoided.
   
    ![Create workspace][27]
5. Click the check mark to start the virtual machine provisioning process.
   
    ![Create workspace][28]

It may take 15-25 minutes to complete the virtual machine provisioning process. After the virtual machine has been created, the status of this machine should show as **Running**.

![Create workspace][29]

## <a name="add-endpoint"></a>Step 2: Add an endpoint for IPython Notebooks to an existing virtual machine
If you created the virtual machine by following the instructions in Step 1, then the endpoint for IPython Notebook has already been added and this step can be skipped.

If the virtual machine already exists, and you need to add an endpoint for IPython Notebook that you will install in Step 3 below, first login to Azure classic portal, select the virtual machine, and add the endpoint for IPython Notebook server. The following figure contains a screen shot of the portal after the endpoint for IPython Notebook has been added to a Windows virtual machine.

![Create workspace][17]

## <a name="run-commands"></a>Step 3: Install IPython Notebook and other supporting tools
After the virtual machine is created, use Remote Desktop Protocol (RDP) to log on to the Windows virtual machine. For instructions, see [How to Log on to a Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Open the **Command Prompt** (**Not the Powershell command window**) as an **Administrator** and run the following command.

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

When the installation completes, the IPython Notebook server is launched automatically in the *C:\\Users\\\<user name\>\\Documents\\IPython Notebooks* directory.

When prompted, enter a password for the IPython Notebook and the password of the machine administrator. This enables the IPython Notebook to run as a service on the machine.

## <a name="access"></a>Step 4: Access IPython Notebooks from a web browser
To access the IPython Notebook server, open a web browser, and input *https://&#60;virtual machine DNS name>:&#60;public port number>* in the URL text box. Here, the *&#60;public port number>* should  be the port number you specified when the IPython Notebook endpoint was added.

The *&#60;virtual machine DNS name>* can be found at the Azure classic portal. After logging in to the classic portal, click **VIRTUAL MACHINES**, select the machine you created, and then select **DASHBOARD**, the DNS name will be shown as follows:

![Create workspace][19]

You will encounter a warning stating that *There is a problem with this website's security certificate* (Internet Explorer) or *Your connection is not private* (Chrome), as shown in the following figures. Click **Continue to this website (not recommended)** (Internet Explorer) or **Advanced** and then **Proceed to &#60;*DNS Name*> (unsafe)** (Chrome) to continue. Then input the password you specified earlier to access the IPython Notebooks.

**Internet Explorer:**
![Create workspace][20]

**Chrome:**
![Create workspace][21]

After you log on to the IPython Notebook, a directory *DataScienceSamples* will show on the browser. This directory contains sample IPython Notebooks that are shared by Microsoft to help users conduct data science tasks. These sample IPython Notebooks are checked out from [**GitHub repository**](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) to the virtual machines during the IPython Notebook server setup process. Microsoft maintains and updates this repository frequently. Users may visit the GitHub repository to get the most recently updated sample IPython Notebooks.
![Create workspace][18]

## <a name="upload"></a>Step 5: Upload an existing IPython Notebook from a local machine to the IPython Notebook server
IPython Notebooks provide an easy way for users to upload an existing IPython Notebook on their local machines to the IPython Notebook server on the virtual machines. After you log on to the IPython Notebook in a web browser, click into the **directory** that the IPython Notebook will be uploaded to. Then, select an IPython Notebook .ipynb file to upload from the local machine in the **File Explorer**, and drag and drop it to the IPython Notebook directory on the web browser. Click the **Upload** button, to upload the .ipynb file to the IPython Notebook server. Other users can then start using it in from their web browsers.

![Create workspace][22]

![Create workspace][23]

## <a name="shutdown"></a>Shut down and de-allocate virtual machine when not in use
Azure Virtual Machines are priced as **pay only for what you use**. To ensure that you are not being billed when not using your virtual machine, it has to be in the **Stopped (Deallocated)** state when not in use.

> [!NOTE]
> If you shut down the virtual machine from inside the VM (using Windows power options), the VM is stopped but remains allocated. To ensure you do not continue to be billed, always stop virtual machines from the [Azure classic portal](http://manage.windowsazure.com/). You can also stop the VM through Powershell by calling **ShutdownRoleOperation** with "PostShutdownAction" equal to "StoppedDeallocated".
> 
> 

To shut down and deallocate the virtual machine:

1. Log in to the [Azure classic portal](http://manage.windowsazure.com/) using your account.  
2. Select **VIRTUAL MACHINES** from the left navigation bar.
3. In the list of virtual machines, click on the name of your virtual machine then go to the **DASHBOARD** page.
4. At the bottom of the page, click **SHUTDOWN**.

![VM Shutdown][15]

The virtual machine will be deallocated but not deleted. You may restart your virtual machine at any time from the Azure classic portal.

## <a name="your-azure-vm-is-ready-to-use-whats-next"></a>Your Azure VM is ready to use: what's next?
Your virtual machine is now ready to use in your data science exercises. The virtual machine is also ready for use as an IPython Notebook server for the exploration and processing of data, and other tasks in conjunction with Azure Machine Learning and the Team Data Science Process.

The next steps in the Team Data Science Process are mapped in the [Learning Path](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, process and sample it there in preparation for learning from the data with Azure Machine Learning.

[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-setup-virtual-machine/vmshutdown.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-setup-virtual-machine/add-endpoints-after-creation.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-setup-virtual-machine/sample-ipnbs.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-setup-virtual-machine/dns-name-and-host-name.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-setup-virtual-machine/browser-warning-ie.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-setup-virtual-machine/browser-warning.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-1.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-2.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-1.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-2.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-3.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-4.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-5.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-6.png














