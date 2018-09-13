---
title: Create an Jupyter/IPython Notebook | Microsoft Docs
description: Learn how to deploy the Jupyter/IPython Notebook on a Linux virtual machine created with the resource manager deployment model in Azure.
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b494db443b2865280fa34888620710e2e696f7b0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552871"
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="094d0-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span><span class="sxs-lookup"><span data-stu-id="094d0-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="094d0-104">The [Jupyter project](http://jupyter.org), formerly the [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with the creation of a live computational document.</span><span class="sxs-lookup"><span data-stu-id="094d0-104">The [Jupyter project](http://jupyter.org), formerly the [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with the creation of a live computational document.</span></span> <span data-ttu-id="094d0-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span><span class="sxs-lookup"><span data-stu-id="094d0-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="094d0-106">Whether you're absolutely new to Python and want to learn it in a fun, interactive environment or do some serious parallel/technical computing, the Jupyter Notebook is a great choice.</span><span class="sxs-lookup"><span data-stu-id="094d0-106">Whether you're absolutely new to Python and want to learn it in a fun, interactive environment or do some serious parallel/technical computing, the Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="094d0-107">![Screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages to analyze the structure of a sound recording.</span><span class="sxs-lookup"><span data-stu-id="094d0-107">![Screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages to analyze the structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="094d0-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span><span class="sxs-lookup"><span data-stu-id="094d0-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="094d0-109">Azure provides a service that you can use to [quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="094d0-109">Azure provides a service that you can use to [quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="094d0-110">By using the Azure Notebook Service, you can easily gain access to Jupyter's web-accessible interface to scalable computational resources with all the power of Python and its many libraries.</span><span class="sxs-lookup"><span data-stu-id="094d0-110">By using the Azure Notebook Service, you can easily gain access to Jupyter's web-accessible interface to scalable computational resources with all the power of Python and its many libraries.</span></span>  <span data-ttu-id="094d0-111">Since the installation is handled by the service, users can access these resources without the need for administration and configuration by the user.</span><span class="sxs-lookup"><span data-stu-id="094d0-111">Since the installation is handled by the service, users can access these resources without the need for administration and configuration by the user.</span></span>

<span data-ttu-id="094d0-112">If the notebook service does not work for your scenario please continue to read this article which will will show you how to deploy the Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span><span class="sxs-lookup"><span data-stu-id="094d0-112">If the notebook service does not work for your scenario please continue to read this article which will will show you how to deploy the Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="094d0-113">Create and configure a VM on Azure</span><span class="sxs-lookup"><span data-stu-id="094d0-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="094d0-114">The first step is to create a virtual machine (VM)  running on Azure.</span><span class="sxs-lookup"><span data-stu-id="094d0-114">The first step is to create a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="094d0-115">This VM is a complete operating system in the cloud and will be used to run the Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="094d0-115">This VM is a complete operating system in the cloud and will be used to run the Jupyter Notebook.</span></span> <span data-ttu-id="094d0-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover the setup of Jupyter on both types of virtual machines.</span><span class="sxs-lookup"><span data-stu-id="094d0-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover the setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="094d0-117">Create a Linux VM and open a port for Jupyter</span><span class="sxs-lookup"><span data-stu-id="094d0-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="094d0-118">Follow the instructions given [here][portal-vm-linux] to create a virtual machine of the *Ubuntu* distribution.</span><span class="sxs-lookup"><span data-stu-id="094d0-118">Follow the instructions given [here][portal-vm-linux] to create a virtual machine of the *Ubuntu* distribution.</span></span> <span data-ttu-id="094d0-119">This tutorial uses Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="094d0-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="094d0-120">We'll assume the user name *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="094d0-120">We'll assume the user name *azureuser*.</span></span>

<span data-ttu-id="094d0-121">After the virtual machine deploys we need to open up a security rule on the network security group.</span><span class="sxs-lookup"><span data-stu-id="094d0-121">After the virtual machine deploys we need to open up a security rule on the network security group.</span></span>  <span data-ttu-id="094d0-122">From the Azure portal, go to **Network Security Groups** and open the tab for the Security Group corresponding to your VM.</span><span class="sxs-lookup"><span data-stu-id="094d0-122">From the Azure portal, go to **Network Security Groups** and open the tab for the Security Group corresponding to your VM.</span></span> <span data-ttu-id="094d0-123">You need to add an Inbound Security rule with the following settings: **TCP** for the protocol, **\*** for the source (public) port and **9999** for the destination (private) port.</span><span class="sxs-lookup"><span data-stu-id="094d0-123">You need to add an Inbound Security rule with the following settings: **TCP** for the protocol, **\*** for the source (public) port and **9999** for the destination (private) port.</span></span>

![Screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="094d0-125">While in your Network Security Group, click on **Network Interfaces** and note the **Public IP Address** as it will be needed to connect to your VM in the next step.</span><span class="sxs-lookup"><span data-stu-id="094d0-125">While in your Network Security Group, click on **Network Interfaces** and note the **Public IP Address** as it will be needed to connect to your VM in the next step.</span></span>

## <a name="install-required-software-on-the-vm"></a><span data-ttu-id="094d0-126">Install required software on the VM</span><span class="sxs-lookup"><span data-stu-id="094d0-126">Install required software on the VM</span></span>
<span data-ttu-id="094d0-127">To run the Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="094d0-127">To run the Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="094d0-128">Connect to your linux vm using ssh and the username/password pair you chose when you created the vm.</span><span class="sxs-lookup"><span data-stu-id="094d0-128">Connect to your linux vm using ssh and the username/password pair you chose when you created the vm.</span></span> <span data-ttu-id="094d0-129">In this tutorial we will use PuTTY and connect from Windows.</span><span class="sxs-lookup"><span data-stu-id="094d0-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="094d0-130">Installing Jupyter on Ubuntu</span><span class="sxs-lookup"><span data-stu-id="094d0-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="094d0-131">Install Anaconda, a popular data science python distribution, using one of the links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="094d0-131">Install Anaconda, a popular data science python distribution, using one of the links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="094d0-132">As of the writing of this document, the below links are the most up to date versions.</span><span class="sxs-lookup"><span data-stu-id="094d0-132">As of the writing of this document, the below links are the most up to date versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="094d0-133">Anaconda Installs for Linux</span><span class="sxs-lookup"><span data-stu-id="094d0-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="094d0-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="094d0-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="094d0-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="094d0-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="094d0-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="094d0-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="094d0-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="094d0-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="094d0-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="094d0-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="094d0-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="094d0-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="094d0-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span><span class="sxs-lookup"><span data-stu-id="094d0-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="094d0-141">As an example, this is how you can install Anaconda on Ubuntu</span><span class="sxs-lookup"><span data-stu-id="094d0-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter to the latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="094d0-143">Configuring Jupyter and using SSL</span><span class="sxs-lookup"><span data-stu-id="094d0-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="094d0-144">After installing we need to take a moment to setup the configuration files for Jupyter.</span><span class="sxs-lookup"><span data-stu-id="094d0-144">After installing we need to take a moment to setup the configuration files for Jupyter.</span></span> <span data-ttu-id="094d0-145">If you experience troubles with configuring Jupyter it may be helpful to look at the [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="094d0-145">If you experience troubles with configuring Jupyter it may be helpful to look at the [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="094d0-146">Next we `cd` to the profile directory to create our SSL certificate and edit the profiles configuration file.</span><span class="sxs-lookup"><span data-stu-id="094d0-146">Next we `cd` to the profile directory to create our SSL certificate and edit the profiles configuration file.</span></span>

<span data-ttu-id="094d0-147">On Linux use the following command.</span><span class="sxs-lookup"><span data-stu-id="094d0-147">On Linux use the following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="094d0-148">Use the following command to create the SSL certificate(Linux and Windows).</span><span class="sxs-lookup"><span data-stu-id="094d0-148">Use the following command to create the SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="094d0-149">Note that since we are creating a self-signed SSL certificate, when connecting to the notebook your browser will give you a security warning.</span><span class="sxs-lookup"><span data-stu-id="094d0-149">Note that since we are creating a self-signed SSL certificate, when connecting to the notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="094d0-150">For long-term production use, you will want to use a properly signed certificate associated with your organization.</span><span class="sxs-lookup"><span data-stu-id="094d0-150">For long-term production use, you will want to use a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="094d0-151">Since certificate management is beyond the scope of this demo, we will stick to a self-signed certificate for now.</span><span class="sxs-lookup"><span data-stu-id="094d0-151">Since certificate management is beyond the scope of this demo, we will stick to a self-signed certificate for now.</span></span>

<span data-ttu-id="094d0-152">In addition to using a certificate, you must also provide a password to protect your notebook from unauthorized use.</span><span class="sxs-lookup"><span data-stu-id="094d0-152">In addition to using a certificate, you must also provide a password to protect your notebook from unauthorized use.</span></span>  <span data-ttu-id="094d0-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need to encrypt your password first.</span><span class="sxs-lookup"><span data-stu-id="094d0-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need to encrypt your password first.</span></span>  <span data-ttu-id="094d0-154">IPython provides a utility to do so; at a command prompt run the following command.</span><span class="sxs-lookup"><span data-stu-id="094d0-154">IPython provides a utility to do so; at a command prompt run the following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="094d0-155">This will prompt you for a password and confirmation, and will then print the password.</span><span class="sxs-lookup"><span data-stu-id="094d0-155">This will prompt you for a password and confirmation, and will then print the password.</span></span> <span data-ttu-id="094d0-156">Note this for the following step.</span><span class="sxs-lookup"><span data-stu-id="094d0-156">Note this for the following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided the rest for security)

<span data-ttu-id="094d0-157">Next, we will edit the profile's configuration file, which is the `jupyter_notebook_config.py` file in the directory you are in.</span><span class="sxs-lookup"><span data-stu-id="094d0-157">Next, we will edit the profile's configuration file, which is the `jupyter_notebook_config.py` file in the directory you are in.</span></span>  <span data-ttu-id="094d0-158">Note that this file may not exist -- just create it if that is the case.</span><span class="sxs-lookup"><span data-stu-id="094d0-158">Note that this file may not exist -- just create it if that is the case.</span></span>  <span data-ttu-id="094d0-159">This file has a number of fields and by default all are commented out.  You can open this file with any text editor of your liking, and you should ensure that it has at least the following content.</span><span class="sxs-lookup"><span data-stu-id="094d0-159">This file has a number of fields and by default all are commented out.  You can open this file with any text editor of your liking, and you should ensure that it has at least the following content.</span></span> <span data-ttu-id="094d0-160">**Be sure to replace the c.NotebookApp.password in the config with the sha1 from the previous step**.</span><span class="sxs-lookup"><span data-stu-id="094d0-160">**Be sure to replace the c.NotebookApp.password in the config with the sha1 from the previous step**.</span></span>

    c = get_config()

    # You must give the path to the certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-the-jupyter-notebook"></a><span data-ttu-id="094d0-161">Run the Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="094d0-161">Run the Jupyter Notebook</span></span>
<span data-ttu-id="094d0-162">At this point we are ready to start the Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="094d0-162">At this point we are ready to start the Jupyter Notebook.</span></span> <span data-ttu-id="094d0-163">To do this, navigate to the directory you want to store notebooks in and start the Jupyter Notebook server with the following command.</span><span class="sxs-lookup"><span data-stu-id="094d0-163">To do this, navigate to the directory you want to store notebooks in and start the Jupyter Notebook server with the following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="094d0-164">You should now be able to access your Jupyter Notebook at the address `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="094d0-164">You should now be able to access your Jupyter Notebook at the address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="094d0-165">When you first access your notebook, the login page asks for your password.</span><span class="sxs-lookup"><span data-stu-id="094d0-165">When you first access your notebook, the login page asks for your password.</span></span> <span data-ttu-id="094d0-166">And once you log in, you will see the "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span><span class="sxs-lookup"><span data-stu-id="094d0-166">And once you log in, you will see the "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="094d0-167">From this page you can create new notebooks and open existing ones.</span><span class="sxs-lookup"><span data-stu-id="094d0-167">From this page you can create new notebooks and open existing ones.</span></span>

![Screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-the-jupyter-notebook"></a><span data-ttu-id="094d0-169">Using the Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="094d0-169">Using the Jupyter Notebook</span></span>
<span data-ttu-id="094d0-170">If you click the **New** button, you will see the following opening page.</span><span class="sxs-lookup"><span data-stu-id="094d0-170">If you click the **New** button, you will see the following opening page.</span></span>

![Screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="094d0-172">The area marked with an `In []:` prompt is the input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on the "Play" icon (the right-pointing triangle in the toolbar).</span><span class="sxs-lookup"><span data-stu-id="094d0-172">The area marked with an `In []:` prompt is the input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on the "Play" icon (the right-pointing triangle in the toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="094d0-173">A powerful paradigm: live computational documents with rich media</span><span class="sxs-lookup"><span data-stu-id="094d0-173">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="094d0-174">The notebook itself should feel very natural to anyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing the style of a cell from "Code" to "Markdown" using the drop-down menu in the toolbar.</span><span class="sxs-lookup"><span data-stu-id="094d0-174">The notebook itself should feel very natural to anyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing the style of a cell from "Code" to "Markdown" using the drop-down menu in the toolbar.</span></span>

<span data-ttu-id="094d0-175">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span><span class="sxs-lookup"><span data-stu-id="094d0-175">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="094d0-176">You can mix, text, code, videos and more!</span><span class="sxs-lookup"><span data-stu-id="094d0-176">You can mix, text, code, videos and more!</span></span>

![Screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="094d0-178">And with the power of Python's many excellent libraries for scientific and technical computing, in the following screenshot, a simple calculation can be performed with the same ease as a complex network analysis, all in one environment.</span><span class="sxs-lookup"><span data-stu-id="094d0-178">And with the power of Python's many excellent libraries for scientific and technical computing, in the following screenshot, a simple calculation can be performed with the same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="094d0-179">This paradigm of mixing the power of the modern web with live computation offers many possibilities, and is ideally suited for the cloud; the Notebook can be used:</span><span class="sxs-lookup"><span data-stu-id="094d0-179">This paradigm of mixing the power of the modern web with live computation offers many possibilities, and is ideally suited for the cloud; the Notebook can be used:</span></span>

* <span data-ttu-id="094d0-180">As a computational scratchpad to record exploratory work on a problem.</span><span class="sxs-lookup"><span data-stu-id="094d0-180">As a computational scratchpad to record exploratory work on a problem.</span></span>
* <span data-ttu-id="094d0-181">To share results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span><span class="sxs-lookup"><span data-stu-id="094d0-181">To share results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="094d0-182">To distribute and present live teaching materials that involve computation, so students can immediately experiment with the real code, modify it and re-execute it interactively.</span><span class="sxs-lookup"><span data-stu-id="094d0-182">To distribute and present live teaching materials that involve computation, so students can immediately experiment with the real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="094d0-183">To provide "executable papers" that present the results of research in a way that can be immediately reproduced, validated and extended by others.</span><span class="sxs-lookup"><span data-stu-id="094d0-183">To provide "executable papers" that present the results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="094d0-184">As a platform for collaborative computing: multiple users can log in to the same notebook server to share a live computational session.</span><span class="sxs-lookup"><span data-stu-id="094d0-184">As a platform for collaborative computing: multiple users can log in to the same notebook server to share a live computational session.</span></span>

<span data-ttu-id="094d0-185">If you go to the IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span><span class="sxs-lookup"><span data-stu-id="094d0-185">If you go to the IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="094d0-186">Simply download the `.ipynb` files from the site and upload them onto the dashboard of your notebook Azure VM (or download them directly into the VM).</span><span class="sxs-lookup"><span data-stu-id="094d0-186">Simply download the `.ipynb` files from the site and upload them onto the dashboard of your notebook Azure VM (or download them directly into the VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="094d0-187">Conclusion</span><span class="sxs-lookup"><span data-stu-id="094d0-187">Conclusion</span></span>
<span data-ttu-id="094d0-188">The Jupyter Notebook provides a powerful interface for accessing interactively the power of the Python ecosystem on Azure.</span><span class="sxs-lookup"><span data-stu-id="094d0-188">The Jupyter Notebook provides a powerful interface for accessing interactively the power of the Python ecosystem on Azure.</span></span>  <span data-ttu-id="094d0-189">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span><span class="sxs-lookup"><span data-stu-id="094d0-189">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="094d0-190">The resulting Notebook documents contain a complete record of the computations that are performed and can be shared with other Jupyter users.</span><span class="sxs-lookup"><span data-stu-id="094d0-190">The resulting Notebook documents contain a complete record of the computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="094d0-191">The Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span><span class="sxs-lookup"><span data-stu-id="094d0-191">The Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="094d0-192">The core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="094d0-192">The core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="094d0-193">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span><span class="sxs-lookup"><span data-stu-id="094d0-193">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="094d0-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="094d0-194">Next steps</span></span>
<span data-ttu-id="094d0-195">For more information, see the [Python Developer Center](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="094d0-195">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs






