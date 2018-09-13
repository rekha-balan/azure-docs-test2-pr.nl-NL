---
title: Desired State Configuration Resource Manager Template | Microsoft Docs
description: Resource Manager Template definition for Desired State Configuration in Azure with examples and troubleshooting
services: virtual-machines-windows
documentationcenter: ''
author: zjalexander
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
keywords: ''
ms.assetid: b5402e5a-1768-4075-8c19-b7f7402687af
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: ce9baacb761c06263cc25000c7597f8101bf1b85
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549144"
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="68845-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="68845-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="68845-104">This article describes the Resource Manager template for the [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68845-104">This article describes the Resource Manager template for the [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="68845-105">Template example for a Windows VM</span><span class="sxs-lookup"><span data-stu-id="68845-105">Template example for a Windows VM</span></span>
<span data-ttu-id="68845-106">The following snippet goes into the Resource section of the template.</span><span class="sxs-lookup"><span data-stu-id="68845-106">The following snippet goes into the Resource section of the template.</span></span>

```json
            "name": "Microsoft.Powershell.DSC",
            "type": "extensions",
             "location": "[resourceGroup().location]",
             "apiVersion": "2015-06-15",
             "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "dscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }

```

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="68845-107">Template example for Windows VMSS</span><span class="sxs-lookup"><span data-stu-id="68845-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="68845-108">A VMSS node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span><span class="sxs-lookup"><span data-stu-id="68845-108">A VMSS node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="68845-109">DSC is added under "extensions".</span><span class="sxs-lookup"><span data-stu-id="68845-109">DSC is added under "extensions".</span></span> 

```json
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": true,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
```

## <a name="detailed-settings-information"></a><span data-ttu-id="68845-110">Detailed Settings Information</span><span class="sxs-lookup"><span data-stu-id="68845-110">Detailed Settings Information</span></span>
<span data-ttu-id="68845-111">The following schema is for the settings portion of the Azure DSC extension in an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="68845-111">The following schema is for the settings portion of the Azure DSC extension in an Azure Resource Manager template.</span></span>

```json

"settings": {
  "wmfVersion": "latest",
  "configuration": {
    "url": "http://validURLToConfigLocation",
    "script": "ConfigurationScript.ps1",
    "function": "ConfigurationFunction"
  },
  "configurationArguments": {
    "argument1": "Value1",
    "argument2": "Value2"
  },
  "configurationData": {
    "url": "https://foo.psd1"
  },
  "privacy": {
    "dataCollection": "enable"
  },
  "advancedOptions": {
    "downloadMappings": {
      "customWmfLocation": "http://myWMFlocation"
    }
  } 
},
"protectedSettings": {
  "configurationArguments": {
    "parameterOfTypePSCredential1": {
      "userName": "UsernameValue1",
      "password": "PasswordValue1"
    },
    "parameterOfTypePSCredential2": {
      "userName": "UsernameValue2",
      "password": "PasswordValue2"
    }
  },
  "configurationUrlSasToken": "?g!bber1sht0k3n",
  "configurationDataUrlSasToken": "?dataAcC355T0k3N"
}

```

## <a name="details"></a><span data-ttu-id="68845-112">Details</span><span class="sxs-lookup"><span data-stu-id="68845-112">Details</span></span>
| <span data-ttu-id="68845-113">Property Name</span><span class="sxs-lookup"><span data-stu-id="68845-113">Property Name</span></span> | <span data-ttu-id="68845-114">Type</span><span class="sxs-lookup"><span data-stu-id="68845-114">Type</span></span> | <span data-ttu-id="68845-115">Description</span><span class="sxs-lookup"><span data-stu-id="68845-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="68845-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="68845-116">settings.wmfVersion</span></span> |<span data-ttu-id="68845-117">string</span><span class="sxs-lookup"><span data-stu-id="68845-117">string</span></span> |<span data-ttu-id="68845-118">Specifies the version of the Windows Management Framework that should be installed on your VM.</span><span class="sxs-lookup"><span data-stu-id="68845-118">Specifies the version of the Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="68845-119">Setting this property to 'latest' installs the most updated version of WMF.</span><span class="sxs-lookup"><span data-stu-id="68845-119">Setting this property to 'latest' installs the most updated version of WMF.</span></span> <span data-ttu-id="68845-120">The only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span><span class="sxs-lookup"><span data-stu-id="68845-120">The only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="68845-121">These possible values are subject to updates.</span><span class="sxs-lookup"><span data-stu-id="68845-121">These possible values are subject to updates.</span></span> <span data-ttu-id="68845-122">The default value is 'latest'.</span><span class="sxs-lookup"><span data-stu-id="68845-122">The default value is 'latest'.</span></span> |
| <span data-ttu-id="68845-123">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="68845-123">settings.configuration.url</span></span> |<span data-ttu-id="68845-124">string</span><span class="sxs-lookup"><span data-stu-id="68845-124">string</span></span> |<span data-ttu-id="68845-125">Specifies the URL location from which to download your DSC configuration zip file.</span><span class="sxs-lookup"><span data-stu-id="68845-125">Specifies the URL location from which to download your DSC configuration zip file.</span></span> <span data-ttu-id="68845-126">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationUrlSasToken property to the value of your SAS token.</span><span class="sxs-lookup"><span data-stu-id="68845-126">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationUrlSasToken property to the value of your SAS token.</span></span> <span data-ttu-id="68845-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span><span class="sxs-lookup"><span data-stu-id="68845-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="68845-128">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="68845-128">settings.configuration.script</span></span> |<span data-ttu-id="68845-129">string</span><span class="sxs-lookup"><span data-stu-id="68845-129">string</span></span> |<span data-ttu-id="68845-130">Specifies the file name of the script that contains the definition of your DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="68845-130">Specifies the file name of the script that contains the definition of your DSC configuration.</span></span> <span data-ttu-id="68845-131">This script must be in the root folder of the zip file downloaded from the URL specified by the configuration.url property.</span><span class="sxs-lookup"><span data-stu-id="68845-131">This script must be in the root folder of the zip file downloaded from the URL specified by the configuration.url property.</span></span> <span data-ttu-id="68845-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span><span class="sxs-lookup"><span data-stu-id="68845-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="68845-133">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="68845-133">settings.configuration.function</span></span> |<span data-ttu-id="68845-134">string</span><span class="sxs-lookup"><span data-stu-id="68845-134">string</span></span> |<span data-ttu-id="68845-135">Specifies the name of your DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="68845-135">Specifies the name of your DSC configuration.</span></span> <span data-ttu-id="68845-136">The configuration named must be contained in the script defined by configuration.script.</span><span class="sxs-lookup"><span data-stu-id="68845-136">The configuration named must be contained in the script defined by configuration.script.</span></span> <span data-ttu-id="68845-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span><span class="sxs-lookup"><span data-stu-id="68845-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="68845-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="68845-138">settings.configurationArguments</span></span> |<span data-ttu-id="68845-139">Collection</span><span class="sxs-lookup"><span data-stu-id="68845-139">Collection</span></span> |<span data-ttu-id="68845-140">Defines any parameters you would like to pass to your DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="68845-140">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="68845-141">This property is not encrypted.</span><span class="sxs-lookup"><span data-stu-id="68845-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="68845-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="68845-142">settings.configurationData.url</span></span> |<span data-ttu-id="68845-143">string</span><span class="sxs-lookup"><span data-stu-id="68845-143">string</span></span> |<span data-ttu-id="68845-144">Specifies the URL from which to download your configuration data (.psd1) file to use as input for your DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="68845-144">Specifies the URL from which to download your configuration data (.psd1) file to use as input for your DSC configuration.</span></span> <span data-ttu-id="68845-145">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationDataUrlSasToken property to the value of your SAS token.</span><span class="sxs-lookup"><span data-stu-id="68845-145">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationDataUrlSasToken property to the value of your SAS token.</span></span> |
| <span data-ttu-id="68845-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="68845-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="68845-147">string</span><span class="sxs-lookup"><span data-stu-id="68845-147">string</span></span> |<span data-ttu-id="68845-148">Enables or disables telemetry collection.</span><span class="sxs-lookup"><span data-stu-id="68845-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="68845-149">The only possible values for this property are **'Enable', 'Disable', '', or $null**.</span><span class="sxs-lookup"><span data-stu-id="68845-149">The only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="68845-150">Leaving this property blank or null enables telemetry.</span><span class="sxs-lookup"><span data-stu-id="68845-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="68845-151">The default value is ''.</span><span class="sxs-lookup"><span data-stu-id="68845-151">The default value is ''.</span></span> [<span data-ttu-id="68845-152">More Information</span><span class="sxs-lookup"><span data-stu-id="68845-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="68845-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="68845-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="68845-154">Collection</span><span class="sxs-lookup"><span data-stu-id="68845-154">Collection</span></span> |<span data-ttu-id="68845-155">Defines alternate locations from which to download the WMF.</span><span class="sxs-lookup"><span data-stu-id="68845-155">Defines alternate locations from which to download the WMF.</span></span> [<span data-ttu-id="68845-156">More Information</span><span class="sxs-lookup"><span data-stu-id="68845-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="68845-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="68845-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="68845-158">Collection</span><span class="sxs-lookup"><span data-stu-id="68845-158">Collection</span></span> |<span data-ttu-id="68845-159">Defines any parameters you would like to pass to your DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="68845-159">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="68845-160">This property is encrypted.</span><span class="sxs-lookup"><span data-stu-id="68845-160">This property is encrypted.</span></span> |
| <span data-ttu-id="68845-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="68845-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="68845-162">string</span><span class="sxs-lookup"><span data-stu-id="68845-162">string</span></span> |<span data-ttu-id="68845-163">Specifies the SAS token to access the URL defined by configuration.url.</span><span class="sxs-lookup"><span data-stu-id="68845-163">Specifies the SAS token to access the URL defined by configuration.url.</span></span> <span data-ttu-id="68845-164">This property is encrypted.</span><span class="sxs-lookup"><span data-stu-id="68845-164">This property is encrypted.</span></span> |
| <span data-ttu-id="68845-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="68845-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="68845-166">string</span><span class="sxs-lookup"><span data-stu-id="68845-166">string</span></span> |<span data-ttu-id="68845-167">Specifies the SAS token to access the URL defined by configurationData.url.</span><span class="sxs-lookup"><span data-stu-id="68845-167">Specifies the SAS token to access the URL defined by configurationData.url.</span></span> <span data-ttu-id="68845-168">This property is encrypted.</span><span class="sxs-lookup"><span data-stu-id="68845-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="68845-169">Settings vs. ProtectedSettings</span><span class="sxs-lookup"><span data-stu-id="68845-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="68845-170">All settings are saved in a settings text file on the VM.</span><span class="sxs-lookup"><span data-stu-id="68845-170">All settings are saved in a settings text file on the VM.</span></span>
<span data-ttu-id="68845-171">Properties under 'settings' are public properties because they are not encrypted in the settings text file.</span><span class="sxs-lookup"><span data-stu-id="68845-171">Properties under 'settings' are public properties because they are not encrypted in the settings text file.</span></span>
<span data-ttu-id="68845-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on the VM.</span><span class="sxs-lookup"><span data-stu-id="68845-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on the VM.</span></span>

<span data-ttu-id="68845-173">If the configuration needs credentials, they can be included in protectedSettings:</span><span class="sxs-lookup"><span data-stu-id="68845-173">If the configuration needs credentials, they can be included in protectedSettings:</span></span>

```json
"protectedSettings": {
    "configurationArguments": {
        "parameterOfTypePSCredential1": {
               "userName": "UsernameValue1",
               "password": "PasswordValue1"
        }
    }
}
```

## <a name="example"></a><span data-ttu-id="68845-174">Example</span><span class="sxs-lookup"><span data-stu-id="68845-174">Example</span></span>
<span data-ttu-id="68845-175">The following example derives from the "Getting Started" section of the [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68845-175">The following example derives from the "Getting Started" section of the [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="68845-176">This example uses Resource Manager templates instead of cmdlets to deploy the extension.</span><span class="sxs-lookup"><span data-stu-id="68845-176">This example uses Resource Manager templates instead of cmdlets to deploy the extension.</span></span> <span data-ttu-id="68845-177">Save the "IisInstall.ps1" configuration, place it in a .ZIP file, and upload the file in an accessible URL.</span><span class="sxs-lookup"><span data-stu-id="68845-177">Save the "IisInstall.ps1" configuration, place it in a .ZIP file, and upload the file in an accessible URL.</span></span> <span data-ttu-id="68845-178">This example uses Azure blob storage, but it is possible to download .ZIP files from any arbitrary location.</span><span class="sxs-lookup"><span data-stu-id="68845-178">This example uses Azure blob storage, but it is possible to download .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="68845-179">In the Azure Resource Manager template, the following code instructs the VM to download the correct file and run the appropriate PowerShell function:</span><span class="sxs-lookup"><span data-stu-id="68845-179">In the Azure Resource Manager template, the following code instructs the VM to download the correct file and run the appropriate PowerShell function:</span></span>

```json
"settings": {
    "configuration": {
        "url": "https://demo.blob.core.windows.net/",
        "script": "IisInstall.ps1",
        "function": "IISInstall"
    }
    } 
},
"protectedSettings": {
    "configurationUrlSasToken": "odLPL/U1p9lvcnp..."
}
```

## <a name="updating-from-the-previous-format"></a><span data-ttu-id="68845-180">Updating from the Previous Format</span><span class="sxs-lookup"><span data-stu-id="68845-180">Updating from the Previous Format</span></span>
<span data-ttu-id="68845-181">Any settings in the previous format (containing the public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt to the current format and run just as they did before.</span><span class="sxs-lookup"><span data-stu-id="68845-181">Any settings in the previous format (containing the public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt to the current format and run just as they did before.</span></span>

<span data-ttu-id="68845-182">The following schema is what the previous settings schema looked like:</span><span class="sxs-lookup"><span data-stu-id="68845-182">The following schema is what the previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points to private Azure Blob Storage",
    "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
    "Properties":  {
        "ParameterToConfigurationFunction1":  "Value1",
        "ParameterToConfigurationFunction2":  "Value2",
        "ParameterOfTypePSCredential1": {
            "UserName": "UsernameValue1",
            "Password": "PrivateSettingsRef:Key1" 
        },
        "ParameterOfTypePSCredential2": {
            "UserName": "UsernameValue2",
            "Password": "PrivateSettingsRef:Key2"
        }
    }
},
"protectedSettings": { 
    "Items": {
        "Key1": "PasswordValue1",
        "Key2": "PasswordValue2"
    },
    "DataBlobUri": "https://UrlToConfigurationDataWithOptionalSasToken.psd1"
}
```

<span data-ttu-id="68845-183">Here's how the previous format adapts to the current format:</span><span class="sxs-lookup"><span data-stu-id="68845-183">Here's how the previous format adapts to the current format:</span></span>

| <span data-ttu-id="68845-184">Property Name</span><span class="sxs-lookup"><span data-stu-id="68845-184">Property Name</span></span> | <span data-ttu-id="68845-185">Previous Schema Equivalent</span><span class="sxs-lookup"><span data-stu-id="68845-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="68845-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="68845-186">settings.wmfVersion</span></span> |<span data-ttu-id="68845-187">settings.WMFVersion</span><span class="sxs-lookup"><span data-stu-id="68845-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="68845-188">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="68845-188">settings.configuration.url</span></span> |<span data-ttu-id="68845-189">settings.ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="68845-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="68845-190">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="68845-190">settings.configuration.script</span></span> |<span data-ttu-id="68845-191">First part of settings.ConfigurationFunction (before '\\\\')</span><span class="sxs-lookup"><span data-stu-id="68845-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="68845-192">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="68845-192">settings.configuration.function</span></span> |<span data-ttu-id="68845-193">Second part of settings.ConfigurationFunction (after '\\\\')</span><span class="sxs-lookup"><span data-stu-id="68845-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="68845-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="68845-194">settings.configurationArguments</span></span> |<span data-ttu-id="68845-195">settings.Properties</span><span class="sxs-lookup"><span data-stu-id="68845-195">settings.Properties</span></span> |
| <span data-ttu-id="68845-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="68845-196">settings.configurationData.url</span></span> |<span data-ttu-id="68845-197">protectedSettings.DataBlobUri (without SAS token)</span><span class="sxs-lookup"><span data-stu-id="68845-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="68845-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="68845-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="68845-199">settings.Privacy.DataEnabled</span><span class="sxs-lookup"><span data-stu-id="68845-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="68845-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="68845-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="68845-201">settings.AdvancedOptions.DownloadMappings</span><span class="sxs-lookup"><span data-stu-id="68845-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="68845-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="68845-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="68845-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="68845-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="68845-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="68845-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="68845-205">settings.SasToken</span><span class="sxs-lookup"><span data-stu-id="68845-205">settings.SasToken</span></span> |
| <span data-ttu-id="68845-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="68845-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="68845-207">SAS token from protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="68845-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="68845-208">Troubleshooting - Error Code 1100</span><span class="sxs-lookup"><span data-stu-id="68845-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="68845-209">Error Code 1100 indicates that there is a problem with the user input to the DSC extension.</span><span class="sxs-lookup"><span data-stu-id="68845-209">Error Code 1100 indicates that there is a problem with the user input to the DSC extension.</span></span>
<span data-ttu-id="68845-210">The text of these errors is variable and may change.</span><span class="sxs-lookup"><span data-stu-id="68845-210">The text of these errors is variable and may change.</span></span>
<span data-ttu-id="68845-211">Here are some of the errors you may run into and how you can fix them.</span><span class="sxs-lookup"><span data-stu-id="68845-211">Here are some of the errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="68845-212">Invalid Values</span><span class="sxs-lookup"><span data-stu-id="68845-212">Invalid Values</span></span>
<span data-ttu-id="68845-213">"Privacy.dataCollection is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="68845-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="68845-214">The only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="68845-214">The only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="68845-215">Only possible values are …</span><span class="sxs-lookup"><span data-stu-id="68845-215">Only possible values are …</span></span> <span data-ttu-id="68845-216">and 'latest'"</span><span class="sxs-lookup"><span data-stu-id="68845-216">and 'latest'"</span></span>

<span data-ttu-id="68845-217">Problem: A provided value is not allowed.</span><span class="sxs-lookup"><span data-stu-id="68845-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="68845-218">Solution: Change the invalid value to a valid value.</span><span class="sxs-lookup"><span data-stu-id="68845-218">Solution: Change the invalid value to a valid value.</span></span> <span data-ttu-id="68845-219">See the table in the Details section.</span><span class="sxs-lookup"><span data-stu-id="68845-219">See the table in the Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="68845-220">Invalid URL</span><span class="sxs-lookup"><span data-stu-id="68845-220">Invalid URL</span></span>
<span data-ttu-id="68845-221">"ConfigurationData.url is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="68845-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="68845-222">This is not a valid URL" "DataBlobUri is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="68845-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="68845-223">This is not a valid URL" "Configuration.url is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="68845-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="68845-224">This is not a valid URL"</span><span class="sxs-lookup"><span data-stu-id="68845-224">This is not a valid URL"</span></span>

<span data-ttu-id="68845-225">Problem: A provided URL is not valid.</span><span class="sxs-lookup"><span data-stu-id="68845-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="68845-226">Solution: Check all your provided URLs.</span><span class="sxs-lookup"><span data-stu-id="68845-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="68845-227">Make sure all URLs resolve to valid locations that the extension can access on the remote machine.</span><span class="sxs-lookup"><span data-stu-id="68845-227">Make sure all URLs resolve to valid locations that the extension can access on the remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="68845-228">Invalid ConfigurationArgument Type</span><span class="sxs-lookup"><span data-stu-id="68845-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="68845-229">"Invalid configurationArguments type {0}"</span><span class="sxs-lookup"><span data-stu-id="68845-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="68845-230">Problem: The ConfigurationArguments property cannot resolve to a Hashtable object.</span><span class="sxs-lookup"><span data-stu-id="68845-230">Problem: The ConfigurationArguments property cannot resolve to a Hashtable object.</span></span> 

<span data-ttu-id="68845-231">Solution: Make your ConfigurationArguments property a Hashtable.</span><span class="sxs-lookup"><span data-stu-id="68845-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="68845-232">Follow the format provided in the preceeding example.</span><span class="sxs-lookup"><span data-stu-id="68845-232">Follow the format provided in the preceeding example.</span></span> <span data-ttu-id="68845-233">Watch out for quotes, commas, and braces.</span><span class="sxs-lookup"><span data-stu-id="68845-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="68845-234">Duplicate ConfigurationArguments</span><span class="sxs-lookup"><span data-stu-id="68845-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="68845-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span><span class="sxs-lookup"><span data-stu-id="68845-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="68845-236">Problem: The ConfigurationArguments in public settings and the ConfigurationArguments in protected settings contain properties with the same name.</span><span class="sxs-lookup"><span data-stu-id="68845-236">Problem: The ConfigurationArguments in public settings and the ConfigurationArguments in protected settings contain properties with the same name.</span></span>

<span data-ttu-id="68845-237">Solution: Remove one of the duplicate properties.</span><span class="sxs-lookup"><span data-stu-id="68845-237">Solution: Remove one of the duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="68845-238">Missing Properties</span><span class="sxs-lookup"><span data-stu-id="68845-238">Missing Properties</span></span>
<span data-ttu-id="68845-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span><span class="sxs-lookup"><span data-stu-id="68845-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="68845-240">"Configuration.url requires that configuration.script is specified"</span><span class="sxs-lookup"><span data-stu-id="68845-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="68845-241">"Configuration.script requires that configuration.url is specified"</span><span class="sxs-lookup"><span data-stu-id="68845-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="68845-242">"Configuration.url requires that configuration.function is specified"</span><span class="sxs-lookup"><span data-stu-id="68845-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="68845-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span><span class="sxs-lookup"><span data-stu-id="68845-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="68845-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span><span class="sxs-lookup"><span data-stu-id="68845-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="68845-245">Problem: A defined property needs another property that is missing.</span><span class="sxs-lookup"><span data-stu-id="68845-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="68845-246">Solutions:</span><span class="sxs-lookup"><span data-stu-id="68845-246">Solutions:</span></span> 

* <span data-ttu-id="68845-247">Provide the missing property.</span><span class="sxs-lookup"><span data-stu-id="68845-247">Provide the missing property.</span></span>
* <span data-ttu-id="68845-248">Remove the property that needs the missing property.</span><span class="sxs-lookup"><span data-stu-id="68845-248">Remove the property that needs the missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68845-249">Next Steps</span><span class="sxs-lookup"><span data-stu-id="68845-249">Next Steps</span></span>
<span data-ttu-id="68845-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with the Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="68845-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with the Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="68845-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68845-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="68845-252">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68845-252">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="68845-253">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="68845-253">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

