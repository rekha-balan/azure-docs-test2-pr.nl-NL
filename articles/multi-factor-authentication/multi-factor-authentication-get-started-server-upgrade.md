---
title: Upgrade PhoneFactor to Azure MFA Server | Microsoft Docs
description: Get started with Azure MFA Server when you upgrade from the older phonefactor agent.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: 42838ff7-bdf2-4d06-bacc-b3839a00cd76
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/06/2017
ms.author: kgremban
ms.openlocfilehash: 5bbd7088f5d4986a5b1c9f5695a5defb678307a9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661326"
---
# <a name="upgrade-the-phonefactor-agent-to-azure-multi-factor-authentication-server"></a>Upgrade the PhoneFactor Agent to Azure Multi-Factor Authentication Server
To upgrading the PhoneFactor Agent v5.x or older to Azure Multi-Factor Authentication Server, uninstall the PhoneFactor Agent and affiliated components first. Then the Multi-Factor Authentication Server and its affiliated components can be installed.

## <a name="uninstall-the-phonefactor-agent"></a>Uninstall the PhoneFactor Agent

1. First, back up the PhoneFactor data file. The default installation location is C:\Program Files\PhoneFactor\Data\Phonefactor.pfdata.

2. If the User Portal is installed:
  1. Navigate to the install folder and back up the web.config file. The default installation location is C:\inetpub\wwwroot\PhoneFactor.

  2. If you have added custom themes to the portal, back up your custom folder below the C:\inetpub\wwwroot\PhoneFactor\App_Themes directory.

  3. Uninstall the User Portal either through the PhoneFactor Agent (only available if installed on the same server as the PhoneFactor Agent) or through Windows Programs and Features.

3. If the Mobile App Web Service is installed:

  1. Go to the install folder and back up the web.config file. The default installation location is C:\inetpub\wwwroot\PhoneFactorPhoneAppWebService.

  2. Uninstall the Mobile App Web Service through Windows Programs and Features.

4. If the Web Service SDK is installed, uninstall it either through the PhoneFactor Agent or through Windows Programs and Features.

5. Uninstall the PhoneFactor Agent through Windows Programs and Features.

## <a name="install-the-multi-factor-authentication-server"></a>Install the Multi-Factor Authentication Server

The installation path is picked up from the registry from the previous PhoneFactor Agent installation, so it should install in the same location (e.g. C:\Program Files\PhoneFactor). New installations will have a different default install path (e.g. C:\Program Files\Multi-Factor Authentication Server). The data file left by the previous PhoneFactor Agent should be upgraded during installation, so your users and settings should still be there after installing the new Multi-Factor Authentication Server.

1. If prompted, activate the Multi-Factor Authentication Server and ensure it is assigned to the correct replication group.

2. If the Web Service SDK was previously installed, install the new Web Service SDK through the Multi-Factor Authentication Server User Interface.

  The default virtual directory name is now “MultiFactorAuthWebServiceSdk” instead of “PhoneFactorWebServiceSdk”. If you want to use the previous name, you must change the name of the virtual directory during installation. Otherwise, if you allow the install to use the new default name, you will have to change the URL in any applications that reference the Web Service SDK such as the User Portal and Mobile App Web Service to point at the correct location.

3. If the User Portal was previously installed on the PhoneFactor Agent Server, install the new Multi-Factor Authentication User Portal through the Multi-Factor Authentication Server User Interface.

  The default virtual directory name is now “MultiFactorAuth” instead of “PhoneFactor”. If you want to use the previous name, you must change the name of the virtual directory during installation. Otherwise, if you allow the install to use the new default name, you should click the User Portal icon in the Multi-Factor Authentication Server and update the User Portal URL on the Settings tab.

4. If the User Portal and/or Mobile App Web Service was previously installed on a different server from the PhoneFactor Agent:

  1. Go to the install location (e.g. C:\Program Files\PhoneFactor) and copy the appropriate installer(s) to the other server. There are 32-bit and 64-bit installers for both the User Portal and Mobile App Web Service. They are called MultiFactorAuthenticationUserPortalSetupXX.msi and MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi respectively.

  2. To install the User Portal on the web server, open a command prompt as an administrator and run MultiFactorAuthenticationUserPortalSetupXX.msi.

    The default virtual directory name is now “MultiFactorAuth” instead of “PhoneFactor”. If you want to use the previous name, you must change the name of the virtual directory during installation. Otherwise, if you allow the install to use the new default name, you should click the User Portal icon in the Multi-Factor Authentication Server and update the User Portal URL on the Settings tab. Existing users will need to be informed of the new URL.

  3. Go to the User Portal install location (e.g. C:\inetpub\wwwroot\MultiFactorAuth) and edit the web.config file. Copy the values in the appSettings and applicationSettings sections from your original web.config file that was backed up prior to the upgrade into the new web.config file. If the new default virtual directory name was kept when installing the Web Service SDK, change the URL in the applicationSettings section to point to the correct location. If any other defaults were changed in the previous web.config file, apply those same changes to the new web.config file.

  4. To install the Mobile App Web Service on the web server, open a command prompt as an administrator and run the MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi.

    The default virtual directory name is now “MultiFactorAuthMobileAppWebService” instead of “PhoneFactorPhoneAppWebService”. If you want to use the previous name, you must change the name of the virtual directory during installation. You may want to choose a shorter name to make it easy for end users to type in on their mobile devices. Otherwise, if you allow the install to use the new default name, you should click the Mobile App icon in the Multi-Factor Authentication Server and update the Mobile App Web Service URL.

  5. Go to the Mobile App Web Service install location (e.g. C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService) and edit the web.config file. Copy the values in the appSettings and applicationSettings sections from your original web.config file that was backed up prior to the upgrade into the new web.config file. If the new default virtual directory name was kept when installing the Web Service SDK, change the URL in the applicationSettings section to point to the correct location. If any other defaults were changed in the previous web.config file, apply those same changes to the new web.config file.

## <a name="next-steps"></a>Next steps

- [Install the users portal](multi-factor-authentication-get-started-portal.md) for the Azure Multi-Factor Authentication Server.

- [Configure Windows Authentication](multi-factor-authentication-get-started-server-windows.md) for your applications. 