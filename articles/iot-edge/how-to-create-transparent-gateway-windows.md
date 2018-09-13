---
title: Create a transparent gateway with Azure IoT Edge - Windows | Microsoft Docs
description: Use Azure IoT Edge to create a transparent gateway that can process information for multiple devices
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 6/20/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: 5ffb1b5c9889e2325eab32306b61899b37d22488
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857508"
---
# <a name="create-a-windows-iot-edge-device-that-acts-as-a-transparent-gateway"></a><span data-ttu-id="40349-103">Create a Windows IoT Edge device that acts as a transparent gateway</span><span class="sxs-lookup"><span data-stu-id="40349-103">Create a Windows IoT Edge device that acts as a transparent gateway</span></span>

<span data-ttu-id="40349-104">This article provides detailed instructions for using an IoT Edge device as a transparent gateway.</span><span class="sxs-lookup"><span data-stu-id="40349-104">This article provides detailed instructions for using an IoT Edge device as a transparent gateway.</span></span> <span data-ttu-id="40349-105">For the rest of this article, the term *IoT Edge gateway* refers to an IoT Edge device used as a transparent gateway.</span><span class="sxs-lookup"><span data-stu-id="40349-105">For the rest of this article, the term *IoT Edge gateway* refers to an IoT Edge device used as a transparent gateway.</span></span> <span data-ttu-id="40349-106">For more detailed information, see [How an IoT Edge device can be used as a gateway][lnk-edge-as-gateway], which gives a conceptual overview.</span><span class="sxs-lookup"><span data-stu-id="40349-106">For more detailed information, see [How an IoT Edge device can be used as a gateway][lnk-edge-as-gateway], which gives a conceptual overview.</span></span>

>[!NOTE]
><span data-ttu-id="40349-107">Currently:</span><span class="sxs-lookup"><span data-stu-id="40349-107">Currently:</span></span>
> * <span data-ttu-id="40349-108">If the gateway is disconnected from IoT Hub, downstream devices cannot authenticate with the gateway.</span><span class="sxs-lookup"><span data-stu-id="40349-108">If the gateway is disconnected from IoT Hub, downstream devices cannot authenticate with the gateway.</span></span>
> * <span data-ttu-id="40349-109">Edge-enabled devices can't connect to IoT Edge gateways.</span><span class="sxs-lookup"><span data-stu-id="40349-109">Edge-enabled devices can't connect to IoT Edge gateways.</span></span> 
> * <span data-ttu-id="40349-110">Downstream devices can't use file upload.</span><span class="sxs-lookup"><span data-stu-id="40349-110">Downstream devices can't use file upload.</span></span>

<span data-ttu-id="40349-111">The hard part about creating a transparent gateway is securely connecting the gateway to downstream devices.</span><span class="sxs-lookup"><span data-stu-id="40349-111">The hard part about creating a transparent gateway is securely connecting the gateway to downstream devices.</span></span> <span data-ttu-id="40349-112">Azure IoT Edge allows you to use PKI infrastructure to set up secure TLS connections between these devices.</span><span class="sxs-lookup"><span data-stu-id="40349-112">Azure IoT Edge allows you to use PKI infrastructure to set up secure TLS connections between these devices.</span></span> <span data-ttu-id="40349-113">In this case, we’re allowing a downstream device to connect to an IoT Edge device acting as a transparent gateway.</span><span class="sxs-lookup"><span data-stu-id="40349-113">In this case, we’re allowing a downstream device to connect to an IoT Edge device acting as a transparent gateway.</span></span>  <span data-ttu-id="40349-114">To maintain reasonable security, the downstream device should confirm the identity of the Edge device because you only want your devices connecting to your gateways and not a potentially malicious gateway.</span><span class="sxs-lookup"><span data-stu-id="40349-114">To maintain reasonable security, the downstream device should confirm the identity of the Edge device because you only want your devices connecting to your gateways and not a potentially malicious gateway.</span></span>

<span data-ttu-id="40349-115">You can create any certificate infrastructure that enables the trust required for your device-gateway topology.</span><span class="sxs-lookup"><span data-stu-id="40349-115">You can create any certificate infrastructure that enables the trust required for your device-gateway topology.</span></span> <span data-ttu-id="40349-116">In this article, we assume the same certificate setup that you would use to enable [X.509 CA security][lnk-iothub-x509] in IoT Hub, which involves an X.509 CA certificate associated to a specific IoT hub (the IoT hub owner CA), and a series of certificates, signed with this CA, and a CA for the Edge device.</span><span class="sxs-lookup"><span data-stu-id="40349-116">In this article, we assume the same certificate setup that you would use to enable [X.509 CA security][lnk-iothub-x509] in IoT Hub, which involves an X.509 CA certificate associated to a specific IoT hub (the IoT hub owner CA), and a series of certificates, signed with this CA, and a CA for the Edge device.</span></span>

![Gateway setup][1]

<span data-ttu-id="40349-118">The gateway presents its Edge device CA certificate to the downstream device during the initiation of the connection.</span><span class="sxs-lookup"><span data-stu-id="40349-118">The gateway presents its Edge device CA certificate to the downstream device during the initiation of the connection.</span></span> <span data-ttu-id="40349-119">The downstream device checks to make sure the Edge device CA certificate is signed by the owner CA certificate.</span><span class="sxs-lookup"><span data-stu-id="40349-119">The downstream device checks to make sure the Edge device CA certificate is signed by the owner CA certificate.</span></span> <span data-ttu-id="40349-120">This process allows the downstream device to confirm the gateway comes from a trusted source.</span><span class="sxs-lookup"><span data-stu-id="40349-120">This process allows the downstream device to confirm the gateway comes from a trusted source.</span></span>

<span data-ttu-id="40349-121">The following steps walk you through the process of creating the certificates and installing them in the right places.</span><span class="sxs-lookup"><span data-stu-id="40349-121">The following steps walk you through the process of creating the certificates and installing them in the right places.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40349-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="40349-122">Prerequisites</span></span>
1.  <span data-ttu-id="40349-123">[Install the Azure IoT Edge runtime][lnk-install-windows-x64] on a Windows device you want to use as the transparent gateway.</span><span class="sxs-lookup"><span data-stu-id="40349-123">[Install the Azure IoT Edge runtime][lnk-install-windows-x64] on a Windows device you want to use as the transparent gateway.</span></span>

1. <span data-ttu-id="40349-124">Get OpenSSL for Windows.</span><span class="sxs-lookup"><span data-stu-id="40349-124">Get OpenSSL for Windows.</span></span> <span data-ttu-id="40349-125">There are many ways you can install OpenSSL:</span><span class="sxs-lookup"><span data-stu-id="40349-125">There are many ways you can install OpenSSL:</span></span>

   >[!NOTE]
   ><span data-ttu-id="40349-126">If you already have OpenSSL installed on your Windows device, you may skip this step but please ensure that  `openssl.exe` is available in your `%PATH%` environment variable.</span><span class="sxs-lookup"><span data-stu-id="40349-126">If you already have OpenSSL installed on your Windows device, you may skip this step but please ensure that  `openssl.exe` is available in your `%PATH%` environment variable.</span></span>

   * <span data-ttu-id="40349-127">Download and install any [third-party OpenSSL binaries](https://wiki.openssl.org/index.php/Binaries), for example, from [this project on SourceForge](https://sourceforge.net/projects/openssl/).</span><span class="sxs-lookup"><span data-stu-id="40349-127">Download and install any [third-party OpenSSL binaries](https://wiki.openssl.org/index.php/Binaries), for example, from [this project on SourceForge](https://sourceforge.net/projects/openssl/).</span></span>
   
   * <span data-ttu-id="40349-128">Download the OpenSSL source code and build the binaries on your machine by yourself or do this via [vcpkg](https://github.com/Microsoft/vcpkg).</span><span class="sxs-lookup"><span data-stu-id="40349-128">Download the OpenSSL source code and build the binaries on your machine by yourself or do this via [vcpkg](https://github.com/Microsoft/vcpkg).</span></span> <span data-ttu-id="40349-129">The instructions listed below use vcpkg to download source code, compile and install OpenSSL on your Windows machine all in very easy to use steps.</span><span class="sxs-lookup"><span data-stu-id="40349-129">The instructions listed below use vcpkg to download source code, compile and install OpenSSL on your Windows machine all in very easy to use steps.</span></span>

      1. <span data-ttu-id="40349-130">Navigate to a directory where you want to install vcpkg.</span><span class="sxs-lookup"><span data-stu-id="40349-130">Navigate to a directory where you want to install vcpkg.</span></span> <span data-ttu-id="40349-131">From here on we'll refer to this as $VCPKGDIR.</span><span class="sxs-lookup"><span data-stu-id="40349-131">From here on we'll refer to this as $VCPKGDIR.</span></span> <span data-ttu-id="40349-132">Follow the instructions to download and install [vcpkg](https://github.com/Microsoft/vcpkg).</span><span class="sxs-lookup"><span data-stu-id="40349-132">Follow the instructions to download and install [vcpkg](https://github.com/Microsoft/vcpkg).</span></span>
   
      1. <span data-ttu-id="40349-133">Once vcpkg is installed, from a powershell prompt, run the following command to install the OpenSSL package for Windows x64.</span><span class="sxs-lookup"><span data-stu-id="40349-133">Once vcpkg is installed, from a powershell prompt, run the following command to install the OpenSSL package for Windows x64.</span></span> <span data-ttu-id="40349-134">This typically takes about 5 mins to complete.</span><span class="sxs-lookup"><span data-stu-id="40349-134">This typically takes about 5 mins to complete.</span></span>

         ```PowerShell
         .\vcpkg install openssl:x64-windows
         ```
      1. <span data-ttu-id="40349-135">Add `$VCPKGDIR\installed\x64-windows\tools\openssl` to your `PATH` environment variable so that the `openssl.exe` file is available for invocation.</span><span class="sxs-lookup"><span data-stu-id="40349-135">Add `$VCPKGDIR\installed\x64-windows\tools\openssl` to your `PATH` environment variable so that the `openssl.exe` file is available for invocation.</span></span>

1. <span data-ttu-id="40349-136">Navigate to the directory in which you want to work.</span><span class="sxs-lookup"><span data-stu-id="40349-136">Navigate to the directory in which you want to work.</span></span> <span data-ttu-id="40349-137">From here on we'll refer to this as $WRKDIR.</span><span class="sxs-lookup"><span data-stu-id="40349-137">From here on we'll refer to this as $WRKDIR.</span></span>  <span data-ttu-id="40349-138">All files will be created in this directory.</span><span class="sxs-lookup"><span data-stu-id="40349-138">All files will be created in this directory.</span></span>
   
   <span data-ttu-id="40349-139">cd $WRKDIR</span><span class="sxs-lookup"><span data-stu-id="40349-139">cd $WRKDIR</span></span>

1.  <span data-ttu-id="40349-140">Obtain the scripts to generate the required non-production certificates with the following command.</span><span class="sxs-lookup"><span data-stu-id="40349-140">Obtain the scripts to generate the required non-production certificates with the following command.</span></span> <span data-ttu-id="40349-141">These scripts help you create the necessary certificates to set up a transparent gateway.</span><span class="sxs-lookup"><span data-stu-id="40349-141">These scripts help you create the necessary certificates to set up a transparent gateway.</span></span>

      ```PowerShell
      git clone https://github.com/Azure/azure-iot-sdk-c.git
      ```

1. <span data-ttu-id="40349-142">Copy configuration and script files into your working directory.</span><span class="sxs-lookup"><span data-stu-id="40349-142">Copy configuration and script files into your working directory.</span></span> <span data-ttu-id="40349-143">Additionally, set env variable OPENSSL_CONF to use the openssl_root_ca.cnf configuration file.</span><span class="sxs-lookup"><span data-stu-id="40349-143">Additionally, set env variable OPENSSL_CONF to use the openssl_root_ca.cnf configuration file.</span></span>

   ```PowerShell
   copy azure-iot-sdk-c\tools\CACertificates\*.cnf .
   copy azure-iot-sdk-c\tools\CACertificates\ca-certs.ps1 .
   $env:OPENSSL_CONF = "$PWD\openssl_root_ca.cnf"
   ```

1. <span data-ttu-id="40349-144">Enable PowerShell to run the scripts by running the following command</span><span class="sxs-lookup"><span data-stu-id="40349-144">Enable PowerShell to run the scripts by running the following command</span></span>

   ```PowerShell
   Set-ExecutionPolicy -ExecutionPolicy Unrestricted
   ```

1. <span data-ttu-id="40349-145">Bring the functions, used by the scripts, into PowerShell's global namespace by dot-sourcing with the following command</span><span class="sxs-lookup"><span data-stu-id="40349-145">Bring the functions, used by the scripts, into PowerShell's global namespace by dot-sourcing with the following command</span></span>
   
   ```PowerShell
   . .\ca-certs.ps1
   ```

1. <span data-ttu-id="40349-146">Verify OpenSSL has been installed correctly and make sure there won't be name collisions with existing certificates by running the following command.</span><span class="sxs-lookup"><span data-stu-id="40349-146">Verify OpenSSL has been installed correctly and make sure there won't be name collisions with existing certificates by running the following command.</span></span> <span data-ttu-id="40349-147">If there are problems, the script should describe how to fix these on your system.</span><span class="sxs-lookup"><span data-stu-id="40349-147">If there are problems, the script should describe how to fix these on your system.</span></span>

   ```PowerShell
   Test-CACertsPrerequisites
   ```

## <a name="certificate-creation"></a><span data-ttu-id="40349-148">Certificate creation</span><span class="sxs-lookup"><span data-stu-id="40349-148">Certificate creation</span></span>
1.  <span data-ttu-id="40349-149">Create the owner CA certificate and one intermediate certificate.</span><span class="sxs-lookup"><span data-stu-id="40349-149">Create the owner CA certificate and one intermediate certificate.</span></span> <span data-ttu-id="40349-150">These are all placed in `$WRKDIR`.</span><span class="sxs-lookup"><span data-stu-id="40349-150">These are all placed in `$WRKDIR`.</span></span>

      ```PowerShell
      New-CACertsCertChain rsa
      ```

1.  <span data-ttu-id="40349-151">Create the Edge device CA certificate and private key with the command below.</span><span class="sxs-lookup"><span data-stu-id="40349-151">Create the Edge device CA certificate and private key with the command below.</span></span>

   >[!NOTE]
   > <span data-ttu-id="40349-152">**DO NOT** use a name that is the same as the gateway's DNS host name.</span><span class="sxs-lookup"><span data-stu-id="40349-152">**DO NOT** use a name that is the same as the gateway's DNS host name.</span></span> <span data-ttu-id="40349-153">Doing so will cause client certification against these certificates to fail.</span><span class="sxs-lookup"><span data-stu-id="40349-153">Doing so will cause client certification against these certificates to fail.</span></span>

   ```PowerShell
   New-CACertsEdgeDevice "<gateway device name>"
   ```

## <a name="certificate-chain-creation"></a><span data-ttu-id="40349-154">Certificate chain creation</span><span class="sxs-lookup"><span data-stu-id="40349-154">Certificate chain creation</span></span>
<span data-ttu-id="40349-155">Create a certificate chain from the owner CA certificate, intermediate certificate, and Edge device CA certificate with the command below.</span><span class="sxs-lookup"><span data-stu-id="40349-155">Create a certificate chain from the owner CA certificate, intermediate certificate, and Edge device CA certificate with the command below.</span></span> <span data-ttu-id="40349-156">Placing it in a chain file allows you to easily install it on your Edge device acting as a transparent gateway.</span><span class="sxs-lookup"><span data-stu-id="40349-156">Placing it in a chain file allows you to easily install it on your Edge device acting as a transparent gateway.</span></span>

   ```PowerShell
   Write-CACertsCertificatesForEdgeDevice "<gateway device name>"
   ```

   <span data-ttu-id="40349-157">The output of the script execution are the following certificates and key:</span><span class="sxs-lookup"><span data-stu-id="40349-157">The output of the script execution are the following certificates and key:</span></span>
   * `$WRKDIR\certs\new-edge-device.*`
   * `$WRKDIR\private\new-edge-device.key.pem`
   * `$WRKDIR\certs\azure-iot-test-only.root.ca.cert.pem`

## <a name="installation-on-the-gateway"></a><span data-ttu-id="40349-158">Installation on the gateway</span><span class="sxs-lookup"><span data-stu-id="40349-158">Installation on the gateway</span></span>
1.  <span data-ttu-id="40349-159">Copy the following files from $WRKDIR anywhere on your Edge device, we'll refer to that as $CERTDIR.</span><span class="sxs-lookup"><span data-stu-id="40349-159">Copy the following files from $WRKDIR anywhere on your Edge device, we'll refer to that as $CERTDIR.</span></span> <span data-ttu-id="40349-160">If you generated the certificates on your Edge device skip this step.</span><span class="sxs-lookup"><span data-stu-id="40349-160">If you generated the certificates on your Edge device skip this step.</span></span>

   * <span data-ttu-id="40349-161">Device CA certificate -  `$WRKDIR\certs\new-edge-device-full-chain.cert.pem`</span><span class="sxs-lookup"><span data-stu-id="40349-161">Device CA certificate -  `$WRKDIR\certs\new-edge-device-full-chain.cert.pem`</span></span>
   * <span data-ttu-id="40349-162">Device CA private key - `$WRKDIR\private\new-edge-device.key.pem`</span><span class="sxs-lookup"><span data-stu-id="40349-162">Device CA private key - `$WRKDIR\private\new-edge-device.key.pem`</span></span>
   * <span data-ttu-id="40349-163">Owner CA - `$WRKDIR\certs\azure-iot-test-only.root.ca.cert.pem`</span><span class="sxs-lookup"><span data-stu-id="40349-163">Owner CA - `$WRKDIR\certs\azure-iot-test-only.root.ca.cert.pem`</span></span>

2.  <span data-ttu-id="40349-164">Set the `certificate` properties in the Security Daemon config yaml file to the path where you placed the certificate and key files.</span><span class="sxs-lookup"><span data-stu-id="40349-164">Set the `certificate` properties in the Security Daemon config yaml file to the path where you placed the certificate and key files.</span></span>

```yaml
certificates:
  device_ca_cert: "$CERTDIR\\certs\\new-edge-device-full-chain.cert.pem"
  device_ca_pk: "$CERTDIR\\private\\new-edge-device.key.pem"
  trusted_ca_certs: "$CERTDIR\\certs\\azure-iot-test-only.root.ca.cert.pem"
```
## <a name="deploy-edgehub-to-the-gateway"></a><span data-ttu-id="40349-165">Deploy EdgeHub to the gateway</span><span class="sxs-lookup"><span data-stu-id="40349-165">Deploy EdgeHub to the gateway</span></span>
<span data-ttu-id="40349-166">One of the key capabilities of Azure IoT Edge is being able to deploy modules to your IoT Edge devices from the cloud.</span><span class="sxs-lookup"><span data-stu-id="40349-166">One of the key capabilities of Azure IoT Edge is being able to deploy modules to your IoT Edge devices from the cloud.</span></span> <span data-ttu-id="40349-167">This section has you create a seemingly empty deployment; however Edge Hub is automatcially added to all deployments even if there are no other modules present.</span><span class="sxs-lookup"><span data-stu-id="40349-167">This section has you create a seemingly empty deployment; however Edge Hub is automatcially added to all deployments even if there are no other modules present.</span></span> <span data-ttu-id="40349-168">Edge Hub is the only module you need on an Edge Device to have it act as a transparent gateway so creating an empty deployment is enough.</span><span class="sxs-lookup"><span data-stu-id="40349-168">Edge Hub is the only module you need on an Edge Device to have it act as a transparent gateway so creating an empty deployment is enough.</span></span> 
1. <span data-ttu-id="40349-169">In the Azure portal, navigate to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="40349-169">In the Azure portal, navigate to your IoT hub.</span></span>
2. <span data-ttu-id="40349-170">Go to **IoT Edge** and select your IoT Edge device that you want to use as a gateway.</span><span class="sxs-lookup"><span data-stu-id="40349-170">Go to **IoT Edge** and select your IoT Edge device that you want to use as a gateway.</span></span>
3. <span data-ttu-id="40349-171">Select **Set Modules**.</span><span class="sxs-lookup"><span data-stu-id="40349-171">Select **Set Modules**.</span></span>
4. <span data-ttu-id="40349-172">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="40349-172">Select **Next**.</span></span>
5. <span data-ttu-id="40349-173">In the **Specify routes** step, you should have a default route that sends all messages from all modules to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="40349-173">In the **Specify routes** step, you should have a default route that sends all messages from all modules to IoT Hub.</span></span> <span data-ttu-id="40349-174">If not, add the following code then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="40349-174">If not, add the following code then select **Next**.</span></span>
   ```JSON
   {
       "routes": {
           "route": "FROM /* INTO $upstream"
       }
   }
   ```
6. <span data-ttu-id="40349-175">In the Review template step, select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="40349-175">In the Review template step, select **Submit**.</span></span>

## <a name="installation-on-the-downstream-device"></a><span data-ttu-id="40349-176">Installation on the downstream device</span><span class="sxs-lookup"><span data-stu-id="40349-176">Installation on the downstream device</span></span>
<span data-ttu-id="40349-177">A downstream device can be any application using the [Azure IoT device SDK][lnk-devicesdk], such as the simple one described in [Connect your device to your IoT hub using .NET][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="40349-177">A downstream device can be any application using the [Azure IoT device SDK][lnk-devicesdk], such as the simple one described in [Connect your device to your IoT hub using .NET][lnk-iothub-getstarted].</span></span> <span data-ttu-id="40349-178">A downstream device application has to trust the **owner CA** certificate in order to validate the TLS connections to the gateway devices.</span><span class="sxs-lookup"><span data-stu-id="40349-178">A downstream device application has to trust the **owner CA** certificate in order to validate the TLS connections to the gateway devices.</span></span> <span data-ttu-id="40349-179">This step can usually be performed in two ways: at the OS level, or (for certain languages) at the application level.</span><span class="sxs-lookup"><span data-stu-id="40349-179">This step can usually be performed in two ways: at the OS level, or (for certain languages) at the application level.</span></span>

### <a name="os-level"></a><span data-ttu-id="40349-180">OS level</span><span class="sxs-lookup"><span data-stu-id="40349-180">OS level</span></span>
<span data-ttu-id="40349-181">Installing this certificate in the OS certificate store will allow all applications to use the owner CA certificate as a trusted certificate.</span><span class="sxs-lookup"><span data-stu-id="40349-181">Installing this certificate in the OS certificate store will allow all applications to use the owner CA certificate as a trusted certificate.</span></span>

* <span data-ttu-id="40349-182">Ubuntu - Here is an example of how to install a CA certificate on an Ubuntu host.</span><span class="sxs-lookup"><span data-stu-id="40349-182">Ubuntu - Here is an example of how to install a CA certificate on an Ubuntu host.</span></span>

   ```cmd
   sudo cp $CERTDIR/certs/azure-iot-test-only.root.ca.cert.pem  /usr/local/share/ca-certificates/azure-iot-test-only.root.ca.cert.pem.crt
   sudo update-ca-certificates
   ```
 
    <span data-ttu-id="40349-183">You should see a message saying, "Updating certificates in /etc/ssl/certs... 1 added, 0 removed; done."</span><span class="sxs-lookup"><span data-stu-id="40349-183">You should see a message saying, "Updating certificates in /etc/ssl/certs... 1 added, 0 removed; done."</span></span>

* <span data-ttu-id="40349-184">Windows - Here is an example of how to install a CA certificate on an Windows host.</span><span class="sxs-lookup"><span data-stu-id="40349-184">Windows - Here is an example of how to install a CA certificate on an Windows host.</span></span>
  * <span data-ttu-id="40349-185">On the start menu type in "Manage computer certificates".</span><span class="sxs-lookup"><span data-stu-id="40349-185">On the start menu type in "Manage computer certificates".</span></span> <span data-ttu-id="40349-186">This should bring up a utility called `certlm`.</span><span class="sxs-lookup"><span data-stu-id="40349-186">This should bring up a utility called `certlm`.</span></span>
  * <span data-ttu-id="40349-187">Navigate to Certificates Local Computer --> Trusted Root Certificates --> Certificates --> Right click --> All Tasks --> Import to launch the certificate import wizard.</span><span class="sxs-lookup"><span data-stu-id="40349-187">Navigate to Certificates Local Computer --> Trusted Root Certificates --> Certificates --> Right click --> All Tasks --> Import to launch the certificate import wizard.</span></span>
  * <span data-ttu-id="40349-188">Follow the steps as directed and import certificate file $CERTDIR/certs/azure-iot-test-only.root.ca.cert.pem.</span><span class="sxs-lookup"><span data-stu-id="40349-188">Follow the steps as directed and import certificate file $CERTDIR/certs/azure-iot-test-only.root.ca.cert.pem.</span></span>
  * <span data-ttu-id="40349-189">When completed, you should see a "Successfully imported" message.</span><span class="sxs-lookup"><span data-stu-id="40349-189">When completed, you should see a "Successfully imported" message.</span></span>

### <a name="application-level"></a><span data-ttu-id="40349-190">Application level</span><span class="sxs-lookup"><span data-stu-id="40349-190">Application level</span></span>
<span data-ttu-id="40349-191">For .NET applications, you can add the following snippet to trust a certificate in PEM format.</span><span class="sxs-lookup"><span data-stu-id="40349-191">For .NET applications, you can add the following snippet to trust a certificate in PEM format.</span></span> <span data-ttu-id="40349-192">Initialize the variable `certPath` with `$CERTDIR\certs\azure-iot-test-only.root.ca.cert.pem`.</span><span class="sxs-lookup"><span data-stu-id="40349-192">Initialize the variable `certPath` with `$CERTDIR\certs\azure-iot-test-only.root.ca.cert.pem`.</span></span>

   ```
   using System.Security.Cryptography.X509Certificates;

   ...

   X509Store store = new X509Store(StoreName.Root, StoreLocation.CurrentUser);
   store.Open(OpenFlags.ReadWrite);
   store.Add(new X509Certificate2(X509Certificate2.CreateFromCertFile(certPath)));
   store.Close();
   ```

## <a name="connect-the-downstream-device-to-the-gateway"></a><span data-ttu-id="40349-193">Connect the downstream device to the gateway</span><span class="sxs-lookup"><span data-stu-id="40349-193">Connect the downstream device to the gateway</span></span>
<span data-ttu-id="40349-194">You must initialize the IoT Hub device sdk with a connection string referring to the hostname of the gateway device.</span><span class="sxs-lookup"><span data-stu-id="40349-194">You must initialize the IoT Hub device sdk with a connection string referring to the hostname of the gateway device.</span></span> <span data-ttu-id="40349-195">This is done by appending the `GatewayHostName` property to your device connection string.</span><span class="sxs-lookup"><span data-stu-id="40349-195">This is done by appending the `GatewayHostName` property to your device connection string.</span></span> <span data-ttu-id="40349-196">For instance, here is a sample device connection string for a device, to which we appended the `GatewayHostName` property:</span><span class="sxs-lookup"><span data-stu-id="40349-196">For instance, here is a sample device connection string for a device, to which we appended the `GatewayHostName` property:</span></span>

   ```
   HostName=yourHub.azure-devices.net;DeviceId=yourDevice;SharedAccessKey=XXXYYYZZZ=;GatewayHostName=mygateway.contoso.com
   ```

   >[!NOTE]
   ><span data-ttu-id="40349-197">This is a sample command which tests that everything has been set up correctly.</span><span class="sxs-lookup"><span data-stu-id="40349-197">This is a sample command which tests that everything has been set up correctly.</span></span> <span data-ttu-id="40349-198">You sohuld a message saying "verified OK".</span><span class="sxs-lookup"><span data-stu-id="40349-198">You sohuld a message saying "verified OK".</span></span>
   >
   ><span data-ttu-id="40349-199">openssl s_client -connect mygateway.contoso.com:8883 -CAfile $CERTDIR/certs/azure-iot-test-only.root.ca.cert.pem -showcerts</span><span class="sxs-lookup"><span data-stu-id="40349-199">openssl s_client -connect mygateway.contoso.com:8883 -CAfile $CERTDIR/certs/azure-iot-test-only.root.ca.cert.pem -showcerts</span></span>

## <a name="routing-messages-from-downstream-devices"></a><span data-ttu-id="40349-200">Routing messages from downstream devices</span><span class="sxs-lookup"><span data-stu-id="40349-200">Routing messages from downstream devices</span></span>
<span data-ttu-id="40349-201">The IoT Edge runtime can route messages sent from downstream devices just like messages sent by modules.</span><span class="sxs-lookup"><span data-stu-id="40349-201">The IoT Edge runtime can route messages sent from downstream devices just like messages sent by modules.</span></span> <span data-ttu-id="40349-202">This allows you to perform analytics in a module running on the gateway before sending any data to the cloud.</span><span class="sxs-lookup"><span data-stu-id="40349-202">This allows you to perform analytics in a module running on the gateway before sending any data to the cloud.</span></span> <span data-ttu-id="40349-203">The below route would be used to send messages from a downstream device named `sensor` to a module name `ai_insights`.</span><span class="sxs-lookup"><span data-stu-id="40349-203">The below route would be used to send messages from a downstream device named `sensor` to a module name `ai_insights`.</span></span>

   ```json
   { "routes":{ "sensorToAIInsightsInput1":"FROM /messages/* WHERE NOT IS_DEFINED($connectionModuleId) INTO BrokeredEndpoint(\"/modules/ai_insights/inputs/input1\")", "AIInsightsToIoTHub":"FROM /messages/modules/ai_insights/outputs/output1 INTO $upstream" } }
   ```

<span data-ttu-id="40349-204">Refer to the [module composition article][lnk-module-composition] for more details on message routing.</span><span class="sxs-lookup"><span data-stu-id="40349-204">Refer to the [module composition article][lnk-module-composition] for more details on message routing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40349-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="40349-205">Next steps</span></span>
<span data-ttu-id="40349-206">[Understand the requirements and tools for developing IoT Edge modules][lnk-module-dev].</span><span class="sxs-lookup"><span data-stu-id="40349-206">[Understand the requirements and tools for developing IoT Edge modules][lnk-module-dev].</span></span>

<!-- Images -->
[1]: ./media/how-to-create-transparent-gateway/gateway-setup.png

<!-- Links -->
[lnk-install-windows-x64]: ./how-to-install-iot-edge-windows-with-windows.md
[lnk-module-composition]: ./module-composition.md
[lnk-devicesdk]: ../iot-hub/iot-hub-devguide-sdks.md
[lnk-tutorial1-win]: tutorial-simulate-device-windows.md
[lnk-tutorial1-lin]: tutorial-simulate-device-linux.md
[lnk-edge-as-gateway]: ./iot-edge-as-gateway.md
[lnk-module-dev]: module-development.md
[lnk-iothub-getstarted]: ../iot-hub/quickstart-send-telemetry-dotnet.md
[lnk-iothub-x509]: ../iot-hub/iot-hub-x509ca-overview.md
[lnk-iothub-secure-deployment]: ../iot-hub/iot-hub-security-deployment.md
[lnk-iothub-tokens]: ../iot-hub/iot-hub-devguide-security.md#security-tokens
[lnk-iothub-throttles-quotas]: ../iot-hub/iot-hub-devguide-quotas-throttling.md
[lnk-iothub-devicetwins]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-iothub-c2d]: ../iot-hub/iot-hub-devguide-messages-c2d.md
[lnk-ca-scripts]: https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md
[lnk-modbus-module]: https://github.com/Azure/iot-edge-modbus
