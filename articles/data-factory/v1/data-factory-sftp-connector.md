---
title: Move data from SFTP server using Azure Data Factory | Microsoft Docs
description: Learn about how to move data from an on-premises or a cloud SFTP server using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 02/12/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: c22d2cba23e8bae965fa7c5746c9fff69ad3fa9e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968810"
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a><span data-ttu-id="f4d26-103">Move data from an SFTP server using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f4d26-103">Move data from an SFTP server using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-sftp-connector.md)
> * [Version 2 (current version)](../connector-sftp.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [SFTPconnector in V2](../connector-sftp.md).

<span data-ttu-id="f4d26-108">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud SFTP server to a supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="f4d26-108">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud SFTP server to a supported sink data store.</span></span> <span data-ttu-id="f4d26-109">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span><span class="sxs-lookup"><span data-stu-id="f4d26-109">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="f4d26-110">Data factory currently supports only moving data from an SFTP server to other data stores, but not for moving data from other data stores to an SFTP server.</span><span class="sxs-lookup"><span data-stu-id="f4d26-110">Data factory currently supports only moving data from an SFTP server to other data stores, but not for moving data from other data stores to an SFTP server.</span></span> <span data-ttu-id="f4d26-111">It supports both on-premises and cloud SFTP servers.</span><span class="sxs-lookup"><span data-stu-id="f4d26-111">It supports both on-premises and cloud SFTP servers.</span></span>

> [!NOTE]
> Copy Activity does not delete the source file after it is successfully copied to the destination. If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline. 

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="f4d26-114">Supported scenarios and authentication types</span><span class="sxs-lookup"><span data-stu-id="f4d26-114">Supported scenarios and authentication types</span></span>
<span data-ttu-id="f4d26-115">You can use this SFTP connector to copy data from **both cloud SFTP servers and on-premises SFTP servers**.</span><span class="sxs-lookup"><span data-stu-id="f4d26-115">You can use this SFTP connector to copy data from **both cloud SFTP servers and on-premises SFTP servers**.</span></span> <span data-ttu-id="f4d26-116">**Basic** and **SshPublicKey** authentication types are supported when connecting to the SFTP server.</span><span class="sxs-lookup"><span data-stu-id="f4d26-116">**Basic** and **SshPublicKey** authentication types are supported when connecting to the SFTP server.</span></span>

<span data-ttu-id="f4d26-117">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span><span class="sxs-lookup"><span data-stu-id="f4d26-117">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span></span> <span data-ttu-id="f4d26-118">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on the gateway.</span><span class="sxs-lookup"><span data-stu-id="f4d26-118">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on the gateway.</span></span> <span data-ttu-id="f4d26-119">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway and using it.</span><span class="sxs-lookup"><span data-stu-id="f4d26-119">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway and using it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f4d26-120">Getting started</span><span class="sxs-lookup"><span data-stu-id="f4d26-120">Getting started</span></span>
<span data-ttu-id="f4d26-121">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="f4d26-121">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="f4d26-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="f4d26-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="f4d26-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="f4d26-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

- <span data-ttu-id="f4d26-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="f4d26-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f4d26-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="f4d26-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> <span data-ttu-id="f4d26-126">For JSON samples to copy data from SFTP server to Azure Blob Storage, see [JSON Example: Copy data from SFTP server to Azure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="f4d26-126">For JSON samples to copy data from SFTP server to Azure Blob Storage, see [JSON Example: Copy data from SFTP server to Azure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f4d26-127">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="f4d26-127">Linked service properties</span></span>
<span data-ttu-id="f4d26-128">The following table provides description for JSON elements specific to FTP linked service.</span><span class="sxs-lookup"><span data-stu-id="f4d26-128">The following table provides description for JSON elements specific to FTP linked service.</span></span>

| <span data-ttu-id="f4d26-129">Property</span><span class="sxs-lookup"><span data-stu-id="f4d26-129">Property</span></span> | <span data-ttu-id="f4d26-130">Description</span><span class="sxs-lookup"><span data-stu-id="f4d26-130">Description</span></span> | <span data-ttu-id="f4d26-131">Required</span><span class="sxs-lookup"><span data-stu-id="f4d26-131">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f4d26-132">type</span><span class="sxs-lookup"><span data-stu-id="f4d26-132">type</span></span> | <span data-ttu-id="f4d26-133">The type property must be set to `Sftp`.</span><span class="sxs-lookup"><span data-stu-id="f4d26-133">The type property must be set to `Sftp`.</span></span> |<span data-ttu-id="f4d26-134">Yes</span><span class="sxs-lookup"><span data-stu-id="f4d26-134">Yes</span></span> |
| <span data-ttu-id="f4d26-135">host</span><span class="sxs-lookup"><span data-stu-id="f4d26-135">host</span></span> | <span data-ttu-id="f4d26-136">Name or IP address of the SFTP server.</span><span class="sxs-lookup"><span data-stu-id="f4d26-136">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="f4d26-137">Yes</span><span class="sxs-lookup"><span data-stu-id="f4d26-137">Yes</span></span> |
| <span data-ttu-id="f4d26-138">port</span><span class="sxs-lookup"><span data-stu-id="f4d26-138">port</span></span> |<span data-ttu-id="f4d26-139">Port on which the SFTP server is listening.</span><span class="sxs-lookup"><span data-stu-id="f4d26-139">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="f4d26-140">The default value is: 21</span><span class="sxs-lookup"><span data-stu-id="f4d26-140">The default value is: 21</span></span> |<span data-ttu-id="f4d26-141">No</span><span class="sxs-lookup"><span data-stu-id="f4d26-141">No</span></span> |
| <span data-ttu-id="f4d26-142">authenticationType</span><span class="sxs-lookup"><span data-stu-id="f4d26-142">authenticationType</span></span> |<span data-ttu-id="f4d26-143">Specify authentication type.</span><span class="sxs-lookup"><span data-stu-id="f4d26-143">Specify authentication type.</span></span> <span data-ttu-id="f4d26-144">Allowed values: **Basic**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="f4d26-144">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="f4d26-145">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span><span class="sxs-lookup"><span data-stu-id="f4d26-145">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="f4d26-146">Yes</span><span class="sxs-lookup"><span data-stu-id="f4d26-146">Yes</span></span> |
| <span data-ttu-id="f4d26-147">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="f4d26-147">skipHostKeyValidation</span></span> | <span data-ttu-id="f4d26-148">Specify whether to skip host key validation.</span><span class="sxs-lookup"><span data-stu-id="f4d26-148">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="f4d26-149">No.</span><span class="sxs-lookup"><span data-stu-id="f4d26-149">No.</span></span> <span data-ttu-id="f4d26-150">The default value: false</span><span class="sxs-lookup"><span data-stu-id="f4d26-150">The default value: false</span></span> |
| <span data-ttu-id="f4d26-151">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="f4d26-151">hostKeyFingerprint</span></span> | <span data-ttu-id="f4d26-152">Specify the finger print of the host key.</span><span class="sxs-lookup"><span data-stu-id="f4d26-152">Specify the finger print of the host key.</span></span> | <span data-ttu-id="f4d26-153">Yes if the `skipHostKeyValidation` is set to false.</span><span class="sxs-lookup"><span data-stu-id="f4d26-153">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="f4d26-154">gatewayName</span><span class="sxs-lookup"><span data-stu-id="f4d26-154">gatewayName</span></span> |<span data-ttu-id="f4d26-155">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span><span class="sxs-lookup"><span data-stu-id="f4d26-155">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="f4d26-156">Yes if copying data from an on-premises SFTP server.</span><span class="sxs-lookup"><span data-stu-id="f4d26-156">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="f4d26-157">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="f4d26-157">encryptedCredential</span></span> | <span data-ttu-id="f4d26-158">Encrypted credential to access the SFTP server.</span><span class="sxs-lookup"><span data-stu-id="f4d26-158">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="f4d26-159">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span><span class="sxs-lookup"><span data-stu-id="f4d26-159">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="f4d26-160">No.</span><span class="sxs-lookup"><span data-stu-id="f4d26-160">No.</span></span> <span data-ttu-id="f4d26-161">Apply only when copying data from an on-premises SFTP server.</span><span class="sxs-lookup"><span data-stu-id="f4d26-161">Apply only when copying data from an on-premises SFTP server.</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="f4d26-162">Using basic authentication</span><span class="sxs-lookup"><span data-stu-id="f4d26-162">Using basic authentication</span></span>

<span data-ttu-id="f4d26-163">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span><span class="sxs-lookup"><span data-stu-id="f4d26-163">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="f4d26-164">Property</span><span class="sxs-lookup"><span data-stu-id="f4d26-164">Property</span></span> | <span data-ttu-id="f4d26-165">Description</span><span class="sxs-lookup"><span data-stu-id="f4d26-165">Description</span></span> | <span data-ttu-id="f4d26-166">Required</span><span class="sxs-lookup"><span data-stu-id="f4d26-166">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f4d26-167">username</span><span class="sxs-lookup"><span data-stu-id="f4d26-167">username</span></span> | <span data-ttu-id="f4d26-168">User who has access to the SFTP server.</span><span class="sxs-lookup"><span data-stu-id="f4d26-168">User who has access to the SFTP server.</span></span> |<span data-ttu-id="f4d26-169">Yes</span><span class="sxs-lookup"><span data-stu-id="f4d26-169">Yes</span></span> |
| <span data-ttu-id="f4d26-170">password</span><span class="sxs-lookup"><span data-stu-id="f4d26-170">password</span></span> | <span data-ttu-id="f4d26-171">Password for the user (username).</span><span class="sxs-lookup"><span data-stu-id="f4d26-171">Password for the user (username).</span></span> | <span data-ttu-id="f4d26-172">Yes</span><span class="sxs-lookup"><span data-stu-id="f4d26-172">Yes</span></span> |

#### <a name="example-basic-authentication"></a><span data-ttu-id="f4d26-173">Example: Basic authentication</span><span class="sxs-lookup"><span data-stu-id="f4d26-173">Example: Basic authentication</span></span>
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="f4d26-174">Example: Basic authentication with encrypted credential</span><span class="sxs-lookup"><span data-stu-id="f4d26-174">Example: Basic authentication with encrypted credential</span></span>

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="f4d26-175">Using SSH public key authentication</span><span class="sxs-lookup"><span data-stu-id="f4d26-175">Using SSH public key authentication</span></span>

<span data-ttu-id="f4d26-176">To use SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span><span class="sxs-lookup"><span data-stu-id="f4d26-176">To use SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="f4d26-177">Property</span><span class="sxs-lookup"><span data-stu-id="f4d26-177">Property</span></span> | <span data-ttu-id="f4d26-178">Description</span><span class="sxs-lookup"><span data-stu-id="f4d26-178">Description</span></span> | <span data-ttu-id="f4d26-179">Required</span><span class="sxs-lookup"><span data-stu-id="f4d26-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f4d26-180">username</span><span class="sxs-lookup"><span data-stu-id="f4d26-180">username</span></span> |<span data-ttu-id="f4d26-181">User who has access to the SFTP server</span><span class="sxs-lookup"><span data-stu-id="f4d26-181">User who has access to the SFTP server</span></span> |<span data-ttu-id="f4d26-182">Yes</span><span class="sxs-lookup"><span data-stu-id="f4d26-182">Yes</span></span> |
| <span data-ttu-id="f4d26-183">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="f4d26-183">privateKeyPath</span></span> | <span data-ttu-id="f4d26-184">Specify absolute path to the private key file that gateway can access.</span><span class="sxs-lookup"><span data-stu-id="f4d26-184">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="f4d26-185">Specify either the `privateKeyPath` or `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="f4d26-185">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="f4d26-186">Apply only when copying data from an on-premises SFTP server.</span><span class="sxs-lookup"><span data-stu-id="f4d26-186">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="f4d26-187">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="f4d26-187">privateKeyContent</span></span> | <span data-ttu-id="f4d26-188">A serialized string of the private key content.</span><span class="sxs-lookup"><span data-stu-id="f4d26-188">A serialized string of the private key content.</span></span> <span data-ttu-id="f4d26-189">The Copy Wizard can read the private key file and extract the private key content automatically.</span><span class="sxs-lookup"><span data-stu-id="f4d26-189">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="f4d26-190">If you are using any other tool/SDK, use the privateKeyPath property instead.</span><span class="sxs-lookup"><span data-stu-id="f4d26-190">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="f4d26-191">Specify either the `privateKeyPath` or `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="f4d26-191">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="f4d26-192">passPhrase</span><span class="sxs-lookup"><span data-stu-id="f4d26-192">passPhrase</span></span> | <span data-ttu-id="f4d26-193">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span><span class="sxs-lookup"><span data-stu-id="f4d26-193">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="f4d26-194">Yes if the private key file is protected by a pass phrase.</span><span class="sxs-lookup"><span data-stu-id="f4d26-194">Yes if the private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> SFTP connector supports RSA/DSA OpenSSH key. Make sure your key file content starts with "-----BEGIN [RSA/DSA] PRIVATE KEY-----". If the private key file is a ppk-format file, please use Putty tool to convert from .ppk to OpenSSH format.

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a><span data-ttu-id="f4d26-198">Example: SshPublicKey authentication using private key filePath</span><span class="sxs-lookup"><span data-stu-id="f4d26-198">Example: SshPublicKey authentication using private key filePath</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="f4d26-199">Example: SshPublicKey authentication using private key content</span><span class="sxs-lookup"><span data-stu-id="f4d26-199">Example: SshPublicKey authentication using private key content</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of the private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="f4d26-200">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="f4d26-200">Dataset properties</span></span>
<span data-ttu-id="f4d26-201">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="f4d26-201">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f4d26-202">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span><span class="sxs-lookup"><span data-stu-id="f4d26-202">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="f4d26-203">The **typeProperties** section is different for each type of dataset.</span><span class="sxs-lookup"><span data-stu-id="f4d26-203">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="f4d26-204">It provides information that is specific to the dataset type.</span><span class="sxs-lookup"><span data-stu-id="f4d26-204">It provides information that is specific to the dataset type.</span></span> <span data-ttu-id="f4d26-205">The typeProperties section for a dataset of type **FileShare** dataset has the following properties:</span><span class="sxs-lookup"><span data-stu-id="f4d26-205">The typeProperties section for a dataset of type **FileShare** dataset has the following properties:</span></span>

| <span data-ttu-id="f4d26-206">Property</span><span class="sxs-lookup"><span data-stu-id="f4d26-206">Property</span></span> | <span data-ttu-id="f4d26-207">Description</span><span class="sxs-lookup"><span data-stu-id="f4d26-207">Description</span></span> | <span data-ttu-id="f4d26-208">Required</span><span class="sxs-lookup"><span data-stu-id="f4d26-208">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4d26-209">folderPath</span><span class="sxs-lookup"><span data-stu-id="f4d26-209">folderPath</span></span> |<span data-ttu-id="f4d26-210">Sub path to the folder.</span><span class="sxs-lookup"><span data-stu-id="f4d26-210">Sub path to the folder.</span></span> <span data-ttu-id="f4d26-211">Use escape character ‘ \ ’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="f4d26-211">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="f4d26-212">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="f4d26-212">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="f4d26-213">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span><span class="sxs-lookup"><span data-stu-id="f4d26-213">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="f4d26-214">Yes</span><span class="sxs-lookup"><span data-stu-id="f4d26-214">Yes</span></span> |
| <span data-ttu-id="f4d26-215">fileName</span><span class="sxs-lookup"><span data-stu-id="f4d26-215">fileName</span></span> |<span data-ttu-id="f4d26-216">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span><span class="sxs-lookup"><span data-stu-id="f4d26-216">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="f4d26-217">If you do not specify any value for this property, the table points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="f4d26-217">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="f4d26-218">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span><span class="sxs-lookup"><span data-stu-id="f4d26-218">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="f4d26-219">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="f4d26-219">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="f4d26-220">No</span><span class="sxs-lookup"><span data-stu-id="f4d26-220">No</span></span> |
| <span data-ttu-id="f4d26-221">fileFilter</span><span class="sxs-lookup"><span data-stu-id="f4d26-221">fileFilter</span></span> |<span data-ttu-id="f4d26-222">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span><span class="sxs-lookup"><span data-stu-id="f4d26-222">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="f4d26-223">Allowed values are: `*` (multiple characters) and `?` (single character).</span><span class="sxs-lookup"><span data-stu-id="f4d26-223">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="f4d26-224">Examples 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="f4d26-224">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="f4d26-225">Example 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="f4d26-225">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="f4d26-226">fileFilter is applicable for an input FileShare dataset.</span><span class="sxs-lookup"><span data-stu-id="f4d26-226">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="f4d26-227">This property is not supported with HDFS.</span><span class="sxs-lookup"><span data-stu-id="f4d26-227">This property is not supported with HDFS.</span></span> |<span data-ttu-id="f4d26-228">No</span><span class="sxs-lookup"><span data-stu-id="f4d26-228">No</span></span> |
| <span data-ttu-id="f4d26-229">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="f4d26-229">partitionedBy</span></span> |<span data-ttu-id="f4d26-230">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="f4d26-230">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="f4d26-231">For example, folderPath parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="f4d26-231">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="f4d26-232">No</span><span class="sxs-lookup"><span data-stu-id="f4d26-232">No</span></span> |
| <span data-ttu-id="f4d26-233">format</span><span class="sxs-lookup"><span data-stu-id="f4d26-233">format</span></span> | <span data-ttu-id="f4d26-234">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="f4d26-234">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="f4d26-235">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="f4d26-235">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="f4d26-236">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="f4d26-236">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="f4d26-237">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="f4d26-237">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="f4d26-238">No</span><span class="sxs-lookup"><span data-stu-id="f4d26-238">No</span></span> |
| <span data-ttu-id="f4d26-239">compression</span><span class="sxs-lookup"><span data-stu-id="f4d26-239">compression</span></span> | <span data-ttu-id="f4d26-240">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="f4d26-240">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="f4d26-241">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="f4d26-241">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="f4d26-242">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="f4d26-242">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="f4d26-243">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="f4d26-243">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="f4d26-244">No</span><span class="sxs-lookup"><span data-stu-id="f4d26-244">No</span></span> |
| <span data-ttu-id="f4d26-245">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="f4d26-245">useBinaryTransfer</span></span> |<span data-ttu-id="f4d26-246">Specify whether use Binary transfer mode.</span><span class="sxs-lookup"><span data-stu-id="f4d26-246">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="f4d26-247">True for binary mode and false ASCII.</span><span class="sxs-lookup"><span data-stu-id="f4d26-247">True for binary mode and false ASCII.</span></span> <span data-ttu-id="f4d26-248">Default value: True.</span><span class="sxs-lookup"><span data-stu-id="f4d26-248">Default value: True.</span></span> <span data-ttu-id="f4d26-249">This property can only be used when associated linked service type is of type: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="f4d26-249">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="f4d26-250">No</span><span class="sxs-lookup"><span data-stu-id="f4d26-250">No</span></span> |

> [!NOTE]
> filename and fileFilter cannot be used simultaneously.

### <a name="using-partionedby-property"></a><span data-ttu-id="f4d26-252">Using partionedBy property</span><span class="sxs-lookup"><span data-stu-id="f4d26-252">Using partionedBy property</span></span>
<span data-ttu-id="f4d26-253">As mentioned in the previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="f4d26-253">As mentioned in the previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span></span> <span data-ttu-id="f4d26-254">You can do so with the Data Factory macros and the system variable SliceStart, SliceEnd that indicate the logical time period for a given data slice.</span><span class="sxs-lookup"><span data-stu-id="f4d26-254">You can do so with the Data Factory macros and the system variable SliceStart, SliceEnd that indicate the logical time period for a given data slice.</span></span>

<span data-ttu-id="f4d26-255">To learn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span><span class="sxs-lookup"><span data-stu-id="f4d26-255">To learn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="f4d26-256">Sample 1:</span><span class="sxs-lookup"><span data-stu-id="f4d26-256">Sample 1:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="f4d26-257">In this example {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span><span class="sxs-lookup"><span data-stu-id="f4d26-257">In this example {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="f4d26-258">The SliceStart refers to start time of the slice.</span><span class="sxs-lookup"><span data-stu-id="f4d26-258">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="f4d26-259">The folderPath is different for each slice.</span><span class="sxs-lookup"><span data-stu-id="f4d26-259">The folderPath is different for each slice.</span></span> <span data-ttu-id="f4d26-260">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="f4d26-260">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="f4d26-261">Sample 2:</span><span class="sxs-lookup"><span data-stu-id="f4d26-261">Sample 2:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="f4d26-262">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span><span class="sxs-lookup"><span data-stu-id="f4d26-262">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="f4d26-263">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="f4d26-263">Copy activity properties</span></span>
<span data-ttu-id="f4d26-264">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="f4d26-264">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f4d26-265">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="f4d26-265">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="f4d26-266">Whereas, the properties available in the typeProperties section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="f4d26-266">Whereas, the properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="f4d26-267">For Copy activity, the type properties vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="f4d26-267">For Copy activity, the type properties vary depending on the types of sources and sinks.</span></span>

[!INCLUDE [data-factory-file-system-source](../../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="f4d26-268">Supported file and compression formats</span><span class="sxs-lookup"><span data-stu-id="f4d26-268">Supported file and compression formats</span></span>
<span data-ttu-id="f4d26-269">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span><span class="sxs-lookup"><span data-stu-id="f4d26-269">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-sftp-server-to-azure-blob"></a><span data-ttu-id="f4d26-270">JSON Example: Copy data from SFTP server to Azure blob</span><span class="sxs-lookup"><span data-stu-id="f4d26-270">JSON Example: Copy data from SFTP server to Azure blob</span></span>
<span data-ttu-id="f4d26-271">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f4d26-271">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f4d26-272">They show how to copy data from SFTP source to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f4d26-272">They show how to copy data from SFTP source to Azure Blob Storage.</span></span> <span data-ttu-id="f4d26-273">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f4d26-273">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> This sample provides JSON snippets. It does not include step-by-step instructions for creating the data factory. See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.

<span data-ttu-id="f4d26-277">The sample has the following data factory entities:</span><span class="sxs-lookup"><span data-stu-id="f4d26-277">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="f4d26-278">A linked service of type [sftp](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f4d26-278">A linked service of type [sftp](#linked-service-properties).</span></span>
* <span data-ttu-id="f4d26-279">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f4d26-279">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="f4d26-280">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f4d26-280">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="f4d26-281">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f4d26-281">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="f4d26-282">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f4d26-282">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f4d26-283">The sample copies data from an SFTP server to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="f4d26-283">The sample copies data from an SFTP server to an Azure blob every hour.</span></span> <span data-ttu-id="f4d26-284">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="f4d26-284">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="f4d26-285">**SFTP linked service**</span><span class="sxs-lookup"><span data-stu-id="f4d26-285">**SFTP linked service**</span></span>

<span data-ttu-id="f4d26-286">This example uses the basic authentication with user name and password in plain text.</span><span class="sxs-lookup"><span data-stu-id="f4d26-286">This example uses the basic authentication with user name and password in plain text.</span></span> <span data-ttu-id="f4d26-287">You can also use one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="f4d26-287">You can also use one of the following ways:</span></span>

* <span data-ttu-id="f4d26-288">Basic authentication with encrypted credentials</span><span class="sxs-lookup"><span data-stu-id="f4d26-288">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="f4d26-289">SSH public key authentication</span><span class="sxs-lookup"><span data-stu-id="f4d26-289">SSH public key authentication</span></span>

<span data-ttu-id="f4d26-290">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span><span class="sxs-lookup"><span data-stu-id="f4d26-290">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
<span data-ttu-id="f4d26-291">**Azure Storage linked service**</span><span class="sxs-lookup"><span data-stu-id="f4d26-291">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="f4d26-292">**SFTP input dataset**</span><span class="sxs-lookup"><span data-stu-id="f4d26-292">**SFTP input dataset**</span></span>

<span data-ttu-id="f4d26-293">This dataset refers to the SFTP folder `mysharedfolder` and file `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="f4d26-293">This dataset refers to the SFTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="f4d26-294">The pipeline copies the file to the destination.</span><span class="sxs-lookup"><span data-stu-id="f4d26-294">The pipeline copies the file to the destination.</span></span>

<span data-ttu-id="f4d26-295">Setting "external": "true" informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="f4d26-295">Setting "external": "true" informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="f4d26-296">**Azure Blob output dataset**</span><span class="sxs-lookup"><span data-stu-id="f4d26-296">**Azure Blob output dataset**</span></span>

<span data-ttu-id="f4d26-297">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="f4d26-297">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f4d26-298">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="f4d26-298">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="f4d26-299">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="f4d26-299">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="f4d26-300">**Pipeline with Copy activity**</span><span class="sxs-lookup"><span data-stu-id="f4d26-300">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="f4d26-301">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="f4d26-301">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="f4d26-302">In the pipeline JSON definition, the **source** type is set to **FileSystemSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f4d26-302">In the pipeline JSON definition, the **source** type is set to **FileSystemSource** and **sink** type is set to **BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a><span data-ttu-id="f4d26-303">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="f4d26-303">Performance and Tuning</span></span>
<span data-ttu-id="f4d26-304">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="f4d26-304">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4d26-305">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f4d26-305">Next Steps</span></span>
<span data-ttu-id="f4d26-306">See the following articles:</span><span class="sxs-lookup"><span data-stu-id="f4d26-306">See the following articles:</span></span>

* <span data-ttu-id="f4d26-307">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="f4d26-307">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
