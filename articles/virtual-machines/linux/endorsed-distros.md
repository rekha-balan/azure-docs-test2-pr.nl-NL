---
title: Endorsed distributions of Linux | Microsoft Docs
description: Learn about Linux on Azure-endorsed distributions, including guidelines for Ubuntu, OpenLogic, Oracle, and SUSE.
services: virtual-machines-linux
documentationcenter: ''
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: 2777a526-c260-4cb9-a31a-bdfe1a55fffc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: f015c26f80eb0d164b86390426b42be08d723daa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553209"
---
# <a name="linux-on-azure-endorsed-distributions"></a>Linux on Azure-Endorsed Distributions
> [!NOTE]
> If you have a few moments, please help us to improve the Azure Linux VM documentation by taking this [quick survey](https://aka.ms/linuxdocsurvey) of your experiences. Every answer helps us help you get your work done.
> 
> 

The Linux images in the Azure Gallery or Marketplace are provided by a number of partners, and we are working with various Linux communities to add even more flavors to the Endorsed Distribution list. In the meantime, for distributions not available from the Gallery you can always Bring-Your-Own-Linux by following the guidelines on [this page](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="supported-distributions--versions"></a>Supported Distributions & Versions
The following table lists the Linux distributions and versions that are supported on Azure. Please also refer to [support for Linux images in Microsoft Azure](https://support.microsoft.com/en-us/kb/2941892) for more detailed information.

The Linux Integration Services (LIS) drivers for Hyper-V and Azure are kernel modules that Microsoft contributes directly to the upstream Linux kernel.  The LIS drivers are either built into the distribution's kernel by default, or for older RHEL/CentOS-based distributions are available as a separate download [here](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409).  Please see [this article](create-upload-generic.md#linux-kernel-requirements) for more information about the LIS drivers.

The Azure Linux Agent is already pre-installed on the Azure Gallery images and are typically available from the distribution's package repository.  Source code can be found on [GitHub](https://github.com/azure/walinuxagent).

| Distribution | Version | Drivers | Agent |
| --- | --- | --- | --- |
| CentOS by OpenLogic |CentOS 6.3+, 7.0+ |CentOS 6.3: [LIS Download](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409)<p>CentOS 6.4+: In Kernel |Package: In [OpenLogic repo](http://olcentgbl.trafficmanager.net/openlogic/6/openlogic/x86_64/RPMS/) under "WALinuxAgent" <br/>Source Code: [GitHub](https://github.com/Azure/WALinuxAgent) |
| [CoreOS](https://coreos.com/docs/running-coreos/cloud-providers/azure/) |494.4.0+ |In Kernel |Source Code: [GitHub](https://github.com/coreos/coreos-overlay/tree/master/app-emulation/wa-linux-agent) |
| Debian |Debian 7.9+, 8.2+ |In Kernel |Package: In repo under "waagent" <br/>Source Code: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Oracle Linux |6.4+, 7.0+ |In Kernel |Package: In repo under "WALinuxAgent" <br/>Source Code: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| Red Hat Enterprise Linux |RHEL 6.7+, 7.1+ |In Kernel |Package: In repo under "WALinuxAgent" <br/>Source Code: [GitHub](https://github.com/Azure/WALinuxAgent) |
| SUSE Linux Enterprise |SLES/SLES for SAP<br>11 SP4<br>12 SP1+|In Kernel |Package:<p> for 11 in [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools) repo<br>for 12 included in "Public Cloud" Module under "python-azure-agent"<br/>Source Code: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| openSUSE |openSUSE Leap 42.1+ |In Kernel |Package: In [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools) repo under "python-azure-agent" <br/>Source Code: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Ubuntu |Ubuntu 12.04, 14.04, 16.04, 16.10 |In Kernel |Package: In repo under "walinuxagent" <br/>Source Code: [GitHub](https://github.com/Azure/WALinuxAgent) |

## <a name="partners"></a>Partners
### <a name="openlogic"></a>OpenLogic
[http://www.openlogic.com/azure](http://www.openlogic.com/azure)

OpenLogic is a leading provider of enterprise open source solutions for the cloud and the data center. OpenLogic helps hundreds of leading enterprise across a wide range of industries to safely acquire, support, and control open source software. OpenLogic offers commercial-grade technical support and indemnification for 600 open source packages backed by the OpenLogic Expert Community, including enterprise level support for CentOS as well as being the launch partner for providing CentOS-based images on Azure.

### <a name="coreos"></a>CoreOS
[https://coreos.com/docs/running-coreos/cloud-providers/azure/](https://coreos.com/docs/running-coreos/cloud-providers/azure/)

From the CoreOS Website:

*CoreOS is designed for security, consistency, and reliability. Instead of installing packages via yum or apt, CoreOS uses Linux containers to manage your services at a higher level of abstraction. A single service's code and all dependencies are packaged within a container that can be run on one or many CoreOS machines.*

### <a name="credativ"></a>Credativ
[http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure](http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure)

Credativ is an independent consulting and services company, specializing in the development and implementation of professional solutions through the use of free software. As leading Open Source specialists, Credative has international recognition with many IT departments using their support. In conjunction with Microsoft, Credativ is currently preparing corresponding Debian images for Debian 8 (Jessie) and Debian before 7 (Wheezy), which are specially designed to run on Azure and can be easily managed via the platform. Credativ will also support the long term maintenance and updating of the Debian images for Azure through its Open Source Support Centers.

### <a name="oracle"></a>Oracle
[http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html)

Oracle’s strategy is to offer a broad portfolio of solutions for public and private clouds, while giving customers choice and flexibility in how they deploy Oracle software in Oracle clouds as well as other clouds.  Oracle’s partnership with Microsoft enables customers to deploy Oracle software in Microsoft public and private clouds with the confidence of certification and support from Oracle.  Oracle’s commitment and investment in Oracle public and private cloud solutions is unchanged.

### <a name="red-hat"></a>Red Hat
[http://www.redhat.com/en/partners/strategic-alliance/microsoft](http://www.redhat.com/en/partners/strategic-alliance/microsoft)

The world's leading provider of open source solutions, Red Hat helps more than 90% of Fortune 500 companies solve business challenges, align their IT and business strategies, and prepare for the future of technology. Red Hat does this by providing secure solutions through an open business model and an affordable, predictable subscription model.

### <a name="suse"></a>SUSE
[http://www.suse.com/suse-linux-enterprise-server-on-azure](http://www.suse.com/suse-linux-enterprise-server-on-azure)

SUSE Linux Enterprise Server on Azure is a proven platform that provides superior reliability and security for cloud computing. SUSE's versatile Linux platform seamlessly integrates with Azure cloud services to deliver an easily manageable cloud environment. And with more than 9,200 certified applications from over 1,800 independent software vendors for SUSE Linux Enterprise Server, SUSE ensures that workloads running supported in the data center can be confidently deployed on Azure.

### <a name="canonical"></a>Canonical
[http://www.ubuntu.com/cloud/azure](http://www.ubuntu.com/cloud/azure)

Canonical engineering and open community governance drive Ubuntu's success in client, server and cloud computing,  including personal cloud services for consumers. Canonical's vision of a unified free platform in Ubuntu, from phone to cloud, with a family of coherent interfaces for the phone, tablet, TV and desktop, makes Ubuntu the first choice for diverse institutions from public cloud providers to the makers of consumer electronics, and a favorite among individual technologists.

With developers and engineering centers around the world, Canonical is uniquely positioned to partner with hardware makers, content providers and software developers to bring Ubuntu solutions to market, from PCs to servers and handheld devices.
