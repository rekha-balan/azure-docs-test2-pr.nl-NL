---
title: Create an Oracle 12c Database on Azure VM | Microsoft Docs
description: Quickly get an Oracle 12c database up and running in your Azure environment.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: tonyguid
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/17/2017
ms.author: rclaus
ms.openlocfilehash: 3cf6625407afe5b4fb53a945f4a505338122aaec
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660583"
---
# <a name="create-an-oracle-12c-database-on-azure-vm"></a><span data-ttu-id="2f61c-103">Create an Oracle 12c Database on Azure VM</span><span class="sxs-lookup"><span data-stu-id="2f61c-103">Create an Oracle 12c Database on Azure VM</span></span>

<span data-ttu-id="2f61c-104">This script creates an Oracle 12c Database using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2f61c-104">This script creates an Oracle 12c Database using the Azure CLI.</span></span>

<span data-ttu-id="2f61c-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="2f61c-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="2f61c-106">This guide details using the Azure CLI to deploy an Oracle 12c Database from the Marketplace gallery image.</span><span class="sxs-lookup"><span data-stu-id="2f61c-106">This guide details using the Azure CLI to deploy an Oracle 12c Database from the Marketplace gallery image.</span></span>

<span data-ttu-id="2f61c-107">Before you start, make sure that the Azure CLI has been installed.</span><span class="sxs-lookup"><span data-stu-id="2f61c-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="2f61c-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2f61c-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="2f61c-109">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="2f61c-109">Log in to Azure</span></span> 

<span data-ttu-id="2f61c-110">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="2f61c-110">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="2f61c-111">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="2f61c-111">Create a resource group</span></span>

<span data-ttu-id="2f61c-112">Create a resource group with the [az group create](/cli/azure/group#create) command.</span><span class="sxs-lookup"><span data-stu-id="2f61c-112">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="2f61c-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="2f61c-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="2f61c-114">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span><span class="sxs-lookup"><span data-stu-id="2f61c-114">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="2f61c-115">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="2f61c-115">Create virtual machine</span></span>

<span data-ttu-id="2f61c-116">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span><span class="sxs-lookup"><span data-stu-id="2f61c-116">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="2f61c-117">The following example creates a VM named `myVM` and creates SSH keys if they do not already exist in a default key location.</span><span class="sxs-lookup"><span data-stu-id="2f61c-117">The following example creates a VM named `myVM` and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="2f61c-118">To use a specific set of keys, use the `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="2f61c-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli
az vm create --resource-group myResourceGroup --name myVM --image Oracle:Oracle-Database-Ee:12.1.0.2:latest --data-disk-sizes-gb 20 --size Standard_DS2_v2  --generate-ssh-keys
```

<span data-ttu-id="2f61c-119">When the VM has been created, the Azure CLI shows information similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="2f61c-119">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="2f61c-120">Take note of the `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="2f61c-120">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="2f61c-121">This address is used to access the VM.</span><span class="sxs-lookup"><span data-stu-id="2f61c-121">This address is used to access the VM.</span></span>

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="2f61c-122">Connect to virtual machine</span><span class="sxs-lookup"><span data-stu-id="2f61c-122">Connect to virtual machine</span></span>

<span data-ttu-id="2f61c-123">Use the following command to create an SSH session with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f61c-123">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="2f61c-124">Replace the IP address with the `publicIpAddress` of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f61c-124">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-database"></a><span data-ttu-id="2f61c-125">Create Database</span><span class="sxs-lookup"><span data-stu-id="2f61c-125">Create Database</span></span>

<span data-ttu-id="2f61c-126">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span><span class="sxs-lookup"><span data-stu-id="2f61c-126">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> <span data-ttu-id="2f61c-127">the first step is running as the 'oracle' superuser and initialize the listener for logging:</span><span class="sxs-lookup"><span data-stu-id="2f61c-127">the first step is running as the 'oracle' superuser and initialize the listener for logging:</span></span>

```bash
su oracle
Password: <enter initial oracle password: xxxxxxxx >
[oracle@myVM /]$ lsnrctl start
Copyright (c) 1991, 2014, Oracle.  All rights reserved.

Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

TNSLSNR for Linux: Version 12.1.0.2.0 - Production
Log messages written to /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
STATUS of the LISTENER
------------------------
Alias                     LISTENER
Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
Start Date                23-MAR-2017 15:32:08
Uptime                    0 days 0 hr. 0 min. 0 sec
Trace Level               off
Security                  ON: Local OS Authentication
SNMP                      OFF
Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
Listening Endpoints Summary...
  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
The listener supports no services
The command completed successfully
```

<span data-ttu-id="2f61c-128">The next step is to create the database:</span><span class="sxs-lookup"><span data-stu-id="2f61c-128">The next step is to create the database:</span></span>

```bash
[oracle@myVM /]$ dbca -silent -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 -sid cdb1 -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs

Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

## <a name="set-up-connectivity"></a><span data-ttu-id="2f61c-129">Set up Connectivity</span><span class="sxs-lookup"><span data-stu-id="2f61c-129">Set up Connectivity</span></span> 
<span data-ttu-id="2f61c-130">Test for local connectivity</span><span class="sxs-lookup"><span data-stu-id="2f61c-130">Test for local connectivity</span></span>

<span data-ttu-id="2f61c-131">Once we have created the database, we need to set the ORACLE_HOME and ORACLE_SID environment variables.</span><span class="sxs-lookup"><span data-stu-id="2f61c-131">Once we have created the database, we need to set the ORACLE_HOME and ORACLE_SID environment variables.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME

ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="2f61c-132">Now we can connect using sqlplus:</span><span class="sxs-lookup"><span data-stu-id="2f61c-132">Now we can connect using sqlplus:</span></span>

```bash
sqlplus / as sysdba

SQL*Plus: Release 12.1.0.2.0 Production on Fri Apr 7 13:16:30 2017

Copyright (c) 1982, 2014, Oracle.  All rights reserved.


Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

```

<span data-ttu-id="2f61c-133">The final thing is to configure the external endpoint.</span><span class="sxs-lookup"><span data-stu-id="2f61c-133">The final thing is to configure the external endpoint.</span></span> <span data-ttu-id="2f61c-134">We should exit the SSH session on the VM, as we need to configure the Azure Network Security Group protecting the VM.</span><span class="sxs-lookup"><span data-stu-id="2f61c-134">We should exit the SSH session on the VM, as we need to configure the Azure Network Security Group protecting the VM.</span></span> <span data-ttu-id="2f61c-135">We execute this with the Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="2f61c-135">We execute this with the Azure CLI:</span></span>

```bash
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmNSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="2f61c-136">Result should look similar to the following response:</span><span class="sxs-lookup"><span data-stu-id="2f61c-136">Result should look similar to the following response:</span></span>

```
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

<span data-ttu-id="2f61c-137">To test the external connectivity, run sqlplus on a remote pc.</span><span class="sxs-lookup"><span data-stu-id="2f61c-137">To test the external connectivity, run sqlplus on a remote pc.</span></span> <span data-ttu-id="2f61c-138">Before connecting, create a 'tnsnames.ora' file on that PC:</span><span class="sxs-lookup"><span data-stu-id="2f61c-138">Before connecting, create a 'tnsnames.ora' file on that PC:</span></span>

```
azure_pdb1=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<vm-name>.cloudapp.net)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=pdb1)
    )
  )
```


## <a name="delete-virtual-machine"></a><span data-ttu-id="2f61c-139">Delete virtual machine</span><span class="sxs-lookup"><span data-stu-id="2f61c-139">Delete virtual machine</span></span>

<span data-ttu-id="2f61c-140">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="2f61c-140">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="2f61c-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f61c-141">Next steps</span></span>

[<span data-ttu-id="2f61c-142">Create highly available virtual machines tutorial</span><span class="sxs-lookup"><span data-stu-id="2f61c-142">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="2f61c-143">Explore VM deployment CLI samples</span><span class="sxs-lookup"><span data-stu-id="2f61c-143">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
