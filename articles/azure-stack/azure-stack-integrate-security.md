---
title: Azure Stack syslog forwarding
description: Learn how to integrate Azure Stack with monitoring solutions by using syslog forwarding
services: azure-stack
author: PatAltimore
manager: femila
ms.service: azure-stack
ms.topic: article
ms.date: 08/14/2018
ms.author: patricka
ms.reviewer: fiseraci
keywords: ''
ms.openlocfilehash: 8e59f2e7e2fceda7f30e12571cd9e2a552f76231
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865745"
---
# <a name="azure-stack-datacenter-integration---syslog-forwarding"></a><span data-ttu-id="571ff-103">Azure Stack datacenter integration - syslog forwarding</span><span class="sxs-lookup"><span data-stu-id="571ff-103">Azure Stack datacenter integration - syslog forwarding</span></span>

<span data-ttu-id="571ff-104">This article shows you how to use syslog to integrate Azure Stack infrastructure with external security solution(s) already deployed in your datacenter.</span><span class="sxs-lookup"><span data-stu-id="571ff-104">This article shows you how to use syslog to integrate Azure Stack infrastructure with external security solution(s) already deployed in your datacenter.</span></span> <span data-ttu-id="571ff-105">For example, a Security Information Event Management (SIEM) system.</span><span class="sxs-lookup"><span data-stu-id="571ff-105">For example, a Security Information Event Management (SIEM) system.</span></span> <span data-ttu-id="571ff-106">The syslog channel exposes audits, alerts, and security logs from all the components of the Azure Stack infrastructure.</span><span class="sxs-lookup"><span data-stu-id="571ff-106">The syslog channel exposes audits, alerts, and security logs from all the components of the Azure Stack infrastructure.</span></span> <span data-ttu-id="571ff-107">Use syslog forwarding to integrate with security monitoring solutions and/or to retrieve all audits, alerts, and security logs to store them for retention.</span><span class="sxs-lookup"><span data-stu-id="571ff-107">Use syslog forwarding to integrate with security monitoring solutions and/or to retrieve all audits, alerts, and security logs to store them for retention.</span></span> 

<span data-ttu-id="571ff-108">Starting with the 1805 update, Azure Stack has an integrated syslog client that, once configured, emits syslog messages with the payload in Common Event Format (CEF).</span><span class="sxs-lookup"><span data-stu-id="571ff-108">Starting with the 1805 update, Azure Stack has an integrated syslog client that, once configured, emits syslog messages with the payload in Common Event Format (CEF).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="571ff-109">Syslog forwarding is in preview.</span><span class="sxs-lookup"><span data-stu-id="571ff-109">Syslog forwarding is in preview.</span></span> <span data-ttu-id="571ff-110">It should not be relied upon in production environments.</span><span class="sxs-lookup"><span data-stu-id="571ff-110">It should not be relied upon in production environments.</span></span> 

<span data-ttu-id="571ff-111">The following diagram shows the main components that participate in the syslog integration.</span><span class="sxs-lookup"><span data-stu-id="571ff-111">The following diagram shows the main components that participate in the syslog integration.</span></span>

![Syslog forwarding diagram](media/azure-stack-integrate-security/syslog-forwarding.png)

## <a name="configuring-syslog-forwarding"></a><span data-ttu-id="571ff-113">Configuring syslog forwarding</span><span class="sxs-lookup"><span data-stu-id="571ff-113">Configuring syslog forwarding</span></span>

<span data-ttu-id="571ff-114">The syslog client in Azure Stack supports the following configurations:</span><span class="sxs-lookup"><span data-stu-id="571ff-114">The syslog client in Azure Stack supports the following configurations:</span></span>

1. <span data-ttu-id="571ff-115">**Syslog over TCP, with mutual authentication (client and server) and TLS 1.2 encryption:** In this configuration, both the syslog server and the syslog client can verify the identity of each other via certificates.</span><span class="sxs-lookup"><span data-stu-id="571ff-115">**Syslog over TCP, with mutual authentication (client and server) and TLS 1.2 encryption:** In this configuration, both the syslog server and the syslog client can verify the identity of each other via certificates.</span></span> <span data-ttu-id="571ff-116">The messages are sent over a TLS 1.2 encrypted channel.</span><span class="sxs-lookup"><span data-stu-id="571ff-116">The messages are sent over a TLS 1.2 encrypted channel.</span></span>

2. <span data-ttu-id="571ff-117">**Syslog over TCP with server authentication and TLS 1.2 encryption:** In this configuration, the syslog client can verify the identity of the syslog server via a certificate.</span><span class="sxs-lookup"><span data-stu-id="571ff-117">**Syslog over TCP with server authentication and TLS 1.2 encryption:** In this configuration, the syslog client can verify the identity of the syslog server via a certificate.</span></span> <span data-ttu-id="571ff-118">The messages are sent over a TLS 1.2 encrypted channel.</span><span class="sxs-lookup"><span data-stu-id="571ff-118">The messages are sent over a TLS 1.2 encrypted channel.</span></span>

3. <span data-ttu-id="571ff-119">**Syslog over TCP, with no encryption:** In this configuration, neither the syslog client nor syslog server verifies the identity of each other.</span><span class="sxs-lookup"><span data-stu-id="571ff-119">**Syslog over TCP, with no encryption:** In this configuration, neither the syslog client nor syslog server verifies the identity of each other.</span></span> <span data-ttu-id="571ff-120">The messages are sent in clear text over TCP.</span><span class="sxs-lookup"><span data-stu-id="571ff-120">The messages are sent in clear text over TCP.</span></span>

4. <span data-ttu-id="571ff-121">**Syslog over UDP, with no encryption:** In this configuration, neither the syslog client nor syslog server verifies the identity of each other.</span><span class="sxs-lookup"><span data-stu-id="571ff-121">**Syslog over UDP, with no encryption:** In this configuration, neither the syslog client nor syslog server verifies the identity of each other.</span></span> <span data-ttu-id="571ff-122">The messages are sent in clear text over UDP.</span><span class="sxs-lookup"><span data-stu-id="571ff-122">The messages are sent in clear text over UDP.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="571ff-123">Microsoft strongly recommends to use TCP using authentication and encryption (configuration #1 or, at the very minimum, #2) for production environments to protect against man-in-the-middle attacks and eavesdropping of messages.</span><span class="sxs-lookup"><span data-stu-id="571ff-123">Microsoft strongly recommends to use TCP using authentication and encryption (configuration #1 or, at the very minimum, #2) for production environments to protect against man-in-the-middle attacks and eavesdropping of messages.</span></span>

### <a name="cmdlets-to-configure-syslog-forwarding"></a><span data-ttu-id="571ff-124">Cmdlets to configure syslog forwarding</span><span class="sxs-lookup"><span data-stu-id="571ff-124">Cmdlets to configure syslog forwarding</span></span>
<span data-ttu-id="571ff-125">Configuring syslog forwarding requires access to the privileged endpoint (PEP).</span><span class="sxs-lookup"><span data-stu-id="571ff-125">Configuring syslog forwarding requires access to the privileged endpoint (PEP).</span></span> <span data-ttu-id="571ff-126">Two PowerShell cmdlets have been added to the PEP to configure the syslog forwarding:</span><span class="sxs-lookup"><span data-stu-id="571ff-126">Two PowerShell cmdlets have been added to the PEP to configure the syslog forwarding:</span></span>


```powershell
### cmdlet to pass the syslog server information to the client and to configure the transport protocol, the encryption and the authentication between the client and the server

Set-SyslogServer [-ServerName <String>] [-NoEncryption] [-SkipCertificateCheck] [-SkipCNCheck] [-UseUDP] [-Remove]

### cmdlet to configure the certificate for the syslog client to authenticate with the server

Set-SyslogClient [-pfxBinary <Byte[]>] [-CertPassword <SecureString>] [-RemoveCertificate] 
```
#### <a name="cmdlets-parameters"></a><span data-ttu-id="571ff-127">Cmdlets parameters</span><span class="sxs-lookup"><span data-stu-id="571ff-127">Cmdlets parameters</span></span>

<span data-ttu-id="571ff-128">Parameters for *Set-SyslogServer* cmdlet:</span><span class="sxs-lookup"><span data-stu-id="571ff-128">Parameters for *Set-SyslogServer* cmdlet:</span></span>

| <span data-ttu-id="571ff-129">Parameter</span><span class="sxs-lookup"><span data-stu-id="571ff-129">Parameter</span></span> | <span data-ttu-id="571ff-130">Description</span><span class="sxs-lookup"><span data-stu-id="571ff-130">Description</span></span> | <span data-ttu-id="571ff-131">Type</span><span class="sxs-lookup"><span data-stu-id="571ff-131">Type</span></span> |
|---------|---------| ---------|
| <span data-ttu-id="571ff-132">*ServerName*</span><span class="sxs-lookup"><span data-stu-id="571ff-132">*ServerName*</span></span> | <span data-ttu-id="571ff-133">FQDN or IP address of the syslog server</span><span class="sxs-lookup"><span data-stu-id="571ff-133">FQDN or IP address of the syslog server</span></span> | <span data-ttu-id="571ff-134">String</span><span class="sxs-lookup"><span data-stu-id="571ff-134">String</span></span> |
|<span data-ttu-id="571ff-135">*NoEncryption*</span><span class="sxs-lookup"><span data-stu-id="571ff-135">*NoEncryption*</span></span>| <span data-ttu-id="571ff-136">Force the client to send syslog messages in clear text</span><span class="sxs-lookup"><span data-stu-id="571ff-136">Force the client to send syslog messages in clear text</span></span> | <span data-ttu-id="571ff-137">flag</span><span class="sxs-lookup"><span data-stu-id="571ff-137">flag</span></span> | 
|<span data-ttu-id="571ff-138">*SkipCertificateCheck*</span><span class="sxs-lookup"><span data-stu-id="571ff-138">*SkipCertificateCheck*</span></span>| <span data-ttu-id="571ff-139">Skip validation of the certificate provided by the syslog server during initial TLS handshake</span><span class="sxs-lookup"><span data-stu-id="571ff-139">Skip validation of the certificate provided by the syslog server during initial TLS handshake</span></span> | <span data-ttu-id="571ff-140">flag</span><span class="sxs-lookup"><span data-stu-id="571ff-140">flag</span></span> |
|<span data-ttu-id="571ff-141">*SkipCNCheck*</span><span class="sxs-lookup"><span data-stu-id="571ff-141">*SkipCNCheck*</span></span>| <span data-ttu-id="571ff-142">Skip validation of the Common Name value of the certificate provided by the syslog server during initial TLS handshake</span><span class="sxs-lookup"><span data-stu-id="571ff-142">Skip validation of the Common Name value of the certificate provided by the syslog server during initial TLS handshake</span></span> | <span data-ttu-id="571ff-143">flag</span><span class="sxs-lookup"><span data-stu-id="571ff-143">flag</span></span> |
|<span data-ttu-id="571ff-144">*UseUDP*</span><span class="sxs-lookup"><span data-stu-id="571ff-144">*UseUDP*</span></span>| <span data-ttu-id="571ff-145">Use syslog with UDP as transport protocol</span><span class="sxs-lookup"><span data-stu-id="571ff-145">Use syslog with UDP as transport protocol</span></span> |<span data-ttu-id="571ff-146">flag</span><span class="sxs-lookup"><span data-stu-id="571ff-146">flag</span></span> |
|<span data-ttu-id="571ff-147">*Remove*</span><span class="sxs-lookup"><span data-stu-id="571ff-147">*Remove*</span></span>| <span data-ttu-id="571ff-148">Remove configuration of the server from the client and stop syslog forwarding</span><span class="sxs-lookup"><span data-stu-id="571ff-148">Remove configuration of the server from the client and stop syslog forwarding</span></span>| <span data-ttu-id="571ff-149">flag</span><span class="sxs-lookup"><span data-stu-id="571ff-149">flag</span></span> |

<span data-ttu-id="571ff-150">Parameters for *Set-SyslogClient* cmdlet:</span><span class="sxs-lookup"><span data-stu-id="571ff-150">Parameters for *Set-SyslogClient* cmdlet:</span></span>
| <span data-ttu-id="571ff-151">Parameter</span><span class="sxs-lookup"><span data-stu-id="571ff-151">Parameter</span></span> | <span data-ttu-id="571ff-152">Description</span><span class="sxs-lookup"><span data-stu-id="571ff-152">Description</span></span> | <span data-ttu-id="571ff-153">Type</span><span class="sxs-lookup"><span data-stu-id="571ff-153">Type</span></span> |
|---------|---------| ---------|
| <span data-ttu-id="571ff-154">*pfxBinary*</span><span class="sxs-lookup"><span data-stu-id="571ff-154">*pfxBinary*</span></span> | <span data-ttu-id="571ff-155">pfx file containing the certificate to be used by the client as identity to authenticate against the syslog server</span><span class="sxs-lookup"><span data-stu-id="571ff-155">pfx file containing the certificate to be used by the client as identity to authenticate against the syslog server</span></span>  | <span data-ttu-id="571ff-156">Byte[]</span><span class="sxs-lookup"><span data-stu-id="571ff-156">Byte[]</span></span> |
| <span data-ttu-id="571ff-157">*CertPassword*</span><span class="sxs-lookup"><span data-stu-id="571ff-157">*CertPassword*</span></span> |  <span data-ttu-id="571ff-158">Password to import the private key that is associated with the pfx file</span><span class="sxs-lookup"><span data-stu-id="571ff-158">Password to import the private key that is associated with the pfx file</span></span> | <span data-ttu-id="571ff-159">SecureString</span><span class="sxs-lookup"><span data-stu-id="571ff-159">SecureString</span></span> |
|<span data-ttu-id="571ff-160">*RemoveCertificate*</span><span class="sxs-lookup"><span data-stu-id="571ff-160">*RemoveCertificate*</span></span> | <span data-ttu-id="571ff-161">Remove certificate from the client</span><span class="sxs-lookup"><span data-stu-id="571ff-161">Remove certificate from the client</span></span> | <span data-ttu-id="571ff-162">flag</span><span class="sxs-lookup"><span data-stu-id="571ff-162">flag</span></span>|

### <a name="configuring-syslog-forwarding-with-tcp-mutual-authentication-and-tls-12-encryption"></a><span data-ttu-id="571ff-163">Configuring syslog forwarding with TCP, mutual authentication, and TLS 1.2 encryption</span><span class="sxs-lookup"><span data-stu-id="571ff-163">Configuring syslog forwarding with TCP, mutual authentication, and TLS 1.2 encryption</span></span>

<span data-ttu-id="571ff-164">In this configuration, the syslog client in Azure Stack forwards the messages to the syslog server over TCP, with TLS 1.2 encryption.</span><span class="sxs-lookup"><span data-stu-id="571ff-164">In this configuration, the syslog client in Azure Stack forwards the messages to the syslog server over TCP, with TLS 1.2 encryption.</span></span> <span data-ttu-id="571ff-165">During the initial handshake, the client verifies that the server provides a valid, trusted certificate; similarly, the client also provides a certificate to the server as proof of its identity.</span><span class="sxs-lookup"><span data-stu-id="571ff-165">During the initial handshake, the client verifies that the server provides a valid, trusted certificate; similarly, the client also provides a certificate to the server as proof of its identity.</span></span> <span data-ttu-id="571ff-166">This configuration is the most secure as it provides a full validation of the identity of both the client and the server and it sends messages over an encrypted channel.</span><span class="sxs-lookup"><span data-stu-id="571ff-166">This configuration is the most secure as it provides a full validation of the identity of both the client and the server and it sends messages over an encrypted channel.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="571ff-167">Microsoft strongly recommends to use this configuration for production environments.</span><span class="sxs-lookup"><span data-stu-id="571ff-167">Microsoft strongly recommends to use this configuration for production environments.</span></span> 

<span data-ttu-id="571ff-168">To configure syslog forwarding with TCP, mutual authentication, and TLS 1.2 encryption, run both these cmdlets:</span><span class="sxs-lookup"><span data-stu-id="571ff-168">To configure syslog forwarding with TCP, mutual authentication, and TLS 1.2 encryption, run both these cmdlets:</span></span>
```powershell
# Configure the server
Set-SyslogServer -ServerName <FQDN or ip address of syslog server>

# Provide certificate to the client to authenticate against the server
Set-SyslogClient -pfxBinary <Byte[] of pfx file> -CertPassword <SecureString, password for accessing the pfx file>
```
<span data-ttu-id="571ff-169">The client certificate must have the same root as the one provided during the deployment of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="571ff-169">The client certificate must have the same root as the one provided during the deployment of Azure Stack.</span></span> <span data-ttu-id="571ff-170">It also must contain a private key.</span><span class="sxs-lookup"><span data-stu-id="571ff-170">It also must contain a private key.</span></span>

```powershell
##Example on how to set your syslog client with the ceritificate for mutual authentication. 
##Run these cmdlets from your hardware lifecycle host or privileged access workstation.

$ErcsNodeName = "<yourPEP>"
$password = ConvertTo-SecureString -String "<your cloudAdmin account password" -AsPlainText -Force
 
$cloudAdmin = "<your cloudAdmin account name>"
$CloudAdminCred = New-Object System.Management.Automation.PSCredential ($cloudAdmin, $password)
 
$certPassword = $password
$certContent = Get-Content -Path C:\cert\<yourClientCertificate>.pfx -Encoding Byte
 
$params = @{ 
    ComputerName = $ErcsNodeName 
    Credential = $CloudAdminCred 
    ConfigurationName = "PrivilegedEndpoint" 
}

$session = New-PSSession @params
 
$params = @{ 
    Session = $session 
    ArgumentList = @($certContent, $certPassword) 
}
Write-Verbose "Invoking cmdlet to set syslog client certificate..." -Verbose 
Invoke-Command @params -ScriptBlock { 
    param($CertContent, $CertPassword) 
    Set-SyslogClient -PfxBinary $CertContent -CertPassword $CertPassword 
```

### <a name="configuring-syslog-forwarding-with-tcp-server-authentication-and-tls-12-encryption"></a><span data-ttu-id="571ff-171">Configuring syslog forwarding with TCP, Server authentication, and TLS 1.2 encryption</span><span class="sxs-lookup"><span data-stu-id="571ff-171">Configuring syslog forwarding with TCP, Server authentication, and TLS 1.2 encryption</span></span>

<span data-ttu-id="571ff-172">In this configuration, the syslog client in Azure Stack forwards the messages to the syslog server over TCP, with TLS 1.2 encryption.</span><span class="sxs-lookup"><span data-stu-id="571ff-172">In this configuration, the syslog client in Azure Stack forwards the messages to the syslog server over TCP, with TLS 1.2 encryption.</span></span> <span data-ttu-id="571ff-173">During the initial handshake, the client also verifies that the server provides a valid, trusted certificate.</span><span class="sxs-lookup"><span data-stu-id="571ff-173">During the initial handshake, the client also verifies that the server provides a valid, trusted certificate.</span></span> <span data-ttu-id="571ff-174">This prevents the client to send messages to untrusted destinations.</span><span class="sxs-lookup"><span data-stu-id="571ff-174">This prevents the client to send messages to untrusted destinations.</span></span>
<span data-ttu-id="571ff-175">TCP using authentication and encryption is the default configuration and represents the minimum level of security that Microsoft recommends for a production environment.</span><span class="sxs-lookup"><span data-stu-id="571ff-175">TCP using authentication and encryption is the default configuration and represents the minimum level of security that Microsoft recommends for a production environment.</span></span> 

```powershell
Set-SyslogServer -ServerName <FQDN or ip address of syslog server>
```

<span data-ttu-id="571ff-176">In case you want to test the integration of your syslog server with the Azure Stack client by using a self-signed and/or untrusted certificate, you can use these flags to skip the server validation performed by the client during the initial handshake.</span><span class="sxs-lookup"><span data-stu-id="571ff-176">In case you want to test the integration of your syslog server with the Azure Stack client by using a self-signed and/or untrusted certificate, you can use these flags to skip the server validation performed by the client during the initial handshake.</span></span>

```powershell
 #Skip validation of the Common Name value in the server certificate. Use this flag if you provide an IP address for your syslog server
 Set-SyslogServer -ServerName <FQDN or ip address of syslog server> -SkipCNCheck
 
 #Skip entirely the server certificate validation
 Set-SyslogServer -ServerName <FQDN or ip address of syslog server> -SkipCertificateCheck
```
> [!IMPORTANT]
> <span data-ttu-id="571ff-177">Microsoft recommends against the use of -SkipCertificateCheck flag for production environments.</span><span class="sxs-lookup"><span data-stu-id="571ff-177">Microsoft recommends against the use of -SkipCertificateCheck flag for production environments.</span></span> 


### <a name="configuring-syslog-forwarding-with-tcp-and-no-encryption"></a><span data-ttu-id="571ff-178">Configuring syslog forwarding with TCP and no encryption</span><span class="sxs-lookup"><span data-stu-id="571ff-178">Configuring syslog forwarding with TCP and no encryption</span></span>

<span data-ttu-id="571ff-179">In this configuration, the syslog client in Azure Stack forwards the messages to the syslog server over TCP, with no encryption.</span><span class="sxs-lookup"><span data-stu-id="571ff-179">In this configuration, the syslog client in Azure Stack forwards the messages to the syslog server over TCP, with no encryption.</span></span> <span data-ttu-id="571ff-180">The client does not verify the identity of the server nor it provides its own identity to the server for verification.</span><span class="sxs-lookup"><span data-stu-id="571ff-180">The client does not verify the identity of the server nor it provides its own identity to the server for verification.</span></span> 

```powershell
Set-SyslogServer -ServerName <FQDN or ip address of syslog server> -NoEncryption
```
> [!IMPORTANT]
> <span data-ttu-id="571ff-181">Microsoft recommends against using this configuration for production environments.</span><span class="sxs-lookup"><span data-stu-id="571ff-181">Microsoft recommends against using this configuration for production environments.</span></span> 


### <a name="configuring-syslog-forwarding-with-udp-and-no-encryption"></a><span data-ttu-id="571ff-182">Configuring syslog forwarding with UDP and no encryption</span><span class="sxs-lookup"><span data-stu-id="571ff-182">Configuring syslog forwarding with UDP and no encryption</span></span>

<span data-ttu-id="571ff-183">In this configuration, the syslog client in Azure Stack forwards the messages to the syslog server over UDP, with no encryption.</span><span class="sxs-lookup"><span data-stu-id="571ff-183">In this configuration, the syslog client in Azure Stack forwards the messages to the syslog server over UDP, with no encryption.</span></span> <span data-ttu-id="571ff-184">The client does not verify the identity of the server nor it provides its own identity to the server for verification.</span><span class="sxs-lookup"><span data-stu-id="571ff-184">The client does not verify the identity of the server nor it provides its own identity to the server for verification.</span></span> 

```powershell
Set-SyslogServer -ServerName <FQDN or ip address of syslog server> -UseUDP
```
<span data-ttu-id="571ff-185">While UDP with no encryption is the easiest to configure, it does not provide any protection against man-in-the-middle attacks and eavesdropping of messages.</span><span class="sxs-lookup"><span data-stu-id="571ff-185">While UDP with no encryption is the easiest to configure, it does not provide any protection against man-in-the-middle attacks and eavesdropping of messages.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="571ff-186">Microsoft recommends against using this configuration for production environments.</span><span class="sxs-lookup"><span data-stu-id="571ff-186">Microsoft recommends against using this configuration for production environments.</span></span> 


## <a name="removing-syslog-forwarding-configuration"></a><span data-ttu-id="571ff-187">Removing syslog forwarding configuration</span><span class="sxs-lookup"><span data-stu-id="571ff-187">Removing syslog forwarding configuration</span></span>

<span data-ttu-id="571ff-188">To remove the syslog server configuration altogether and stop syslog forwarding:</span><span class="sxs-lookup"><span data-stu-id="571ff-188">To remove the syslog server configuration altogether and stop syslog forwarding:</span></span>

<span data-ttu-id="571ff-189">**Remove the syslog server configuration from the client**</span><span class="sxs-lookup"><span data-stu-id="571ff-189">**Remove the syslog server configuration from the client**</span></span>

```PowerShell  
Set-SyslogServer -Remove
```

<span data-ttu-id="571ff-190">**Remove the client certificate from the client**</span><span class="sxs-lookup"><span data-stu-id="571ff-190">**Remove the client certificate from the client**</span></span>

```PowerShell  
Set-SyslogClient -RemoveCertificate
```

## <a name="verifying-the-syslog-setup"></a><span data-ttu-id="571ff-191">Verifying the syslog setup</span><span class="sxs-lookup"><span data-stu-id="571ff-191">Verifying the syslog setup</span></span>

<span data-ttu-id="571ff-192">If you successfully connected the syslog client to your syslog server, you should soon start receiving events.</span><span class="sxs-lookup"><span data-stu-id="571ff-192">If you successfully connected the syslog client to your syslog server, you should soon start receiving events.</span></span> <span data-ttu-id="571ff-193">If you don't see any event, verify the configuration of your syslog client, by running the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="571ff-193">If you don't see any event, verify the configuration of your syslog client, by running the following cmdlets:</span></span>

<span data-ttu-id="571ff-194">**Verify the server configuration in the syslog client**</span><span class="sxs-lookup"><span data-stu-id="571ff-194">**Verify the server configuration in the syslog client**</span></span>

```PowerShell  
Get-SyslogServer
```

<span data-ttu-id="571ff-195">**Verify the certificate setup in the syslog client**</span><span class="sxs-lookup"><span data-stu-id="571ff-195">**Verify the certificate setup in the syslog client**</span></span>

```PowerShell  
Get-SyslogClient
```

## <a name="syslog-message-schema"></a><span data-ttu-id="571ff-196">Syslog message schema</span><span class="sxs-lookup"><span data-stu-id="571ff-196">Syslog message schema</span></span>

<span data-ttu-id="571ff-197">The syslog forwarding of the Azure Stack infrastructure sends messages formatted in Common Event Format (CEF).</span><span class="sxs-lookup"><span data-stu-id="571ff-197">The syslog forwarding of the Azure Stack infrastructure sends messages formatted in Common Event Format (CEF).</span></span>
<span data-ttu-id="571ff-198">Each syslog message is structured based on this schema:</span><span class="sxs-lookup"><span data-stu-id="571ff-198">Each syslog message is structured based on this schema:</span></span> 

```Syslog
<Time> <Host> <CEF payload>
```

<span data-ttu-id="571ff-199">The CEF payload is based on the structure below, but the mapping for each field varies depending on the type of message (Windows Event, Alert created, Alert closed).</span><span class="sxs-lookup"><span data-stu-id="571ff-199">The CEF payload is based on the structure below, but the mapping for each field varies depending on the type of message (Windows Event, Alert created, Alert closed).</span></span>

```CEF
# Common Event Format schema
CEF: <Version>|<Device Vendor>|<Device Product>|<Device Version>|<Signature ID>|<Name>|<Severity>|<Extensions>
* Version: 0.0 
* Device Vendor: Microsoft
* Device Product: Microsoft Azure Stack
* Device Version: 1.0
```

### <a name="cef-mapping-for-windows-events"></a><span data-ttu-id="571ff-200">CEF mapping for Windows events</span><span class="sxs-lookup"><span data-stu-id="571ff-200">CEF mapping for Windows events</span></span>
```
* Signature ID: ProviderName:EventID
* Name: TaskName
* Severity: Level (for details, see the severity table below)
* Extension: Custom Extension Name (for details, see the Custom Extension table below)
```

<span data-ttu-id="571ff-201">Severity table for Windows events:</span><span class="sxs-lookup"><span data-stu-id="571ff-201">Severity table for Windows events:</span></span> 
| <span data-ttu-id="571ff-202">CEF Severity Value</span><span class="sxs-lookup"><span data-stu-id="571ff-202">CEF Severity Value</span></span> | <span data-ttu-id="571ff-203">Windows Event Level</span><span class="sxs-lookup"><span data-stu-id="571ff-203">Windows Event Level</span></span> | <span data-ttu-id="571ff-204">Numerical Value</span><span class="sxs-lookup"><span data-stu-id="571ff-204">Numerical Value</span></span> |
|--------------------|---------------------| ----------------|
|<span data-ttu-id="571ff-205">0</span><span class="sxs-lookup"><span data-stu-id="571ff-205">0</span></span>|<span data-ttu-id="571ff-206">Undefined</span><span class="sxs-lookup"><span data-stu-id="571ff-206">Undefined</span></span>|<span data-ttu-id="571ff-207">Value: 0.</span><span class="sxs-lookup"><span data-stu-id="571ff-207">Value: 0.</span></span> <span data-ttu-id="571ff-208">Indicates logs at all levels</span><span class="sxs-lookup"><span data-stu-id="571ff-208">Indicates logs at all levels</span></span>|
|<span data-ttu-id="571ff-209">10</span><span class="sxs-lookup"><span data-stu-id="571ff-209">10</span></span>|<span data-ttu-id="571ff-210">Critical</span><span class="sxs-lookup"><span data-stu-id="571ff-210">Critical</span></span>|<span data-ttu-id="571ff-211">Value: 1.</span><span class="sxs-lookup"><span data-stu-id="571ff-211">Value: 1.</span></span> <span data-ttu-id="571ff-212">Indicates logs for a critical alert</span><span class="sxs-lookup"><span data-stu-id="571ff-212">Indicates logs for a critical alert</span></span>|
|<span data-ttu-id="571ff-213">8</span><span class="sxs-lookup"><span data-stu-id="571ff-213">8</span></span>|<span data-ttu-id="571ff-214">Error</span><span class="sxs-lookup"><span data-stu-id="571ff-214">Error</span></span>| <span data-ttu-id="571ff-215">Value: 2.</span><span class="sxs-lookup"><span data-stu-id="571ff-215">Value: 2.</span></span> <span data-ttu-id="571ff-216">Indicates logs for an error</span><span class="sxs-lookup"><span data-stu-id="571ff-216">Indicates logs for an error</span></span>|
|<span data-ttu-id="571ff-217">5</span><span class="sxs-lookup"><span data-stu-id="571ff-217">5</span></span>|<span data-ttu-id="571ff-218">Warning</span><span class="sxs-lookup"><span data-stu-id="571ff-218">Warning</span></span>|<span data-ttu-id="571ff-219">Value: 3.</span><span class="sxs-lookup"><span data-stu-id="571ff-219">Value: 3.</span></span> <span data-ttu-id="571ff-220">Indicates logs for a warning</span><span class="sxs-lookup"><span data-stu-id="571ff-220">Indicates logs for a warning</span></span>|
|<span data-ttu-id="571ff-221">2</span><span class="sxs-lookup"><span data-stu-id="571ff-221">2</span></span>|<span data-ttu-id="571ff-222">Information</span><span class="sxs-lookup"><span data-stu-id="571ff-222">Information</span></span>|<span data-ttu-id="571ff-223">Value: 4.</span><span class="sxs-lookup"><span data-stu-id="571ff-223">Value: 4.</span></span> <span data-ttu-id="571ff-224">Indicates logs for an informational message</span><span class="sxs-lookup"><span data-stu-id="571ff-224">Indicates logs for an informational message</span></span>|
|<span data-ttu-id="571ff-225">0</span><span class="sxs-lookup"><span data-stu-id="571ff-225">0</span></span>|<span data-ttu-id="571ff-226">Verbose</span><span class="sxs-lookup"><span data-stu-id="571ff-226">Verbose</span></span>|<span data-ttu-id="571ff-227">Value: 5.</span><span class="sxs-lookup"><span data-stu-id="571ff-227">Value: 5.</span></span> <span data-ttu-id="571ff-228">Indicates logs at all levels</span><span class="sxs-lookup"><span data-stu-id="571ff-228">Indicates logs at all levels</span></span>|

<span data-ttu-id="571ff-229">Custom extension table for Windows events in Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="571ff-229">Custom extension table for Windows events in Azure Stack:</span></span>
| <span data-ttu-id="571ff-230">Custom Extension Name</span><span class="sxs-lookup"><span data-stu-id="571ff-230">Custom Extension Name</span></span> | <span data-ttu-id="571ff-231">Windows Event Example</span><span class="sxs-lookup"><span data-stu-id="571ff-231">Windows Event Example</span></span> | 
|-----------------------|---------|
|<span data-ttu-id="571ff-232">MasChannel</span><span class="sxs-lookup"><span data-stu-id="571ff-232">MasChannel</span></span> | <span data-ttu-id="571ff-233">System</span><span class="sxs-lookup"><span data-stu-id="571ff-233">System</span></span>|
|<span data-ttu-id="571ff-234">MasComputer</span><span class="sxs-lookup"><span data-stu-id="571ff-234">MasComputer</span></span> | <span data-ttu-id="571ff-235">test.azurestack.contoso.com</span><span class="sxs-lookup"><span data-stu-id="571ff-235">test.azurestack.contoso.com</span></span>|
|<span data-ttu-id="571ff-236">MasCorrelationActivityID</span><span class="sxs-lookup"><span data-stu-id="571ff-236">MasCorrelationActivityID</span></span>| <span data-ttu-id="571ff-237">C8F40D7C-3764-423B-A4FA-C994442238AF</span><span class="sxs-lookup"><span data-stu-id="571ff-237">C8F40D7C-3764-423B-A4FA-C994442238AF</span></span>|
|<span data-ttu-id="571ff-238">MasCorrelationRelatedActivityID</span><span class="sxs-lookup"><span data-stu-id="571ff-238">MasCorrelationRelatedActivityID</span></span>| <span data-ttu-id="571ff-239">C8F40D7C-3764-423B-A4FA-C994442238AF</span><span class="sxs-lookup"><span data-stu-id="571ff-239">C8F40D7C-3764-423B-A4FA-C994442238AF</span></span>|
|<span data-ttu-id="571ff-240">MasEventData</span><span class="sxs-lookup"><span data-stu-id="571ff-240">MasEventData</span></span>| <span data-ttu-id="571ff-241">svchost!!4132,G,0!!!!EseDiskFlushConsistency!!ESENT!!0x800000</span><span class="sxs-lookup"><span data-stu-id="571ff-241">svchost!!4132,G,0!!!!EseDiskFlushConsistency!!ESENT!!0x800000</span></span>|
|<span data-ttu-id="571ff-242">MasEventDescription</span><span class="sxs-lookup"><span data-stu-id="571ff-242">MasEventDescription</span></span>| <span data-ttu-id="571ff-243">The Group Policy settings for the user were processed successfully.</span><span class="sxs-lookup"><span data-stu-id="571ff-243">The Group Policy settings for the user were processed successfully.</span></span> <span data-ttu-id="571ff-244">There were no changes detected since the last successful processing of Group Policy.</span><span class="sxs-lookup"><span data-stu-id="571ff-244">There were no changes detected since the last successful processing of Group Policy.</span></span>|
|<span data-ttu-id="571ff-245">MasEventID</span><span class="sxs-lookup"><span data-stu-id="571ff-245">MasEventID</span></span>|<span data-ttu-id="571ff-246">1501</span><span class="sxs-lookup"><span data-stu-id="571ff-246">1501</span></span>|
|<span data-ttu-id="571ff-247">MasEventRecordID</span><span class="sxs-lookup"><span data-stu-id="571ff-247">MasEventRecordID</span></span>|<span data-ttu-id="571ff-248">26637</span><span class="sxs-lookup"><span data-stu-id="571ff-248">26637</span></span>|
|<span data-ttu-id="571ff-249">MasExecutionProcessID</span><span class="sxs-lookup"><span data-stu-id="571ff-249">MasExecutionProcessID</span></span> | <span data-ttu-id="571ff-250">29380</span><span class="sxs-lookup"><span data-stu-id="571ff-250">29380</span></span>|
|<span data-ttu-id="571ff-251">MasExecutionThreadID</span><span class="sxs-lookup"><span data-stu-id="571ff-251">MasExecutionThreadID</span></span> |<span data-ttu-id="571ff-252">25480</span><span class="sxs-lookup"><span data-stu-id="571ff-252">25480</span></span>|
|<span data-ttu-id="571ff-253">MasKeywords</span><span class="sxs-lookup"><span data-stu-id="571ff-253">MasKeywords</span></span> |<span data-ttu-id="571ff-254">0x8000000000000000</span><span class="sxs-lookup"><span data-stu-id="571ff-254">0x8000000000000000</span></span>|
|<span data-ttu-id="571ff-255">MasKeywordName</span><span class="sxs-lookup"><span data-stu-id="571ff-255">MasKeywordName</span></span> |<span data-ttu-id="571ff-256">Audit Success</span><span class="sxs-lookup"><span data-stu-id="571ff-256">Audit Success</span></span>|
|<span data-ttu-id="571ff-257">MasLevel</span><span class="sxs-lookup"><span data-stu-id="571ff-257">MasLevel</span></span> |<span data-ttu-id="571ff-258">4</span><span class="sxs-lookup"><span data-stu-id="571ff-258">4</span></span>|
|<span data-ttu-id="571ff-259">MasOpcode</span><span class="sxs-lookup"><span data-stu-id="571ff-259">MasOpcode</span></span> |<span data-ttu-id="571ff-260">1</span><span class="sxs-lookup"><span data-stu-id="571ff-260">1</span></span>|
|<span data-ttu-id="571ff-261">MasOpcodeName</span><span class="sxs-lookup"><span data-stu-id="571ff-261">MasOpcodeName</span></span> |<span data-ttu-id="571ff-262">info</span><span class="sxs-lookup"><span data-stu-id="571ff-262">info</span></span>|
|<span data-ttu-id="571ff-263">MasProviderEventSourceName</span><span class="sxs-lookup"><span data-stu-id="571ff-263">MasProviderEventSourceName</span></span> ||
|<span data-ttu-id="571ff-264">MasProviderGuid</span><span class="sxs-lookup"><span data-stu-id="571ff-264">MasProviderGuid</span></span> |<span data-ttu-id="571ff-265">AEA1B4FA-97D1-45F2-A64C-4D69FFFD92C9</span><span class="sxs-lookup"><span data-stu-id="571ff-265">AEA1B4FA-97D1-45F2-A64C-4D69FFFD92C9</span></span>|
|<span data-ttu-id="571ff-266">MasProviderName</span><span class="sxs-lookup"><span data-stu-id="571ff-266">MasProviderName</span></span> |<span data-ttu-id="571ff-267">Microsoft-Windows-GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="571ff-267">Microsoft-Windows-GroupPolicy</span></span>|
|<span data-ttu-id="571ff-268">MasSecurityUserId</span><span class="sxs-lookup"><span data-stu-id="571ff-268">MasSecurityUserId</span></span> |<span data-ttu-id="571ff-269">\<Windows SID\></span><span class="sxs-lookup"><span data-stu-id="571ff-269">\<Windows SID\></span></span> |
|<span data-ttu-id="571ff-270">MasTask</span><span class="sxs-lookup"><span data-stu-id="571ff-270">MasTask</span></span> |<span data-ttu-id="571ff-271">0</span><span class="sxs-lookup"><span data-stu-id="571ff-271">0</span></span>|
|<span data-ttu-id="571ff-272">MasTaskCategory</span><span class="sxs-lookup"><span data-stu-id="571ff-272">MasTaskCategory</span></span>| <span data-ttu-id="571ff-273">Process Creation</span><span class="sxs-lookup"><span data-stu-id="571ff-273">Process Creation</span></span>|
|<span data-ttu-id="571ff-274">MasUserData</span><span class="sxs-lookup"><span data-stu-id="571ff-274">MasUserData</span></span>|<span data-ttu-id="571ff-275">KB4093112!!5112!!Installed!!0x0!!WindowsUpdateAgent Xpath: /Event/UserData/\*</span><span class="sxs-lookup"><span data-stu-id="571ff-275">KB4093112!!5112!!Installed!!0x0!!WindowsUpdateAgent Xpath: /Event/UserData/\*</span></span>|
|<span data-ttu-id="571ff-276">MasVersion</span><span class="sxs-lookup"><span data-stu-id="571ff-276">MasVersion</span></span>|<span data-ttu-id="571ff-277">0</span><span class="sxs-lookup"><span data-stu-id="571ff-277">0</span></span>|

### <a name="cef-mapping-for-alerts-created"></a><span data-ttu-id="571ff-278">CEF mapping for alerts created</span><span class="sxs-lookup"><span data-stu-id="571ff-278">CEF mapping for alerts created</span></span>
```
* Signature ID: Microsoft Azure Stack Alert Creation : FaultTypeId
* Name: FaultTypeId : AlertId
* Severity: Alert Severity (for details, see alerts severity table below)
* Extension: Custom Extension Name (for details, see the Custom Extension table below)
```
<span data-ttu-id="571ff-279">Alerts severity table:</span><span class="sxs-lookup"><span data-stu-id="571ff-279">Alerts severity table:</span></span>
| <span data-ttu-id="571ff-280">Severity</span><span class="sxs-lookup"><span data-stu-id="571ff-280">Severity</span></span> | <span data-ttu-id="571ff-281">Level</span><span class="sxs-lookup"><span data-stu-id="571ff-281">Level</span></span> |
|----------|-------|
|<span data-ttu-id="571ff-282">0</span><span class="sxs-lookup"><span data-stu-id="571ff-282">0</span></span>|<span data-ttu-id="571ff-283">Undefined</span><span class="sxs-lookup"><span data-stu-id="571ff-283">Undefined</span></span>|
|<span data-ttu-id="571ff-284">10</span><span class="sxs-lookup"><span data-stu-id="571ff-284">10</span></span>|<span data-ttu-id="571ff-285">Critical</span><span class="sxs-lookup"><span data-stu-id="571ff-285">Critical</span></span>|
|<span data-ttu-id="571ff-286">5</span><span class="sxs-lookup"><span data-stu-id="571ff-286">5</span></span>|<span data-ttu-id="571ff-287">Warning</span><span class="sxs-lookup"><span data-stu-id="571ff-287">Warning</span></span>|

<span data-ttu-id="571ff-288">Custom Extension table for Alerts created in Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="571ff-288">Custom Extension table for Alerts created in Azure Stack:</span></span>
| <span data-ttu-id="571ff-289">Custom Extension Name</span><span class="sxs-lookup"><span data-stu-id="571ff-289">Custom Extension Name</span></span> | <span data-ttu-id="571ff-290">Example</span><span class="sxs-lookup"><span data-stu-id="571ff-290">Example</span></span> | 
|-----------------------|---------|
|<span data-ttu-id="571ff-291">MasEventDescription</span><span class="sxs-lookup"><span data-stu-id="571ff-291">MasEventDescription</span></span>|<span data-ttu-id="571ff-292">DESCRIPTION: A user account \<TestUser\> was created for \<TestDomain\>.</span><span class="sxs-lookup"><span data-stu-id="571ff-292">DESCRIPTION: A user account \<TestUser\> was created for \<TestDomain\>.</span></span> <span data-ttu-id="571ff-293">It's a potential security risk.</span><span class="sxs-lookup"><span data-stu-id="571ff-293">It's a potential security risk.</span></span> <span data-ttu-id="571ff-294">-- REMEDIATION: Contact support.</span><span class="sxs-lookup"><span data-stu-id="571ff-294">-- REMEDIATION: Contact support.</span></span> <span data-ttu-id="571ff-295">Customer Assistance is required to resolve this issue.</span><span class="sxs-lookup"><span data-stu-id="571ff-295">Customer Assistance is required to resolve this issue.</span></span> <span data-ttu-id="571ff-296">Do not try to resolve this issue without their assistance.</span><span class="sxs-lookup"><span data-stu-id="571ff-296">Do not try to resolve this issue without their assistance.</span></span> <span data-ttu-id="571ff-297">Before you open a support request, start the log file collection process using the guidance from https://aka.ms/azurestacklogfiles</span><span class="sxs-lookup"><span data-stu-id="571ff-297">Before you open a support request, start the log file collection process using the guidance from https://aka.ms/azurestacklogfiles</span></span> |

### <a name="cef-mapping-for-alerts-closed"></a><span data-ttu-id="571ff-298">CEF mapping for alerts closed</span><span class="sxs-lookup"><span data-stu-id="571ff-298">CEF mapping for alerts closed</span></span>
```
* Signature ID: Microsoft Azure Stack Alert Creation : FaultTypeId
* Name: FaultTypeId : AlertId
* Severity: Information
```

<span data-ttu-id="571ff-299">The example below shows a syslog message with CEF payload:</span><span class="sxs-lookup"><span data-stu-id="571ff-299">The example below shows a syslog message with CEF payload:</span></span>
```
2018:05:17:-23:59:28 -07:00 TestHost CEF:0.0|Microsoft|Microsoft Azure Stack|1.0|3|TITLE: User Account Created -- DESCRIPTION: A user account \<TestUser\> was created for \<TestDomain\>. It's a potential security risk. -- REMEDIATION: Please contact Support. Customer Assistance is required to resolve this issue. Do not try to resolve this issue without their assistance. Before you open a support request, start the log file collection process using the guidance from https://aka.ms/azurestacklogfiles|10
```
## <a name="next-steps"></a><span data-ttu-id="571ff-300">Next steps</span><span class="sxs-lookup"><span data-stu-id="571ff-300">Next steps</span></span>

[<span data-ttu-id="571ff-301">Servicing policy</span><span class="sxs-lookup"><span data-stu-id="571ff-301">Servicing policy</span></span>](azure-stack-servicing-policy.md)