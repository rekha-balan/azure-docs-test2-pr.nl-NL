---
title: Azure MFA Server upgrade | Microsoft Docs
description: Steps and guidance to upgrade the Azure Multi-Factor Authentication Server to a newer version.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2017
ms.author: kgremban
ms.openlocfilehash: 6932d0da5f650121c4d0bdd0044fa696c96bcc5e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551112"
---
# <a name="upgrade-to-the-latest-azure-multi-factor-authentication-server"></a>Upgrade to the latest Azure Multi-Factor Authentication Server

This article walks you through the process of upgrading Azure Multi-Factor Authentication (MFA) Server v6.0 or higher. If you need to upgrade an old version of the PhoneFactor Agent, refer to [Upgrade the PhoneFactor Agent to Azure Multi-Factor Authentication Server](multi-factor-authentication-get-started-server-upgrade.md).

If you're upgrading from v6.x or older to v7.x or newer, all components change from .NET 2.0 to .NET 4.5. All components also require Microsoft Visual C++ 2015 Redistributable Update 1 or higher. The MFA Server installer will install both the x86 and x64 versions of these components if they aren't already installed. If the User Portal and Mobile App Web Service run on separate servers, you need to install those packages before upgrading those components. You can search for the latest Microsoft Visual C++ 2015 Redistributable update on the [Microsoft Download Center](https://www.microsoft.com/en-us/download/). 

## <a name="install-the-latest-version-of-azure-mfa-server"></a>Install the latest version of Azure MFA Server

1. Use the instructions in [Download the Azure Multi-Factor Authentication Server](multi-factor-authentication-get-started-server.md#download-the-azure-multi-factor-authentication-server) to get the latest version of the Azure MFA Server.
2. Make a backup of the MFA Server data file located at C:\Program Files\Multi-Factor Authentication Server\Data\PhoneFactor.pfdata (assuming the default install location) on your master MFA Server.
3. If you run multiple servers for high availability, change the client systems that authenticate to the MFA Server so that they stop sending traffic to MFA Servers that are upgrading. If you use a load balancer, remove each MFA Server being upgraded from the load balancer, do the upgrade, and then add the server back into the farm.
4. Run the new installer on each MFA Server. Upgrade subordinate servers first because they can read the old data file being replicated by the master. 

  You do not need to uninstall your current MFA Server before running the installer. The installer performs an in-place upgrade. The installation path is picked up from the registry from the previous installation, so it installs in the same location (for example, C:\Program Files\Multi-Factor Authentication Server). 
  
5. If you're prompted to install a Microsoft Visual C++ 2015 Redistributable update package, accept the prompt. Both the x86 and x64 versions of the package are installed.
5. If the Web Service SDK was previously installed, you should be prompted to install the new Web Service SDK. When you install the new Web Service SDK, make sure that the virtual directory name matches the previously installed virtual directory (for example, MultiFactorAuthWebServiceSdk).
6. Repeat the steps on all subordinate servers. Promote one of the subordinates to be the new master, then upgrade the old master server. 

## <a name="upgrade-the-user-portal"></a>Upgrade the User Portal

1. Make a backup of the web.config file that is in the virtual directory of the User Portal installation location (for example, C:\inetpub\wwwroot\MultiFactorAuth). If any changes were made to the default theme, make a backup of the App_Themes\Default folder as well. It is better to create a copy of the Default folder and create a new theme than to change the Default theme.
2. If the User Portal runs on the same server as the other MFA Server components, the MFA Server installation prompts you to update the User Portal. Accept the prompt and install the User Portal update, ensuring that the virtual directory name matches the previously installed virtual directory (for example, MultiFactorAuth).
3. If the User Portal is installed on its own server, copy the MultiFactorAuthenticationUserPortalSetup64.msi file from install location of one of the MFA Servers and put it onto the User Portal web server. Run the installer. 

  If an error occurs stating that Microsoft Visual C++ 2015 Redistributable Update 1 or higher is required, download and install the latest update package from the [Microsoft Download Center](https://www.microsoft.com/download/). Install both the x86 and x64 versions.

4. After the updated User Portal software is installed, compare the web.config backup you made in step 1 with the new web.config file. If no new attributes exist in the new web.config, copy your backup web.config into the virtual directory to overwrite the new one. Another option is to copy/paste the appSettings values and the Web Service SDK URL from the backup file into the new web.config.

If you have the User Portal on multiple servers, repeat the installation on all of them. 


## <a name="upgrade-the-mobile-app-web-service"></a>Upgrade the Mobile App Web Service

1. Make a backup of the web.config file that is in the virtual directory of the Mobile App Web Service installation location (for example, C:\inetpub\wwwroot\app or C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService).
2. Copy the MultiFactorAuthenticationMobileAppWebServiceSetup64.msi file from the install location of one of the MFA Servers and put it onto the Mobile App registration web server.
3. Run the installer. 

  If an error occurs stating that Microsoft Visual C++ 2015 Redistributable Update 1 or higher is required, download and install the latest update package from the [Microsoft Download Center](https://www.microsoft.com/download/). Install both the x86 and x64 versions.

4. After the updated Mobile App Web Service software is installed, compare the web.config file that was backed up in step 1 with the new web.config file installed by the installer. If no new attributes exist in the new web.config, you can copy your saved web.config back into the virtual directory and overwrite the new one that was installed. Another option is to copy/paste the appSettings values and the Web Service SDK URL from the backup file into the new web.config.

If you have the Mobile App Web Service on multiple servers, repeat the installation on all of them. 

## <a name="upgrade-the-ad-fs-adapters"></a>Upgrade the AD FS Adapters


### <a name="if-mfa-runs-on-different-servers-than-ad-fs"></a>If MFA runs on different servers than AD FS

These instructions only apply if you run Multi-Factor Authentication Server separately from your AD FS servers. If both services run on the same servers, skip this section and go to the installation steps. 

1. Save a copy of the existing MultiFactorAuthenticationAdfsAdapter.config that was registered in AD FS, or export the existing configuration to a file using the following PowerShell command: `Export-AdfsAuthenticationProviderConfigurationData -Name [adapter name] -FilePath [path to config file]`. The adapter name is either "WindowsAzureMultiFactorAuthentication" or "AzureMfaServerAuthentication" depending on the version previously installed.
2. Copy the following files from the MFA Server installation location to the AD FS servers:

  - MultiFactorAuthenticationAdfsAdapterSetup64.msi
  - Register-MultiFactorAuthenticationAdfsAdapter.ps1
  - Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
  - MultiFactorAuthenticationAdfsAdapter.config

3. Edit the Register-MultiFactorAuthenticationAdfsAdapter.ps1 script by adding `-ConfigurationFilePath [path]` to the end of the Register-AdfsAuthenticationProvider command, where *[path]* is the full path to the MultiFactorAuthenticationAdfsAdapter.config file or the configuration file exported in the previous step. 

  Check the attributes in the new MultiFactorAuthenticationAdfsAdapter.config to see if they match the old config file. If any attributes were added or removed in the new version, either copy the attribute values from the old configuration file to the new one, or modify the old configuration file to match.

### <a name="install-new-ad-fs-adapters"></a>Install new AD FS adapters

> [!IMPORTANT] 
> Your users will not be required to perform two-step verification during steps 3-8 of this section. If you have AD FS configured in multiple clusters, you can remove, upgrade, and restore each cluster in the farm independently of the other clusters to avoid downtime.

1. Remove some AD FS servers from the farm. Update these servers while the others are still running.
2. Install the new AD FS adapter on each server removed from the AD FS farm. If the MFA Server is installed on each AD FS server, you can update through the MFA Server admin UX. Otherwise, update by running MultiFactorAuthenticationAdfsAdapterSetup64.msi. 

  If an error occurs stating that Microsoft Visual C++ 2015 Redistributable Update 1 or higher is required, download and install the latest update package from the [Microsoft Download Center](https://www.microsoft.com/download/). Install both the x86 and x64 versions.

3. Go to **AD FS** > **Authentication Policies** > **Edit Global MultiFactor Authentication Policy**. Uncheck **WindowsAzureMultiFactorAuthentication** or **AzureMFAServerAuthentication** (depending on the current version installed). 

  Once this step is complete, two-step verification through MFA Server will not be available in this AD FS cluster until you complete step 8.

4. Unregister the older version of the AD FS adapter by running the Unregister-MultiFactorAuthenticationAdfsAdapter.ps1 PowerShell script. Ensure that the *-Name* parameter listed in the script (either “WindowsAzureMultiFactorAuthentication” or "AzureMFAServerAuthentication") matches the name that was displayed in step 3. This applies to all servers in the same AD FS cluster since there is a central configuration.
5. Register the new AD FS adapter by running the Register-MultiFactorAuthenticationAdfsAdapter.ps1 PowerShell script. This applies to all servers in the same AD FS cluster since there is a central configuration.
6. Restart the AD FS service on each server removed from the AD FS farm.
7. Add the updated servers back to the AD FS farm and remove the other servers from the farm.
8. Go to **AD FS** > **Authentication Policies** > **Edit Global MultiFactor Authentication Policy**. Check **AzureMfaServerAuthentication**.
9. Repeat step 2 to update the servers now removed from the AD FS farm and restart the AD FS service on those servers.
10. Add those servers back into the AD FS farm.

## <a name="next-steps"></a>Next steps

- Get examples of [Advanced scenarios with Azure Multi-Factor Authentication and third-party VPNs](multi-factor-authentication-advanced-vpn-configurations.md)

- [Synchronize MFA Server with Windows Server Active Directory](multi-factor-authentication-get-started-server-dirint.md)

- [Configure Windows Authentication](multi-factor-authentication-get-started-server-windows.md) for your applications