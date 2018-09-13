---
title: Install Python and the SDK - Azure
description: Learn how to install Python and the SDK to use with Azure.
services: ''
documentationcenter: python
author: lmazuel
manager: wpickett
editor: ''
ms.assetid: f36294be-daeb-4caf-9129-fce18130f552
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 09/06/2016
ms.author: lmazuel
ms.openlocfilehash: 200eb40c021e31f0005374e64405cf711c72b061
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552717"
---
# <a name="installing-python-and-the-sdk"></a><span data-ttu-id="9d2ef-103">Installing Python and the SDK</span><span class="sxs-lookup"><span data-stu-id="9d2ef-103">Installing Python and the SDK</span></span>
<span data-ttu-id="9d2ef-104">Python is easy to setup on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="9d2ef-104">Python is easy to setup on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="9d2ef-105">This guide walks you through installation and getting your machine ready for use with Azure.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-the-python-azure-sdk"></a><span data-ttu-id="9d2ef-106">What's in the Python Azure SDK?</span><span class="sxs-lookup"><span data-stu-id="9d2ef-106">What's in the Python Azure SDK?</span></span>
<span data-ttu-id="9d2ef-107">The Azure SDK for Python includes components that allow you to develop, deploy, and manage Python applications for Azure.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-107">The Azure SDK for Python includes components that allow you to develop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="9d2ef-108">Specifically, the Azure SDK for Python includes the following:</span><span class="sxs-lookup"><span data-stu-id="9d2ef-108">Specifically, the Azure SDK for Python includes the following:</span></span>

* <span data-ttu-id="9d2ef-109">**Management libraries**.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-109">**Management libraries**.</span></span> <span data-ttu-id="9d2ef-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="9d2ef-111">**Runtime libraries**.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-111">**Runtime libraries**.</span></span> <span data-ttu-id="9d2ef-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="9d2ef-113">Which Python and which version to use</span><span class="sxs-lookup"><span data-stu-id="9d2ef-113">Which Python and which version to use</span></span>
<span data-ttu-id="9d2ef-114">There are several flavors of Python interpreters available - examples include:</span><span class="sxs-lookup"><span data-stu-id="9d2ef-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="9d2ef-115">CPython - the standard and most commonly used Python interpreter</span><span class="sxs-lookup"><span data-stu-id="9d2ef-115">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="9d2ef-116">PyPy - fast, compliant alternative implementation to CPython</span><span class="sxs-lookup"><span data-stu-id="9d2ef-116">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="9d2ef-117">IronPython - Python interpreter that runs on .Net/CLR</span><span class="sxs-lookup"><span data-stu-id="9d2ef-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="9d2ef-118">Jython - Python interpreter that runs on the Java Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="9d2ef-118">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="9d2ef-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="9d2ef-120">Where to get Python?</span><span class="sxs-lookup"><span data-stu-id="9d2ef-120">Where to get Python?</span></span>
<span data-ttu-id="9d2ef-121">There are several ways to get CPython:</span><span class="sxs-lookup"><span data-stu-id="9d2ef-121">There are several ways to get CPython:</span></span>

* <span data-ttu-id="9d2ef-122">Directly from [www.python.org][www.python.org]</span><span class="sxs-lookup"><span data-stu-id="9d2ef-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="9d2ef-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span><span class="sxs-lookup"><span data-stu-id="9d2ef-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="9d2ef-124">Build from source!</span><span class="sxs-lookup"><span data-stu-id="9d2ef-124">Build from source!</span></span>

<span data-ttu-id="9d2ef-125">Unless you have a specific need, we recommend the first two options.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-125">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="9d2ef-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span><span class="sxs-lookup"><span data-stu-id="9d2ef-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="9d2ef-127">If you already have Python installed, you can use pip to install a bundle of all the client libraries in your existing Python 2.7 or Python 3.3+ environment.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-127">If you already have Python installed, you can use pip to install a bundle of all the client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="9d2ef-128">This will download the packages from the [Python Package Index][Python Package Index] (PyPI).</span><span class="sxs-lookup"><span data-stu-id="9d2ef-128">This will download the packages from the [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="9d2ef-129">You may need administrator rights:</span><span class="sxs-lookup"><span data-stu-id="9d2ef-129">You may need administrator rights:</span></span>

* <span data-ttu-id="9d2ef-130">Linux and MacOS, use the `sudo` command: `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-130">Linux and MacOS, use the `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="9d2ef-131">Windows: open your PowerShell/Command prompt as an administrator</span><span class="sxs-lookup"><span data-stu-id="9d2ef-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="9d2ef-132">You can install individually each library for each Azure service:</span><span class="sxs-lookup"><span data-stu-id="9d2ef-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install the latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="9d2ef-133">Preview packages can be installed using the `--pre` flag:</span><span class="sxs-lookup"><span data-stu-id="9d2ef-133">Preview packages can be installed using the `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="9d2ef-134">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-134">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span> <span data-ttu-id="9d2ef-135">Since not all packages in this meta-package are published as stable yet, the `azure` meta-package is still in preview.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-135">Since not all packages in this meta-package are published as stable yet, the `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="9d2ef-136">However, the core packages, from code quality/completeness perspectives can be considered "stable" at this time</span><span class="sxs-lookup"><span data-stu-id="9d2ef-136">However, the core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="9d2ef-137">it will be officially labeled as such in sync with other languages as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-137">it will be officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="9d2ef-138">We are not planning on any further major changes until then.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="9d2ef-139">Since it's a preview release, you need to use the `--pre` flag:</span><span class="sxs-lookup"><span data-stu-id="9d2ef-139">Since it's a preview release, you need to use the `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="9d2ef-140">or directly</span><span class="sxs-lookup"><span data-stu-id="9d2ef-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="9d2ef-141">Getting More Packages</span><span class="sxs-lookup"><span data-stu-id="9d2ef-141">Getting More Packages</span></span>
<span data-ttu-id="9d2ef-142">The [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-142">The [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="9d2ef-143">If you chose to install a Distro, you'll already have most of the interesting bits for various scenarios from web development to Technical Computing.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-143">If you chose to install a Distro, you'll already have most of the interesting bits for various scenarios from web development to Technical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="9d2ef-144">Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9d2ef-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="9d2ef-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span><span class="sxs-lookup"><span data-stu-id="9d2ef-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![how-to-install-python-ptvs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="9d2ef-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="9d2ef-148">PTVS also makes it easy to deploy to Microsoft Azure, with support for deployment to [Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="9d2ef-148">PTVS also makes it easy to deploy to Microsoft Azure, with support for deployment to [Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="9d2ef-149">PTVS works with your existing Visual Studio 2013 or 2015 installation.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-149">PTVS works with your existing Visual Studio 2013 or 2015 installation.</span></span>  <span data-ttu-id="9d2ef-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="9d2ef-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="9d2ef-151">Python Azure Scenarios for Linux and MacOS</span><span class="sxs-lookup"><span data-stu-id="9d2ef-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="9d2ef-152">For Linux or MacOS, main Azure scenarios that are supported:</span><span class="sxs-lookup"><span data-stu-id="9d2ef-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="9d2ef-153">Consuming Azure Services by using the client libraries for Python</span><span class="sxs-lookup"><span data-stu-id="9d2ef-153">Consuming Azure Services by using the client libraries for Python</span></span>
2. <span data-ttu-id="9d2ef-154">Running your app in a Linux VM</span><span class="sxs-lookup"><span data-stu-id="9d2ef-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="9d2ef-155">Developing and publishing to Azure Websites using Git</span><span class="sxs-lookup"><span data-stu-id="9d2ef-155">Developing and publishing to Azure Websites using Git</span></span>

<span data-ttu-id="9d2ef-156">The first scenario enables you to author rich web apps that take advantage of the Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/storage-python-how-to-use-queue-storage.md), [table storage](storage/storage-python-how-to-use-table-storage.md) etc. via Pythonic wrappers for the Azure REST APIs.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-156">The first scenario enables you to author rich web apps that take advantage of the Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/storage-python-how-to-use-queue-storage.md), [table storage](storage/storage-python-how-to-use-table-storage.md) etc. via Pythonic wrappers for the Azure REST APIs.</span></span> <span data-ttu-id="9d2ef-157">These works identically on Windows, Mac, and Linux.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-157">These works identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="9d2ef-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="9d2ef-159">For the VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-159">For the VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="9d2ef-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser to a Linux or Windows multi-proc VM running the IPython Engine on Azure.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser to a Linux or Windows multi-proc VM running the IPython Engine on Azure.</span></span> <span data-ttu-id="9d2ef-161">See the [IPython Notebook on Azure](virtual-machines/linux/jupyter-notebook.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial for more information.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-161">See the [IPython Notebook on Azure](virtual-machines/linux/jupyter-notebook.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial for more information.</span></span>

<span data-ttu-id="9d2ef-162">For information on how to setup a Linux VM, please see the [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-162">For information on how to setup a Linux VM, please see the [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="9d2ef-163">Using Git deployment, you can develop a Python web application and publish it to an Azure Website from any operating system.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-163">Using Git deployment, you can develop a Python web application and publish it to an Azure Website from any operating system.</span></span>  <span data-ttu-id="9d2ef-164">When you push your repository to Azure, it will automatically create a virtual environment and pip install your required packages.</span><span class="sxs-lookup"><span data-stu-id="9d2ef-164">When you push your repository to Azure, it will automatically create a virtual environment and pip install your required packages.</span></span>

<span data-ttu-id="9d2ef-165">For more information on developing and publishing Azure Websites, see the tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="9d2ef-165">For more information on developing and publishing Azure Websites, see the tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="9d2ef-166">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span><span class="sxs-lookup"><span data-stu-id="9d2ef-166">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="9d2ef-167">Additional Software and Resources:</span><span class="sxs-lookup"><span data-stu-id="9d2ef-167">Additional Software and Resources:</span></span>
* [<span data-ttu-id="9d2ef-168">Azure SDK for Python ReadTheDocs</span><span class="sxs-lookup"><span data-stu-id="9d2ef-168">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="9d2ef-169">Azure SDK for Python GitHub</span><span class="sxs-lookup"><span data-stu-id="9d2ef-169">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="9d2ef-170">Official Azure samples for Python</span><span class="sxs-lookup"><span data-stu-id="9d2ef-170">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="9d2ef-171">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="9d2ef-171">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="9d2ef-172">[Enthought Python Distribution][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="9d2ef-172">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="9d2ef-173">[ActiveState Python Distribution][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="9d2ef-173">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="9d2ef-174">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="9d2ef-174">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="9d2ef-175">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="9d2ef-175">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="9d2ef-176">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="9d2ef-176">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="9d2ef-177">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="9d2ef-177">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* [<span data-ttu-id="9d2ef-178">IPython Notebook on Azure</span><span class="sxs-lookup"><span data-stu-id="9d2ef-178">IPython Notebook on Azure</span></span>](virtual-machines/linux/jupyter-notebook.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="9d2ef-179">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="9d2ef-179">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="9d2ef-180">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="9d2ef-180">Python Developer Center</span></span>](/develop/python/)

[Continuum Analytics Python Distribution]: http://continuum.io
[Enthought Python Distribution]: http://www.enthought.com
[ActiveState Python Distribution]: http://www.activestate.com
[www.python.org]: http://www.python.org
[www.continuum.io]: http://continuum.io
[www.enthought.com]: http://www.enthought.com
[www.activestate.com]: http://www.activestate.com
[SciPy - A suite of Scientific Python libraries]: http://www.scipy.org
[NumPy - A numerics library for Python]: http://www.numpy.org
[Django Project - A mature web framework/CMS]: http://www.djangoproject.com
[IPython - an advanced REPL/Notebook for Python]: http://ipython.org
[IPython]: http://ipython.org
[IPython Notebook on Azure]: virtual-machines-linux-jupyter-notebook.md
[Cloud Services]: cloud-services-python-ptvs.md
[Websites]: web-sites-python-ptvs-django-mysql.md
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio on GitHub]: https://github.com/microsoft/ptvs
[Python Package Index]: http://pypi.python.org/pypi
[Microsoft Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?LinkId=254281
[Microsoft Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?LinkID=516990
[Setting up a Linux VM via the Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How to use the Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]: storage-python-how-to-use-blob-storage.md

