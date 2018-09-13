---
title: Linux HPC Pack cluster options in the cloud | Microsoft Docs
description: Learn about options with Microsoft HPC Pack to create and manage a Linux high performance computing (HPC) cluster in the Azure cloud
services: virtual-machines-linux,cloud-services
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: eb1effae3f512d53da3acb168071161b8b756aa4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661007"
---
# <a name="options-with-hpc-pack-to-create-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a>Options with HPC Pack to create and manage an HPC cluster in Azure for Linux workloads
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

This article focuses on options to use HPC Pack to run Linux workloads. There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>Run an HPC Pack cluster in Azure VMs
### <a name="azure-templates"></a>Azure templates
* (GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)
* (Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)
* (Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)

### <a name="powershell-deployment-script"></a>PowerShell deployment script
* [Create a Linux HPC cluster with the HPC Pack IaaS deployment script](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Tutorials
* [Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a>Cluster management
* [Submit jobs to an HPC Pack cluster in Azure](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Job management in HPC Pack](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>Create RDMA clusters for MPI workloads
* [Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

