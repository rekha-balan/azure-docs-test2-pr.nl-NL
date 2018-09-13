---
title: Copy data from SFTP server using Azure Data Factory | Microsoft Docs
description: Learn about MySQL connector in Azure Data Factory that lets you copy data from an SFTP server to a data store supported as a sink.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 04/27/2018
ms.author: jingwang
ms.openlocfilehash: 3425558ac1ffa9e8d5146a5126f01c4ac55050dc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866213"
---
# <a name="copy-data-from-sftp-server-using-azure-data-factory"></a><span data-ttu-id="805e7-103">Copy data from SFTP server using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="805e7-103">Copy data from SFTP server using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-sftp-connector.md)
> * [Current version](connector-sftp.md)

<span data-ttu-id="805e7-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from an SFTP server.</span><span class="sxs-lookup"><span data-stu-id="805e7-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from an SFTP server.</span></span> <span data-ttu-id="805e7-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="805e7-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="805e7-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="805e7-108">Supported capabilities</span></span>

<span data-ttu-id="805e7-109">You can copy data from SFTP server to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="805e7-109">You can copy data from SFTP server to any supported sink data store.</span></span> <span data-ttu-id="805e7-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="805e7-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="805e7-111">Specifically, this SFTP connector supports:</span><span class="sxs-lookup"><span data-stu-id="805e7-111">Specifically, this SFTP connector supports:</span></span>

- <span data-ttu-id="805e7-112">Copying files using **Basic** or **SshPublicKey** authentication.</span><span class="sxs-lookup"><span data-stu-id="805e7-112">Copying files using **Basic** or **SshPublicKey** authentication.</span></span>
- <span data-ttu-id="805e7-113">Copying files as-is or parsing files with the [supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md).</span><span class="sxs-lookup"><span data-stu-id="805e7-113">Copying files as-is or parsing files with the [supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="805e7-114">Get started</span><span class="sxs-lookup"><span data-stu-id="805e7-114">Get started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="805e7-115">The following sections provide details about properties that are used to define Data Factory entities specific to SFTP.</span><span class="sxs-lookup"><span data-stu-id="805e7-115">The following sections provide details about properties that are used to define Data Factory entities specific to SFTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="805e7-116">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="805e7-116">Linked service properties</span></span>

<span data-ttu-id="805e7-117">The following properties are supported for SFTP linked service:</span><span class="sxs-lookup"><span data-stu-id="805e7-117">The following properties are supported for SFTP linked service:</span></span>

| <span data-ttu-id="805e7-118">Property</span><span class="sxs-lookup"><span data-stu-id="805e7-118">Property</span></span> | <span data-ttu-id="805e7-119">Description</span><span class="sxs-lookup"><span data-stu-id="805e7-119">Description</span></span> | <span data-ttu-id="805e7-120">Required</span><span class="sxs-lookup"><span data-stu-id="805e7-120">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="805e7-121">type</span><span class="sxs-lookup"><span data-stu-id="805e7-121">type</span></span> | <span data-ttu-id="805e7-122">The type property must be set to: **Sftp**.</span><span class="sxs-lookup"><span data-stu-id="805e7-122">The type property must be set to: **Sftp**.</span></span> |<span data-ttu-id="805e7-123">Yes</span><span class="sxs-lookup"><span data-stu-id="805e7-123">Yes</span></span> |
| <span data-ttu-id="805e7-124">host</span><span class="sxs-lookup"><span data-stu-id="805e7-124">host</span></span> | <span data-ttu-id="805e7-125">Name or IP address of the SFTP server.</span><span class="sxs-lookup"><span data-stu-id="805e7-125">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="805e7-126">Yes</span><span class="sxs-lookup"><span data-stu-id="805e7-126">Yes</span></span> |
| <span data-ttu-id="805e7-127">port</span><span class="sxs-lookup"><span data-stu-id="805e7-127">port</span></span> | <span data-ttu-id="805e7-128">Port on which the SFTP server is listening.</span><span class="sxs-lookup"><span data-stu-id="805e7-128">Port on which the SFTP server is listening.</span></span><br/><span data-ttu-id="805e7-129">Allowed values are: integer, default value is **22**.</span><span class="sxs-lookup"><span data-stu-id="805e7-129">Allowed values are: integer, default value is **22**.</span></span> |<span data-ttu-id="805e7-130">No</span><span class="sxs-lookup"><span data-stu-id="805e7-130">No</span></span> |
| <span data-ttu-id="805e7-131">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="805e7-131">skipHostKeyValidation</span></span> | <span data-ttu-id="805e7-132">Specify whether to skip host key validation.</span><span class="sxs-lookup"><span data-stu-id="805e7-132">Specify whether to skip host key validation.</span></span><br/><span data-ttu-id="805e7-133">Allowed values are: **true**, **false** (default).</span><span class="sxs-lookup"><span data-stu-id="805e7-133">Allowed values are: **true**, **false** (default).</span></span>  | <span data-ttu-id="805e7-134">No</span><span class="sxs-lookup"><span data-stu-id="805e7-134">No</span></span> |
| <span data-ttu-id="805e7-135">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="805e7-135">hostKeyFingerprint</span></span> | <span data-ttu-id="805e7-136">Specify the finger print of the host key.</span><span class="sxs-lookup"><span data-stu-id="805e7-136">Specify the finger print of the host key.</span></span> | <span data-ttu-id="805e7-137">Yes if the "skipHostKeyValidation" is set to false.</span><span class="sxs-lookup"><span data-stu-id="805e7-137">Yes if the "skipHostKeyValidation" is set to false.</span></span>  |
| <span data-ttu-id="805e7-138">authenticationType</span><span class="sxs-lookup"><span data-stu-id="805e7-138">authenticationType</span></span> | <span data-ttu-id="805e7-139">Specify authentication type.</span><span class="sxs-lookup"><span data-stu-id="805e7-139">Specify authentication type.</span></span><br/><span data-ttu-id="805e7-140">Allowed values are: **Basic**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="805e7-140">Allowed values are: **Basic**, **SshPublicKey**.</span></span> <span data-ttu-id="805e7-141">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span><span class="sxs-lookup"><span data-stu-id="805e7-141">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="805e7-142">Yes</span><span class="sxs-lookup"><span data-stu-id="805e7-142">Yes</span></span> |
| <span data-ttu-id="805e7-143">connectVia</span><span class="sxs-lookup"><span data-stu-id="805e7-143">connectVia</span></span> | <span data-ttu-id="805e7-144">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="805e7-144">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="805e7-145">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span><span class="sxs-lookup"><span data-stu-id="805e7-145">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span></span> <span data-ttu-id="805e7-146">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="805e7-146">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="805e7-147">No</span><span class="sxs-lookup"><span data-stu-id="805e7-147">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="805e7-148">Using basic authentication</span><span class="sxs-lookup"><span data-stu-id="805e7-148">Using basic authentication</span></span>

<span data-ttu-id="805e7-149">To use basic authentication, set "authenticationType" property to **Basic**, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span><span class="sxs-lookup"><span data-stu-id="805e7-149">To use basic authentication, set "authenticationType" property to **Basic**, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="805e7-150">Property</span><span class="sxs-lookup"><span data-stu-id="805e7-150">Property</span></span> | <span data-ttu-id="805e7-151">Description</span><span class="sxs-lookup"><span data-stu-id="805e7-151">Description</span></span> | <span data-ttu-id="805e7-152">Required</span><span class="sxs-lookup"><span data-stu-id="805e7-152">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="805e7-153">userName</span><span class="sxs-lookup"><span data-stu-id="805e7-153">userName</span></span> | <span data-ttu-id="805e7-154">User who has access to the SFTP server.</span><span class="sxs-lookup"><span data-stu-id="805e7-154">User who has access to the SFTP server.</span></span> |<span data-ttu-id="805e7-155">Yes</span><span class="sxs-lookup"><span data-stu-id="805e7-155">Yes</span></span> |
| <span data-ttu-id="805e7-156">password</span><span class="sxs-lookup"><span data-stu-id="805e7-156">password</span></span> | <span data-ttu-id="805e7-157">Password for the user (userName).</span><span class="sxs-lookup"><span data-stu-id="805e7-157">Password for the user (userName).</span></span> <span data-ttu-id="805e7-158">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="805e7-158">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="805e7-159">Yes</span><span class="sxs-lookup"><span data-stu-id="805e7-159">Yes</span></span> |

<span data-ttu-id="805e7-160">**Example:**</span><span class="sxs-lookup"><span data-stu-id="805e7-160">**Example:**</span></span>

```json
{
    "apiVersion": "2017-09-01-preview",
    "name": "SftpLinkedService",
    "type": "linkedservices",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<sftp server>",
            "port": 22,
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "authenticationType": "Basic",
            "userName": "<username>",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="805e7-161">Using SSH public key authentication</span><span class="sxs-lookup"><span data-stu-id="805e7-161">Using SSH public key authentication</span></span>

<span data-ttu-id="805e7-162">To use SSH public key authentication, set "authenticationType" property as **SshPublicKey**, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span><span class="sxs-lookup"><span data-stu-id="805e7-162">To use SSH public key authentication, set "authenticationType" property as **SshPublicKey**, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="805e7-163">Property</span><span class="sxs-lookup"><span data-stu-id="805e7-163">Property</span></span> | <span data-ttu-id="805e7-164">Description</span><span class="sxs-lookup"><span data-stu-id="805e7-164">Description</span></span> | <span data-ttu-id="805e7-165">Required</span><span class="sxs-lookup"><span data-stu-id="805e7-165">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="805e7-166">userName</span><span class="sxs-lookup"><span data-stu-id="805e7-166">userName</span></span> | <span data-ttu-id="805e7-167">User who has access to the SFTP server</span><span class="sxs-lookup"><span data-stu-id="805e7-167">User who has access to the SFTP server</span></span> |<span data-ttu-id="805e7-168">Yes</span><span class="sxs-lookup"><span data-stu-id="805e7-168">Yes</span></span> |
| <span data-ttu-id="805e7-169">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="805e7-169">privateKeyPath</span></span> | <span data-ttu-id="805e7-170">Specify absolute path to the private key file that Integration Runtime can access.</span><span class="sxs-lookup"><span data-stu-id="805e7-170">Specify absolute path to the private key file that Integration Runtime can access.</span></span> <span data-ttu-id="805e7-171">Applies only when Self-hosted type of Integration Runtime is specified in "connectVia".</span><span class="sxs-lookup"><span data-stu-id="805e7-171">Applies only when Self-hosted type of Integration Runtime is specified in "connectVia".</span></span> | <span data-ttu-id="805e7-172">Specify either the `privateKeyPath` or `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="805e7-172">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span>  |
| <span data-ttu-id="805e7-173">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="805e7-173">privateKeyContent</span></span> | <span data-ttu-id="805e7-174">Base64 encoded SSH private key content.</span><span class="sxs-lookup"><span data-stu-id="805e7-174">Base64 encoded SSH private key content.</span></span> <span data-ttu-id="805e7-175">SSH private key should be OpenSSH format.</span><span class="sxs-lookup"><span data-stu-id="805e7-175">SSH private key should be OpenSSH format.</span></span> <span data-ttu-id="805e7-176">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="805e7-176">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="805e7-177">Specify either the `privateKeyPath` or `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="805e7-177">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="805e7-178">passPhrase</span><span class="sxs-lookup"><span data-stu-id="805e7-178">passPhrase</span></span> | <span data-ttu-id="805e7-179">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span><span class="sxs-lookup"><span data-stu-id="805e7-179">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> <span data-ttu-id="805e7-180">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="805e7-180">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="805e7-181">Yes if the private key file is protected by a pass phrase.</span><span class="sxs-lookup"><span data-stu-id="805e7-181">Yes if the private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> SFTP connector supports RSA/DSA OpenSSH key. Make sure your key file content starts with "-----BEGIN [RSA/DSA] PRIVATE KEY-----". If the private key file is a ppk-format file, please use Putty tool to convert from .ppk to OpenSSH format. 

<span data-ttu-id="805e7-185">**Example 1: SshPublicKey authentication using private key filePath**</span><span class="sxs-lookup"><span data-stu-id="805e7-185">**Example 1: SshPublicKey authentication using private key filePath**</span></span>

```json
{
    "apiVersion": "2017-09-01-preview",
    "name": "SftpLinkedService",
    "type": "Linkedservices",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<sftp server>",
            "port": 22,
            "skipHostKeyValidation": true,
            "authenticationType": "SshPublicKey",
            "userName": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": {
                "type": "SecureString",
                "value": "<pass phrase>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

<span data-ttu-id="805e7-186">**Example 2: SshPublicKey authentication using private key content**</span><span class="sxs-lookup"><span data-stu-id="805e7-186">**Example 2: SshPublicKey authentication using private key content**</span></span>

```json
{
    "apiVersion": "2017-09-01-preview",
    "name": "SftpLinkedService",
    "type": "Linkedservices",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<sftp server>",
            "port": 22,
            "skipHostKeyValidation": true,
            "authenticationType": "SshPublicKey",
            "userName": "<username>",
            "privateKeyContent": {
                "type": "SecureString",
                "value": "<base64 string of the private key content>"
            },
            "passPhrase": {
                "type": "SecureString",
                "value": "<pass phrase>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="805e7-187">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="805e7-187">Dataset properties</span></span>

<span data-ttu-id="805e7-188">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="805e7-188">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="805e7-189">This section provides a list of properties supported by SFTP dataset.</span><span class="sxs-lookup"><span data-stu-id="805e7-189">This section provides a list of properties supported by SFTP dataset.</span></span>

<span data-ttu-id="805e7-190">To copy data from SFTP, set the type property of the dataset to **FileShare**.</span><span class="sxs-lookup"><span data-stu-id="805e7-190">To copy data from SFTP, set the type property of the dataset to **FileShare**.</span></span> <span data-ttu-id="805e7-191">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="805e7-191">The following properties are supported:</span></span>

| <span data-ttu-id="805e7-192">Property</span><span class="sxs-lookup"><span data-stu-id="805e7-192">Property</span></span> | <span data-ttu-id="805e7-193">Description</span><span class="sxs-lookup"><span data-stu-id="805e7-193">Description</span></span> | <span data-ttu-id="805e7-194">Required</span><span class="sxs-lookup"><span data-stu-id="805e7-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="805e7-195">type</span><span class="sxs-lookup"><span data-stu-id="805e7-195">type</span></span> | <span data-ttu-id="805e7-196">The type property of the dataset must be set to: **FileShare**</span><span class="sxs-lookup"><span data-stu-id="805e7-196">The type property of the dataset must be set to: **FileShare**</span></span> |<span data-ttu-id="805e7-197">Yes</span><span class="sxs-lookup"><span data-stu-id="805e7-197">Yes</span></span> |
| <span data-ttu-id="805e7-198">folderPath</span><span class="sxs-lookup"><span data-stu-id="805e7-198">folderPath</span></span> | <span data-ttu-id="805e7-199">Path to the folder.</span><span class="sxs-lookup"><span data-stu-id="805e7-199">Path to the folder.</span></span> <span data-ttu-id="805e7-200">Wildcard filter is not supported.</span><span class="sxs-lookup"><span data-stu-id="805e7-200">Wildcard filter is not supported.</span></span> <span data-ttu-id="805e7-201">For example: folder/subfolder/</span><span class="sxs-lookup"><span data-stu-id="805e7-201">For example: folder/subfolder/</span></span> |<span data-ttu-id="805e7-202">Yes</span><span class="sxs-lookup"><span data-stu-id="805e7-202">Yes</span></span> |
| <span data-ttu-id="805e7-203">fileName</span><span class="sxs-lookup"><span data-stu-id="805e7-203">fileName</span></span> |  <span data-ttu-id="805e7-204">**Name or wildcard filter** for the file(s) under the specified "folderPath".</span><span class="sxs-lookup"><span data-stu-id="805e7-204">**Name or wildcard filter** for the file(s) under the specified "folderPath".</span></span> <span data-ttu-id="805e7-205">If you don't specify a value for this property, the dataset points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="805e7-205">If you don't specify a value for this property, the dataset points to all files in the folder.</span></span> <br/><br/><span data-ttu-id="805e7-206">For filter, allowed wildcards are: `*` (matches zero or more characters) and `?` (matches zero or single character).</span><span class="sxs-lookup"><span data-stu-id="805e7-206">For filter, allowed wildcards are: `*` (matches zero or more characters) and `?` (matches zero or single character).</span></span><br/><span data-ttu-id="805e7-207">- Example 1: `"fileName": "*.csv"`</span><span class="sxs-lookup"><span data-stu-id="805e7-207">- Example 1: `"fileName": "*.csv"`</span></span><br/><span data-ttu-id="805e7-208">- Example 2: `"fileName": "???20180427.txt"`</span><span class="sxs-lookup"><span data-stu-id="805e7-208">- Example 2: `"fileName": "???20180427.txt"`</span></span><br/><span data-ttu-id="805e7-209">Use `^` to escape if your actual file name has wildcard or this escape char inside.</span><span class="sxs-lookup"><span data-stu-id="805e7-209">Use `^` to escape if your actual file name has wildcard or this escape char inside.</span></span> |<span data-ttu-id="805e7-210">No</span><span class="sxs-lookup"><span data-stu-id="805e7-210">No</span></span> |
| <span data-ttu-id="805e7-211">format</span><span class="sxs-lookup"><span data-stu-id="805e7-211">format</span></span> | <span data-ttu-id="805e7-212">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="805e7-212">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span><br/><br/><span data-ttu-id="805e7-213">If you want to parse files with a specific format, the following file format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="805e7-213">If you want to parse files with a specific format, the following file format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="805e7-214">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="805e7-214">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="805e7-215">For more information, see [Text Format](supported-file-formats-and-compression-codecs.md#text-format), [Json Format](supported-file-formats-and-compression-codecs.md#json-format), [Avro Format](supported-file-formats-and-compression-codecs.md#avro-format), [Orc Format](supported-file-formats-and-compression-codecs.md#orc-format), and [Parquet Format](supported-file-formats-and-compression-codecs.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="805e7-215">For more information, see [Text Format](supported-file-formats-and-compression-codecs.md#text-format), [Json Format](supported-file-formats-and-compression-codecs.md#json-format), [Avro Format](supported-file-formats-and-compression-codecs.md#avro-format), [Orc Format](supported-file-formats-and-compression-codecs.md#orc-format), and [Parquet Format](supported-file-formats-and-compression-codecs.md#parquet-format) sections.</span></span> |<span data-ttu-id="805e7-216">No (only for binary copy scenario)</span><span class="sxs-lookup"><span data-stu-id="805e7-216">No (only for binary copy scenario)</span></span> |
| <span data-ttu-id="805e7-217">compression</span><span class="sxs-lookup"><span data-stu-id="805e7-217">compression</span></span> | <span data-ttu-id="805e7-218">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="805e7-218">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="805e7-219">For more information, see [Supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="805e7-219">For more information, see [Supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md#compression-support).</span></span><br/><span data-ttu-id="805e7-220">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="805e7-220">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span><br/><span data-ttu-id="805e7-221">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="805e7-221">Supported levels are: **Optimal** and **Fastest**.</span></span> |<span data-ttu-id="805e7-222">No</span><span class="sxs-lookup"><span data-stu-id="805e7-222">No</span></span> |

>[!TIP]
>To copy all files under a folder, specify **folderPath** only.<br>To copy a single file with a given name, specify **folderPath** with folder part and **fileName** with file name.<br>To copy a subset of files under a folder, specify **folderPath** with folder part and **fileName** with wildcard filter.

>[!NOTE]
>If you were using "fileFilter" property for file filter, it is still supported as-is, while you are suggested to use the new filter capability added to "fileName" going forward.

<span data-ttu-id="805e7-227">**Example:**</span><span class="sxs-lookup"><span data-stu-id="805e7-227">**Example:**</span></span>

```json
{
    "apiVersion": "2017-09-01-preview",
    "name": "SFTPDataset",
    "type": "Datasets",
    "properties": {
        "type": "FileShare",
        "linkedServiceName":{
            "referenceName": "<SFTP linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "folderPath": "folder/subfolder/",
            "fileName": "myfile.csv.gz",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            },
            "compression": {
                "type": "GZip",
                "level": "Optimal"
            }
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="805e7-228">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="805e7-228">Copy activity properties</span></span>

<span data-ttu-id="805e7-229">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="805e7-229">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="805e7-230">This section provides a list of properties supported by SFTP source.</span><span class="sxs-lookup"><span data-stu-id="805e7-230">This section provides a list of properties supported by SFTP source.</span></span>

### <a name="sftp-as-source"></a><span data-ttu-id="805e7-231">SFTP as source</span><span class="sxs-lookup"><span data-stu-id="805e7-231">SFTP as source</span></span>

<span data-ttu-id="805e7-232">To copy data from SFTP, set the source type in the copy activity to **FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="805e7-232">To copy data from SFTP, set the source type in the copy activity to **FileSystemSource**.</span></span> <span data-ttu-id="805e7-233">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="805e7-233">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="805e7-234">Property</span><span class="sxs-lookup"><span data-stu-id="805e7-234">Property</span></span> | <span data-ttu-id="805e7-235">Description</span><span class="sxs-lookup"><span data-stu-id="805e7-235">Description</span></span> | <span data-ttu-id="805e7-236">Required</span><span class="sxs-lookup"><span data-stu-id="805e7-236">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="805e7-237">type</span><span class="sxs-lookup"><span data-stu-id="805e7-237">type</span></span> | <span data-ttu-id="805e7-238">The type property of the copy activity source must be set to: **FileSystemSource**</span><span class="sxs-lookup"><span data-stu-id="805e7-238">The type property of the copy activity source must be set to: **FileSystemSource**</span></span> |<span data-ttu-id="805e7-239">Yes</span><span class="sxs-lookup"><span data-stu-id="805e7-239">Yes</span></span> |
| <span data-ttu-id="805e7-240">recursive</span><span class="sxs-lookup"><span data-stu-id="805e7-240">recursive</span></span> | <span data-ttu-id="805e7-241">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="805e7-241">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> <span data-ttu-id="805e7-242">Note when recursive is set to true and sink is file-based store, empty folder/sub-folder will not be copied/created at sink.</span><span class="sxs-lookup"><span data-stu-id="805e7-242">Note when recursive is set to true and sink is file-based store, empty folder/sub-folder will not be copied/created at sink.</span></span><br/><span data-ttu-id="805e7-243">Allowed values are: **true** (default), **false**</span><span class="sxs-lookup"><span data-stu-id="805e7-243">Allowed values are: **true** (default), **false**</span></span> | <span data-ttu-id="805e7-244">No</span><span class="sxs-lookup"><span data-stu-id="805e7-244">No</span></span> |

<span data-ttu-id="805e7-245">**Example:**</span><span class="sxs-lookup"><span data-stu-id="805e7-245">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromSFTP",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<SFTP input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "FileSystemSource",
                "recursive": true
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```


## <a name="next-steps"></a><span data-ttu-id="805e7-246">Next steps</span><span class="sxs-lookup"><span data-stu-id="805e7-246">Next steps</span></span>
<span data-ttu-id="805e7-247">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="805e7-247">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
