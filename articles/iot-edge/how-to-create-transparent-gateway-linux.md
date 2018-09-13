---
title: Create a transparent gateway with Azure IoT Edge - Linux | Microsoft Docs
description: Use Azure IoT Edge to create a transparent gateway that can process information for multiple devices
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 6/20/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: f8ac885444c0ba52802024be9a78dfc0737e2673
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869465"
---
# <a name="create-a-linux-iot-edge-device-that-acts-as-a-transparent-gateway"></a><span data-ttu-id="bb3c2-103">Create a Linux IoT Edge device that acts as a transparent gateway</span><span class="sxs-lookup"><span data-stu-id="bb3c2-103">Create a Linux IoT Edge device that acts as a transparent gateway</span></span>

<span data-ttu-id="bb3c2-104">This article provides detailed instructions for using an IoT Edge device as a transparent gateway.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-104">This article provides detailed instructions for using an IoT Edge device as a transparent gateway.</span></span> <span data-ttu-id="bb3c2-105">For the rest of this article, the term *IoT Edge gateway* refers to an IoT Edge device used as a transparent gateway.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-105">For the rest of this article, the term *IoT Edge gateway* refers to an IoT Edge device used as a transparent gateway.</span></span> <span data-ttu-id="bb3c2-106">For more detailed information, see [How an IoT Edge device can be used as a gateway][lnk-edge-as-gateway], which gives a conceptual overview.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-106">For more detailed information, see [How an IoT Edge device can be used as a gateway][lnk-edge-as-gateway], which gives a conceptual overview.</span></span>

>[!NOTE]
><span data-ttu-id="bb3c2-107">Currently:</span><span class="sxs-lookup"><span data-stu-id="bb3c2-107">Currently:</span></span>
> * <span data-ttu-id="bb3c2-108">If the gateway is disconnected from IoT Hub, downstream devices cannot authenticate with the gateway.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-108">If the gateway is disconnected from IoT Hub, downstream devices cannot authenticate with the gateway.</span></span>
> * <span data-ttu-id="bb3c2-109">Edge-enabled devices can't connect to IoT Edge gateways.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-109">Edge-enabled devices can't connect to IoT Edge gateways.</span></span> 
> * <span data-ttu-id="bb3c2-110">Downstream devices can't use file upload.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-110">Downstream devices can't use file upload.</span></span>

<span data-ttu-id="bb3c2-111">The hard part about creating a transparent gateway is securely connecting the gateway to downstream devices.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-111">The hard part about creating a transparent gateway is securely connecting the gateway to downstream devices.</span></span> <span data-ttu-id="bb3c2-112">Azure IoT Edge allows you to use PKI infrastructure to set up secure TLS connections between these devices.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-112">Azure IoT Edge allows you to use PKI infrastructure to set up secure TLS connections between these devices.</span></span> <span data-ttu-id="bb3c2-113">In this case, we’re allowing a downstream device to connect to an IoT Edge device acting as a transparent gateway.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-113">In this case, we’re allowing a downstream device to connect to an IoT Edge device acting as a transparent gateway.</span></span>  <span data-ttu-id="bb3c2-114">To maintain reasonable security, the downstream device should confirm the identity of the Edge device because you only want your devices connecting to your gateways and not a potentially malicious gateway.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-114">To maintain reasonable security, the downstream device should confirm the identity of the Edge device because you only want your devices connecting to your gateways and not a potentially malicious gateway.</span></span>

<span data-ttu-id="bb3c2-115">You can create any certificate infrastructure that enables the trust required for your device-gateway topology.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-115">You can create any certificate infrastructure that enables the trust required for your device-gateway topology.</span></span> <span data-ttu-id="bb3c2-116">In this article, we assume the same certificate setup that you would use to enable [X.509 CA security][lnk-iothub-x509] in IoT Hub, which involves an X.509 CA certificate associated to a specific IoT hub (the IoT hub owner CA), and a series of certificates, signed with this CA, and a CA for the Edge device.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-116">In this article, we assume the same certificate setup that you would use to enable [X.509 CA security][lnk-iothub-x509] in IoT Hub, which involves an X.509 CA certificate associated to a specific IoT hub (the IoT hub owner CA), and a series of certificates, signed with this CA, and a CA for the Edge device.</span></span>

![Gateway setup][1]

<span data-ttu-id="bb3c2-118">The gateway presents its Edge device CA certificate to the downstream device during the initiation of the connection.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-118">The gateway presents its Edge device CA certificate to the downstream device during the initiation of the connection.</span></span> <span data-ttu-id="bb3c2-119">The downstream device checks to make sure the Edge device CA certificate is signed by the owner CA certificate.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-119">The downstream device checks to make sure the Edge device CA certificate is signed by the owner CA certificate.</span></span> <span data-ttu-id="bb3c2-120">This process allows the downstream device to confirm the gateway comes from a trusted source.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-120">This process allows the downstream device to confirm the gateway comes from a trusted source.</span></span>

<span data-ttu-id="bb3c2-121">The following steps walk you through the process of creating the certificates and installing them in the right places.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-121">The following steps walk you through the process of creating the certificates and installing them in the right places.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb3c2-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bb3c2-122">Prerequisites</span></span>
1.  <span data-ttu-id="bb3c2-123">Install the Azure IoT Edge runtime on a Linux device you want to use as the transparent gateway.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-123">Install the Azure IoT Edge runtime on a Linux device you want to use as the transparent gateway.</span></span>
   * <span data-ttu-id="bb3c2-124">[Linux x64][lnk-install-linux-x64]</span><span class="sxs-lookup"><span data-stu-id="bb3c2-124">[Linux x64][lnk-install-linux-x64]</span></span>
   * <span data-ttu-id="bb3c2-125">[Linux ARM32][lnk-install-linux-arm]</span><span class="sxs-lookup"><span data-stu-id="bb3c2-125">[Linux ARM32][lnk-install-linux-arm]</span></span>

2.  <span data-ttu-id="bb3c2-126">Obtain the scripts to generate the required non-production certificates with the following command.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-126">Obtain the scripts to generate the required non-production certificates with the following command.</span></span> <span data-ttu-id="bb3c2-127">These scripts help you create the necessary certificates to set up a transparent gateway.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-127">These scripts help you create the necessary certificates to set up a transparent gateway.</span></span> 

   ```cmd
   git clone https://github.com/Azure/azure-iot-sdk-c.git
   ```

3. <span data-ttu-id="bb3c2-128">These scripts use OpenSSL to generate the required certificates and OpenSSL requires some setup.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-128">These scripts use OpenSSL to generate the required certificates and OpenSSL requires some setup.</span></span>
   
   1. <span data-ttu-id="bb3c2-129">Navigate to the directory in which you want to work.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-129">Navigate to the directory in which you want to work.</span></span> <span data-ttu-id="bb3c2-130">From here on we'll refer to this as $WRKDIR.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-130">From here on we'll refer to this as $WRKDIR.</span></span>  <span data-ttu-id="bb3c2-131">All files will be created in this directory.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-131">All files will be created in this directory.</span></span>

      <span data-ttu-id="bb3c2-132">cd $WRKDIR</span><span class="sxs-lookup"><span data-stu-id="bb3c2-132">cd $WRKDIR</span></span>
   
   1. <span data-ttu-id="bb3c2-133">Copy config and script files into your working directory.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-133">Copy config and script files into your working directory.</span></span>

      ```cmd
      cp azure-iot-sdk-c/tools/CACertificates/*.cnf .
      cp azure-iot-sdk-c/tools/CACertificates/certGen.sh .
      chmod 700 certGen.sh 
      ```

## <a name="certificate-creation"></a><span data-ttu-id="bb3c2-134">Certificate creation</span><span class="sxs-lookup"><span data-stu-id="bb3c2-134">Certificate creation</span></span>
1.  <span data-ttu-id="bb3c2-135">Create the owner CA certificate and one intermediate certificate.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-135">Create the owner CA certificate and one intermediate certificate.</span></span> <span data-ttu-id="bb3c2-136">These are all placed in `$WRKDIR`.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-136">These are all placed in `$WRKDIR`.</span></span>

   ```cmd
   ./certGen.sh create_root_and_intermediate
   ```

   <span data-ttu-id="bb3c2-137">The outputs of the script execution are the following certificates and keys:</span><span class="sxs-lookup"><span data-stu-id="bb3c2-137">The outputs of the script execution are the following certificates and keys:</span></span>
   * <span data-ttu-id="bb3c2-138">Certificates</span><span class="sxs-lookup"><span data-stu-id="bb3c2-138">Certificates</span></span>
      * `$WRKDIR/certs/azure-iot-test-only.root.ca.cert.pem`
      * `$WRKDIR/certs/azure-iot-test-only.intermediate.cert.pem`
   * <span data-ttu-id="bb3c2-139">Keys</span><span class="sxs-lookup"><span data-stu-id="bb3c2-139">Keys</span></span>
      * `$WRKDIR/private/azure-iot-test-only.root.ca.key.pem`
      * `$WRKDIR/private/azure-iot-test-only.intermediate.key.pem`

2.  <span data-ttu-id="bb3c2-140">Create the Edge device CA certificate and private key with the command below.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-140">Create the Edge device CA certificate and private key with the command below.</span></span>

   >[!NOTE]
   > <span data-ttu-id="bb3c2-141">**DO NOT** use a name that is the same as the gateway's DNS host name.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-141">**DO NOT** use a name that is the same as the gateway's DNS host name.</span></span> <span data-ttu-id="bb3c2-142">Doing so will cause client certification against these certificates to fail.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-142">Doing so will cause client certification against these certificates to fail.</span></span>

   ```cmd
   ./certGen.sh create_edge_device_certificate "<gateway device name>"
   ```

   <span data-ttu-id="bb3c2-143">The outputs of the script execution are the following certificates and key:</span><span class="sxs-lookup"><span data-stu-id="bb3c2-143">The outputs of the script execution are the following certificates and key:</span></span>
   * `$WRKDIR/certs/new-edge-device.*`
   * `$WRKDIR/private/new-edge-device.key.pem`

## <a name="certificate-chain-creation"></a><span data-ttu-id="bb3c2-144">Certificate chain creation</span><span class="sxs-lookup"><span data-stu-id="bb3c2-144">Certificate chain creation</span></span>
<span data-ttu-id="bb3c2-145">Create a certificate chain from the owner CA certificate, intermediate certificate, and Edge device CA certificate with the command below.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-145">Create a certificate chain from the owner CA certificate, intermediate certificate, and Edge device CA certificate with the command below.</span></span> <span data-ttu-id="bb3c2-146">Placing it in a chain file allows you to easily install it on your Edge device acting as a transparent gateway.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-146">Placing it in a chain file allows you to easily install it on your Edge device acting as a transparent gateway.</span></span>

   ```cmd
   cat ./certs/new-edge-device.cert.pem ./certs/azure-iot-test-only.intermediate.cert.pem ./certs/azure-iot-test-only.root.ca.cert.pem > ./certs/new-edge-device-full-chain.cert.pem
   ```

## <a name="installation-on-the-gateway"></a><span data-ttu-id="bb3c2-147">Installation on the gateway</span><span class="sxs-lookup"><span data-stu-id="bb3c2-147">Installation on the gateway</span></span>
1.  <span data-ttu-id="bb3c2-148">Copy the following files from $WRKDIR anywhere on your Edge device, we'll refer to that as $CERTDIR.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-148">Copy the following files from $WRKDIR anywhere on your Edge device, we'll refer to that as $CERTDIR.</span></span> <span data-ttu-id="bb3c2-149">If you generated the certificates on your Edge device skip this step.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-149">If you generated the certificates on your Edge device skip this step.</span></span>

   * <span data-ttu-id="bb3c2-150">Device CA certificate -  `$WRKDIR/certs/new-edge-device-full-chain.cert.pem`</span><span class="sxs-lookup"><span data-stu-id="bb3c2-150">Device CA certificate -  `$WRKDIR/certs/new-edge-device-full-chain.cert.pem`</span></span>
   * <span data-ttu-id="bb3c2-151">Device CA private key - `$WRKDIR/private/new-edge-device.key.pem`</span><span class="sxs-lookup"><span data-stu-id="bb3c2-151">Device CA private key - `$WRKDIR/private/new-edge-device.key.pem`</span></span>
   * <span data-ttu-id="bb3c2-152">Owner CA - `$WRKDIR/certs/azure-iot-test-only.root.ca.cert.pem`</span><span class="sxs-lookup"><span data-stu-id="bb3c2-152">Owner CA - `$WRKDIR/certs/azure-iot-test-only.root.ca.cert.pem`</span></span>
   
2. <span data-ttu-id="bb3c2-153">Open the IoT Edge configuration file.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-153">Open the IoT Edge configuration file.</span></span> <span data-ttu-id="bb3c2-154">It is a protected file so you may have to use elevated privileges to access it.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-154">It is a protected file so you may have to use elevated privileges to access it.</span></span>
   
   ```bash
   sudo nano /etc/iotedge/config.yaml
   ```

3.  <span data-ttu-id="bb3c2-155">Set the `certificate` properties in the Iot Edge Daemon config yaml file to the path where you placed the certificate and key files.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-155">Set the `certificate` properties in the Iot Edge Daemon config yaml file to the path where you placed the certificate and key files.</span></span>

   ```yaml
   certificates:
     device_ca_cert: "$CERTDIR/certs/new-edge-device-full-chain.cert.pem"
     device_ca_pk: "$CERTDIR/private/new-edge-device.key.pem"
     trusted_ca_certs: "$CERTDIR/certs/azure-iot-test-only.root.ca.cert.pem"
   ```

## <a name="deploy-edgehub-to-the-gateway"></a><span data-ttu-id="bb3c2-156">Deploy EdgeHub to the gateway</span><span class="sxs-lookup"><span data-stu-id="bb3c2-156">Deploy EdgeHub to the gateway</span></span>
<span data-ttu-id="bb3c2-157">One of the key capabilities of Azure IoT Edge is being able to deploy modules to your IoT Edge devices from the cloud.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-157">One of the key capabilities of Azure IoT Edge is being able to deploy modules to your IoT Edge devices from the cloud.</span></span> <span data-ttu-id="bb3c2-158">This section has you create a seemingly empty deployment; however Edge Hub is automatically added to all deployments even if there are no other modules present.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-158">This section has you create a seemingly empty deployment; however Edge Hub is automatically added to all deployments even if there are no other modules present.</span></span> <span data-ttu-id="bb3c2-159">Edge Hub is the only module you need on an Edge Device to have it act as a transparent gateway so creating an empty deployment is enough.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-159">Edge Hub is the only module you need on an Edge Device to have it act as a transparent gateway so creating an empty deployment is enough.</span></span> 
1. <span data-ttu-id="bb3c2-160">In the Azure portal, navigate to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-160">In the Azure portal, navigate to your IoT hub.</span></span>
2. <span data-ttu-id="bb3c2-161">Go to **IoT Edge** and select your IoT Edge device that you want to use as a gateway.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-161">Go to **IoT Edge** and select your IoT Edge device that you want to use as a gateway.</span></span>
3. <span data-ttu-id="bb3c2-162">Select **Set Modules**.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-162">Select **Set Modules**.</span></span>
4. <span data-ttu-id="bb3c2-163">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-163">Select **Next**.</span></span>
5. <span data-ttu-id="bb3c2-164">In the **Specify routes** step, you should have a default route that sends all messages from all modules to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-164">In the **Specify routes** step, you should have a default route that sends all messages from all modules to IoT Hub.</span></span> <span data-ttu-id="bb3c2-165">If not, add the following code then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-165">If not, add the following code then select **Next**.</span></span>
   ```JSON
   {
       "routes": {
           "route": "FROM /* INTO $upstream"
       }
   }
   ```
6. <span data-ttu-id="bb3c2-166">In the Review template step, select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-166">In the Review template step, select **Submit**.</span></span>

## <a name="installation-on-the-downstream-device"></a><span data-ttu-id="bb3c2-167">Installation on the downstream device</span><span class="sxs-lookup"><span data-stu-id="bb3c2-167">Installation on the downstream device</span></span>
<span data-ttu-id="bb3c2-168">A downstream device can be any application using the [Azure IoT device SDK][lnk-devicesdk], such as the simple one described in [Connect your device to your IoT hub using .NET][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="bb3c2-168">A downstream device can be any application using the [Azure IoT device SDK][lnk-devicesdk], such as the simple one described in [Connect your device to your IoT hub using .NET][lnk-iothub-getstarted].</span></span> <span data-ttu-id="bb3c2-169">A downstream device application has to trust the **owner CA** certificate in order to validate the TLS connections to the gateway devices.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-169">A downstream device application has to trust the **owner CA** certificate in order to validate the TLS connections to the gateway devices.</span></span> <span data-ttu-id="bb3c2-170">This step can usually be performed in two ways: at the OS level, or (for certain languages) at the application level.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-170">This step can usually be performed in two ways: at the OS level, or (for certain languages) at the application level.</span></span>

### <a name="os-level"></a><span data-ttu-id="bb3c2-171">OS level</span><span class="sxs-lookup"><span data-stu-id="bb3c2-171">OS level</span></span>
<span data-ttu-id="bb3c2-172">Installing this certificate in the OS certificate store will allow all applications to use the owner CA certificate as a trusted certificate.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-172">Installing this certificate in the OS certificate store will allow all applications to use the owner CA certificate as a trusted certificate.</span></span>

* <span data-ttu-id="bb3c2-173">Ubuntu - Here is an example of how to install a CA certificate on an Ubuntu host.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-173">Ubuntu - Here is an example of how to install a CA certificate on an Ubuntu host.</span></span>

   ```cmd
   sudo cp $CERTDIR/certs/azure-iot-test-only.root.ca.cert.pem  /usr/local/share/ca-certificates/azure-iot-test-only.root.ca.cert.pem.crt
   sudo update-ca-certificates
   ```
 
    <span data-ttu-id="bb3c2-174">You should see a message saying, "Updating certificates in /etc/ssl/certs... 1 added, 0 removed; done."</span><span class="sxs-lookup"><span data-stu-id="bb3c2-174">You should see a message saying, "Updating certificates in /etc/ssl/certs... 1 added, 0 removed; done."</span></span>

* <span data-ttu-id="bb3c2-175">Windows - Here is an example of how to install a CA certificate on an Windows host.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-175">Windows - Here is an example of how to install a CA certificate on an Windows host.</span></span>
  * <span data-ttu-id="bb3c2-176">On the start menu type in "Manage computer certificates".</span><span class="sxs-lookup"><span data-stu-id="bb3c2-176">On the start menu type in "Manage computer certificates".</span></span> <span data-ttu-id="bb3c2-177">This should bring up a utility called `certlm`.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-177">This should bring up a utility called `certlm`.</span></span>
  * <span data-ttu-id="bb3c2-178">Navigate to Certificates Local Computer --> Trusted Root Certificates --> Certificates --> Right click --> All Tasks --> Import to launch the certificate import wizard.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-178">Navigate to Certificates Local Computer --> Trusted Root Certificates --> Certificates --> Right click --> All Tasks --> Import to launch the certificate import wizard.</span></span>
  * <span data-ttu-id="bb3c2-179">Follow the steps as directed and import certificate file $CERTDIR/certs/azure-iot-test-only.root.ca.cert.pem.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-179">Follow the steps as directed and import certificate file $CERTDIR/certs/azure-iot-test-only.root.ca.cert.pem.</span></span>
  * <span data-ttu-id="bb3c2-180">When completed, you should see a "Successfully imported" message.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-180">When completed, you should see a "Successfully imported" message.</span></span>

### <a name="application-level"></a><span data-ttu-id="bb3c2-181">Application level</span><span class="sxs-lookup"><span data-stu-id="bb3c2-181">Application level</span></span>
<span data-ttu-id="bb3c2-182">For .NET applications, you can add the following snippet to trust a certificate in PEM format.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-182">For .NET applications, you can add the following snippet to trust a certificate in PEM format.</span></span> <span data-ttu-id="bb3c2-183">Initialize the variable `certPath` with `$CERTDIR/certs/azure-iot-test-only.root.ca.cert.pem`.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-183">Initialize the variable `certPath` with `$CERTDIR/certs/azure-iot-test-only.root.ca.cert.pem`.</span></span>

   ```
   using System.Security.Cryptography.X509Certificates;

   ...

   X509Store store = new X509Store(StoreName.Root, StoreLocation.CurrentUser);
   store.Open(OpenFlags.ReadWrite);
   store.Add(new X509Certificate2(X509Certificate2.CreateFromCertFile(certPath)));
   store.Close();
   ```

## <a name="connect-the-downstream-device-to-the-gateway"></a><span data-ttu-id="bb3c2-184">Connect the downstream device to the gateway</span><span class="sxs-lookup"><span data-stu-id="bb3c2-184">Connect the downstream device to the gateway</span></span>
<span data-ttu-id="bb3c2-185">You must initialize the IoT Hub device sdk with a connection string referring to the hostname of the gateway device.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-185">You must initialize the IoT Hub device sdk with a connection string referring to the hostname of the gateway device.</span></span> <span data-ttu-id="bb3c2-186">This is done by appending the `GatewayHostName` property to your device connection string.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-186">This is done by appending the `GatewayHostName` property to your device connection string.</span></span> <span data-ttu-id="bb3c2-187">For instance, here is a sample device connection string for a device, to which we appended the `GatewayHostName` property:</span><span class="sxs-lookup"><span data-stu-id="bb3c2-187">For instance, here is a sample device connection string for a device, to which we appended the `GatewayHostName` property:</span></span>

   ```
   HostName=yourHub.azure-devices.net;DeviceId=yourDevice;SharedAccessKey=XXXYYYZZZ=;GatewayHostName=mygateway.contoso.com
   ```

   >[!NOTE]
   ><span data-ttu-id="bb3c2-188">This is a sample command which tests that everything has been set up correctly.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-188">This is a sample command which tests that everything has been set up correctly.</span></span> <span data-ttu-id="bb3c2-189">You sohuld a message saying "verified OK".</span><span class="sxs-lookup"><span data-stu-id="bb3c2-189">You sohuld a message saying "verified OK".</span></span>
   >
   ><span data-ttu-id="bb3c2-190">openssl s_client -connect mygateway.contoso.com:8883 -CAfile $CERTDIR/certs/azure-iot-test-only.root.ca.cert.pem -showcerts</span><span class="sxs-lookup"><span data-stu-id="bb3c2-190">openssl s_client -connect mygateway.contoso.com:8883 -CAfile $CERTDIR/certs/azure-iot-test-only.root.ca.cert.pem -showcerts</span></span>

## <a name="routing-messages-from-downstream-devices"></a><span data-ttu-id="bb3c2-191">Routing messages from downstream devices</span><span class="sxs-lookup"><span data-stu-id="bb3c2-191">Routing messages from downstream devices</span></span>
<span data-ttu-id="bb3c2-192">The IoT Edge runtime can route messages sent from downstream devices just like messages sent by modules.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-192">The IoT Edge runtime can route messages sent from downstream devices just like messages sent by modules.</span></span> <span data-ttu-id="bb3c2-193">This allows you to perform analytics in a module running on the gateway before sending any data to the cloud.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-193">This allows you to perform analytics in a module running on the gateway before sending any data to the cloud.</span></span> <span data-ttu-id="bb3c2-194">The below route would be used to send messages from a downstream device named `sensor` to a module name `ai_insights`.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-194">The below route would be used to send messages from a downstream device named `sensor` to a module name `ai_insights`.</span></span>

   ```json
   { "routes":{ "sensorToAIInsightsInput1":"FROM /messages/* WHERE NOT IS_DEFINED($connectionModuleId) INTO BrokeredEndpoint(\"/modules/ai_insights/inputs/input1\")", "AIInsightsToIoTHub":"FROM /messages/modules/ai_insights/outputs/output1 INTO $upstream" } }
   ```

<span data-ttu-id="bb3c2-195">Refer to the [module composition article][lnk-module-composition] for more details on message routing.</span><span class="sxs-lookup"><span data-stu-id="bb3c2-195">Refer to the [module composition article][lnk-module-composition] for more details on message routing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb3c2-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="bb3c2-196">Next steps</span></span>
<span data-ttu-id="bb3c2-197">[Understand the requirements and tools for developing IoT Edge modules][lnk-module-dev].</span><span class="sxs-lookup"><span data-stu-id="bb3c2-197">[Understand the requirements and tools for developing IoT Edge modules][lnk-module-dev].</span></span>

<!-- Images -->
[1]: ./media/how-to-create-transparent-gateway/gateway-setup.png

<!-- Links -->
[lnk-install-linux-x64]: ./how-to-install-iot-edge-linux.md
[lnk-install-linux-arm]: ./how-to-install-iot-edge-linux-arm.md
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
