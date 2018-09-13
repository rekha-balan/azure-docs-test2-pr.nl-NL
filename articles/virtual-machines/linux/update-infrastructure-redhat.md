---
title: Red Hat Update Infrastructure (RHUI) | Microsoft Docs
description: Learn about Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux instances in Microsoft Azure
services: virtual-machines-linux
documentationcenter: ''
author: BorisB2015
manager: timlt
editor: ''
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: aa61c684dbdb9a7e1a9254b61c0383c6d04228af
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549965"
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="8bc28-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span><span class="sxs-lookup"><span data-stu-id="8bc28-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="8bc28-104">Virtual machines created from the on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered to access the Red Hat Update Infrastructure (RHUI) deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="8bc28-104">Virtual machines created from the on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered to access the Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="8bc28-105">The on-demand RHEL instances have access to a regional yum repository and able to receive incremental updates.</span><span class="sxs-lookup"><span data-stu-id="8bc28-105">The on-demand RHEL instances have access to a regional yum repository and able to receive incremental updates.</span></span>

<span data-ttu-id="8bc28-106">The yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span><span class="sxs-lookup"><span data-stu-id="8bc28-106">The yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="8bc28-107">You don't need to do any additional configuration - run `yum update` after your RHEL instance is ready to get the latest updates.</span><span class="sxs-lookup"><span data-stu-id="8bc28-107">You don't need to do any additional configuration - run `yum update` after your RHEL instance is ready to get the latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="8bc28-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of the older Azure RHUI.</span><span class="sxs-lookup"><span data-stu-id="8bc28-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of the older Azure RHUI.</span></span> <span data-ttu-id="8bc28-109">If you have been using the RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span><span class="sxs-lookup"><span data-stu-id="8bc28-109">If you have been using the RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="8bc28-110">If, however, you have older snapshots/VMs, their configuration needs to be updated for uninterrupted access to the Azure RHUI.</span><span class="sxs-lookup"><span data-stu-id="8bc28-110">If, however, you have older snapshots/VMs, their configuration needs to be updated for uninterrupted access to the Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="8bc28-111">RHUI Azure Infrastructure Update</span><span class="sxs-lookup"><span data-stu-id="8bc28-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="8bc28-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span><span class="sxs-lookup"><span data-stu-id="8bc28-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="8bc28-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.micrsoft.com) can be used by any VM regardless of region.</span><span class="sxs-lookup"><span data-stu-id="8bc28-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.micrsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="8bc28-114">The new RHEL Pay-As-You-Go (PAYG) images in the Azure Marketplace (versions dated September 2016 or later) point to the new Azure RHUI servers and do not require any additional action.</span><span class="sxs-lookup"><span data-stu-id="8bc28-114">The new RHEL Pay-As-You-Go (PAYG) images in the Azure Marketplace (versions dated September 2016 or later) point to the new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="8bc28-115">Determine if action is required</span><span class="sxs-lookup"><span data-stu-id="8bc28-115">Determine if action is required</span></span>
<span data-ttu-id="8bc28-116">If you are experiencing problems connecting to Azure RHUI from your Azure RHEL PAYG VM, follow these steps</span><span class="sxs-lookup"><span data-stu-id="8bc28-116">If you are experiencing problems connecting to Azure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="8bc28-117">Inspect VM configuration for Azure RHUI endpoint</span><span class="sxs-lookup"><span data-stu-id="8bc28-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="8bc28-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference to `rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of the file.</span><span class="sxs-lookup"><span data-stu-id="8bc28-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference to `rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of the file.</span></span> <span data-ttu-id="8bc28-119">If it is - you are using the new Azure RHUI.</span><span class="sxs-lookup"><span data-stu-id="8bc28-119">If it is - you are using the new Azure RHUI.</span></span>

    <span data-ttu-id="8bc28-120">If it pointing to a location with the following pattern `mirrorlist.*cds[1-4].cloudapp.net` - the configuration update is required.</span><span class="sxs-lookup"><span data-stu-id="8bc28-120">If it pointing to a location with the following pattern `mirrorlist.*cds[1-4].cloudapp.net` - the configuration update is required.</span></span>

    <span data-ttu-id="8bc28-121">If you are using the new configuration and still cannot connect to Azure RHUI - file a support case with Microsoft or Red Hat.</span><span class="sxs-lookup"><span data-stu-id="8bc28-121">If you are using the new configuration and still cannot connect to Azure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8bc28-122">Access to Azure-hosted RHUI is limited to the VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="8bc28-122">Access to Azure-hosted RHUI is limited to the VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="8bc28-123">If the old Azure RHUI is still available when you do this check and you would like to automatically update the configuration, execute the following command:</span><span class="sxs-lookup"><span data-stu-id="8bc28-123">If the old Azure RHUI is still available when you do this check and you would like to automatically update the configuration, execute the following command:</span></span>

    <span data-ttu-id="8bc28-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on the RHEL family version.</span><span class="sxs-lookup"><span data-stu-id="8bc28-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on the RHEL family version.</span></span>

3. <span data-ttu-id="8bc28-125">If you can no longer connect to the old Azure RHUI, follow the manual steps described in the next section.</span><span class="sxs-lookup"><span data-stu-id="8bc28-125">If you can no longer connect to the old Azure RHUI, follow the manual steps described in the next section.</span></span>

4. <span data-ttu-id="8bc28-126">Make sure to update the configuration on the source image/snapshot affected VM was provisioned from.</span><span class="sxs-lookup"><span data-stu-id="8bc28-126">Make sure to update the configuration on the source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-the-old-azure-rhui"></a><span data-ttu-id="8bc28-127">Phased shutdown of the old Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="8bc28-127">Phased shutdown of the old Azure RHUI</span></span>
<span data-ttu-id="8bc28-128">During the shutdown of the old Azure RHUI we restrict access to it as follows:</span><span class="sxs-lookup"><span data-stu-id="8bc28-128">During the shutdown of the old Azure RHUI we restrict access to it as follows:</span></span>

1. <span data-ttu-id="8bc28-129">Further restrict access (ACL) to set of IP addresses that are already connecting to it.</span><span class="sxs-lookup"><span data-stu-id="8bc28-129">Further restrict access (ACL) to set of IP addresses that are already connecting to it.</span></span> <span data-ttu-id="8bc28-130">Possible side-effects: if you continue using the old Azure RHUI - your new VMs may not be able to connect to it.</span><span class="sxs-lookup"><span data-stu-id="8bc28-130">Possible side-effects: if you continue using the old Azure RHUI - your new VMs may not be able to connect to it.</span></span> <span data-ttu-id="8bc28-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing to connect to the old Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="8bc28-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing to connect to the old Azure RHUI</span></span>

2. <span data-ttu-id="8bc28-132">Shutdown of mirror content delivery servers.</span><span class="sxs-lookup"><span data-stu-id="8bc28-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="8bc28-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until the point when you can no longer connect to the old Azure RHUI.</span><span class="sxs-lookup"><span data-stu-id="8bc28-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until the point when you can no longer connect to the old Azure RHUI.</span></span>

### <a name="the-ips-for-the-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="8bc28-134">The IPs for the new RHUI content delivery servers are</span><span class="sxs-lookup"><span data-stu-id="8bc28-134">The IPs for the new RHUI content delivery servers are</span></span>
<span data-ttu-id="8bc28-135">If you are using network configuration to further restrict access from RHEL PAYG VMs, make sure the following IPs are allowed for `yum update` to work depending on the environment you are in.</span><span class="sxs-lookup"><span data-stu-id="8bc28-135">If you are using network configuration to further restrict access from RHEL PAYG VMs, make sure the following IPs are allowed for `yum update` to work depending on the environment you are in.</span></span> 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-to-use-the-new-azure-rhui-servers"></a><span data-ttu-id="8bc28-136">Manual update procedure to use the new Azure RHUI servers</span><span class="sxs-lookup"><span data-stu-id="8bc28-136">Manual update procedure to use the new Azure RHUI servers</span></span>
<span data-ttu-id="8bc28-137">Download (via curl) the public key signature</span><span class="sxs-lookup"><span data-stu-id="8bc28-137">Download (via curl) the public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="8bc28-138">Verify the downloaded key</span><span class="sxs-lookup"><span data-stu-id="8bc28-138">Verify the downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="8bc28-139">Check the output, verify `keyid` and `user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="8bc28-139">Check the output, verify `keyid` and `user ID packet`:</span></span>

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

<span data-ttu-id="8bc28-140">Install the public key</span><span class="sxs-lookup"><span data-stu-id="8bc28-140">Install the public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="8bc28-141">Download, Verify, and Install Client RPM</span><span class="sxs-lookup"><span data-stu-id="8bc28-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="8bc28-142">Download: For RHEL 6</span><span class="sxs-lookup"><span data-stu-id="8bc28-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="8bc28-143">For RHEL 7</span><span class="sxs-lookup"><span data-stu-id="8bc28-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="8bc28-144">Verify:</span><span class="sxs-lookup"><span data-stu-id="8bc28-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="8bc28-145">Check in output that signature of the package is OK</span><span class="sxs-lookup"><span data-stu-id="8bc28-145">Check in output that signature of the package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="8bc28-146">Install the RPM</span><span class="sxs-lookup"><span data-stu-id="8bc28-146">Install the RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="8bc28-147">Upon completion, verify that you can access Azure RHUI form the VM</span><span class="sxs-lookup"><span data-stu-id="8bc28-147">Upon completion, verify that you can access Azure RHUI form the VM</span></span>

### <a name="all-in-one-script-for-automating-the-preceding-task"></a><span data-ttu-id="8bc28-148">All-in-one script for automating the preceding task</span><span class="sxs-lookup"><span data-stu-id="8bc28-148">All-in-one script for automating the preceding task</span></span>
<span data-ttu-id="8bc28-149">Use the following script as needed to automate the task of updating affected VMs to the new Azure RHUI servers.</span><span class="sxs-lookup"><span data-stu-id="8bc28-149">Use the following script as needed to automate the task of updating affected VMs to the new Azure RHUI servers.</span></span>

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a><span data-ttu-id="8bc28-150">RHUI overview</span><span class="sxs-lookup"><span data-stu-id="8bc28-150">RHUI overview</span></span>
<span data-ttu-id="8bc28-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution to manage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span><span class="sxs-lookup"><span data-stu-id="8bc28-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution to manage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="8bc28-152">Based on the upstream Pulp project, RHUI allows cloud providers to locally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available to a large group of end users through a load-balanced content delivery system.</span><span class="sxs-lookup"><span data-stu-id="8bc28-152">Based on the upstream Pulp project, RHUI allows cloud providers to locally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available to a large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="8bc28-153">Regions where RHUI is available</span><span class="sxs-lookup"><span data-stu-id="8bc28-153">Regions where RHUI is available</span></span>
<span data-ttu-id="8bc28-154">RHUI is available in all regions where RHEL on-demand images are available.</span><span class="sxs-lookup"><span data-stu-id="8bc28-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="8bc28-155">It currently includes all public regions listed on the [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span><span class="sxs-lookup"><span data-stu-id="8bc28-155">It currently includes all public regions listed on the [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="8bc28-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span><span class="sxs-lookup"><span data-stu-id="8bc28-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="8bc28-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in the future.</span><span class="sxs-lookup"><span data-stu-id="8bc28-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="8bc28-158">Access to Azure-hosted RHUI is limited to the VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="8bc28-158">Access to Azure-hosted RHUI is limited to the VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="8bc28-159">Get updates from another update repository</span><span class="sxs-lookup"><span data-stu-id="8bc28-159">Get updates from another update repository</span></span>
<span data-ttu-id="8bc28-160">If you need to get updates from a different update repository (instead of Azure-hosted RHUI), first you need to unregister your instances from RHUI.</span><span class="sxs-lookup"><span data-stu-id="8bc28-160">If you need to get updates from a different update repository (instead of Azure-hosted RHUI), first you need to unregister your instances from RHUI.</span></span> <span data-ttu-id="8bc28-161">Then you need to re-register them with the desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span><span class="sxs-lookup"><span data-stu-id="8bc28-161">Then you need to re-register them with the desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="8bc28-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="8bc28-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="8bc28-163">To unregister RHUI and reregister to your update infrastructure follow these steps:</span><span class="sxs-lookup"><span data-stu-id="8bc28-163">To unregister RHUI and reregister to your update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="8bc28-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` to `enabled=0`.</span><span class="sxs-lookup"><span data-stu-id="8bc28-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` to `enabled=0`.</span></span> <span data-ttu-id="8bc28-165">For example:</span><span class="sxs-lookup"><span data-stu-id="8bc28-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="8bc28-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` to `enabled=1`.</span><span class="sxs-lookup"><span data-stu-id="8bc28-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` to `enabled=1`.</span></span>
3. <span data-ttu-id="8bc28-167">Then register with the desired infrastructure, such as Red Hat Customer Portal.</span><span class="sxs-lookup"><span data-stu-id="8bc28-167">Then register with the desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="8bc28-168">Follow Red Hat solution guide on [how to register and subscribe a system to the Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span><span class="sxs-lookup"><span data-stu-id="8bc28-168">Follow Red Hat solution guide on [how to register and subscribe a system to the Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="8bc28-169">Access to the Azure-hosted RHUI is included in the RHEL Pay-As-You-Go (PAYG) image price.</span><span class="sxs-lookup"><span data-stu-id="8bc28-169">Access to the Azure-hosted RHUI is included in the RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="8bc28-170">Unregistering a PAYG RHEL VM from the Azure-hosted RHUI does not convert the virtual machine into Bring-Your-Own-License (BYOL) type VM.</span><span class="sxs-lookup"><span data-stu-id="8bc28-170">Unregistering a PAYG RHEL VM from the Azure-hosted RHUI does not convert the virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="8bc28-171">If you register the same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and the second time for Red Hat subscription(s).</span><span class="sxs-lookup"><span data-stu-id="8bc28-171">If you register the same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and the second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="8bc28-172">If you consistently need to use an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span><span class="sxs-lookup"><span data-stu-id="8bc28-172">If you consistently need to use an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="8bc28-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="8bc28-173">Next steps</span></span>
<span data-ttu-id="8bc28-174">To create a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span><span class="sxs-lookup"><span data-stu-id="8bc28-174">To create a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="8bc28-175">You will be able to use `yum update` in your RHEL instance without any additional setup.</span><span class="sxs-lookup"><span data-stu-id="8bc28-175">You will be able to use `yum update` in your RHEL instance without any additional setup.</span></span>

