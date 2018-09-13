---
title: Managing secrets in Service Fabric applications | Microsoft Docs
description: This article describes how to secure secret values in a Service Fabric application.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: ''
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: vturecek
ms.openlocfilehash: 0c0e8f782ecf8b4f7bfc256d3e2c89ca9b8cb25e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552135"
---
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="aa47f-103">Managing secrets in Service Fabric applications</span><span class="sxs-lookup"><span data-stu-id="aa47f-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="aa47f-104">This guide walks you through the steps of managing secrets in a Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="aa47f-104">This guide walks you through the steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="aa47f-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span><span class="sxs-lookup"><span data-stu-id="aa47f-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="aa47f-106">This guide uses Azure Key Vault to manage keys and secrets.</span><span class="sxs-lookup"><span data-stu-id="aa47f-106">This guide uses Azure Key Vault to manage keys and secrets.</span></span> <span data-ttu-id="aa47f-107">However, *using* secrets in an application is cloud platform-agnostic to allow applications to be deployed to a cluster hosted anywhere.</span><span class="sxs-lookup"><span data-stu-id="aa47f-107">However, *using* secrets in an application is cloud platform-agnostic to allow applications to be deployed to a cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="aa47f-108">Overview</span><span class="sxs-lookup"><span data-stu-id="aa47f-108">Overview</span></span>
<span data-ttu-id="aa47f-109">The recommended way to manage service configuration settings is through [service configuration packages][config-package].</span><span class="sxs-lookup"><span data-stu-id="aa47f-109">The recommended way to manage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="aa47f-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span><span class="sxs-lookup"><span data-stu-id="aa47f-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="aa47f-111">This is preferred to global configuration as it reduces the chances of a global service outage.</span><span class="sxs-lookup"><span data-stu-id="aa47f-111">This is preferred to global configuration as it reduces the chances of a global service outage.</span></span> <span data-ttu-id="aa47f-112">Encrypted secrets are no exception.</span><span class="sxs-lookup"><span data-stu-id="aa47f-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="aa47f-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span><span class="sxs-lookup"><span data-stu-id="aa47f-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="aa47f-114">The following diagram illustrates the basic flow for secret management in a Service Fabric application:</span><span class="sxs-lookup"><span data-stu-id="aa47f-114">The following diagram illustrates the basic flow for secret management in a Service Fabric application:</span></span>

![secret management overview][overview]

<span data-ttu-id="aa47f-116">There are four main steps in this flow:</span><span class="sxs-lookup"><span data-stu-id="aa47f-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="aa47f-117">Obtain a data encipherment certificate.</span><span class="sxs-lookup"><span data-stu-id="aa47f-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="aa47f-118">Install the certificate in your cluster.</span><span class="sxs-lookup"><span data-stu-id="aa47f-118">Install the certificate in your cluster.</span></span>
3. <span data-ttu-id="aa47f-119">Encrypt secret values when deploying an application with the certificate and inject them into a service's Settings.xml configuration file.</span><span class="sxs-lookup"><span data-stu-id="aa47f-119">Encrypt secret values when deploying an application with the certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="aa47f-120">Read encrypted values out of Settings.xml by decrypting with the same encipherment certificate.</span><span class="sxs-lookup"><span data-stu-id="aa47f-120">Read encrypted values out of Settings.xml by decrypting with the same encipherment certificate.</span></span> 

<span data-ttu-id="aa47f-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way to get certificates installed on Service Fabric clusters in Azure.</span><span class="sxs-lookup"><span data-stu-id="aa47f-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way to get certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="aa47f-122">If you are not deploying to Azure, you do not need to use Key Vault to manage secrets in Service Fabric applications.</span><span class="sxs-lookup"><span data-stu-id="aa47f-122">If you are not deploying to Azure, you do not need to use Key Vault to manage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="aa47f-123">Data encipherment certificate</span><span class="sxs-lookup"><span data-stu-id="aa47f-123">Data encipherment certificate</span></span>
<span data-ttu-id="aa47f-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span><span class="sxs-lookup"><span data-stu-id="aa47f-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="aa47f-125">The certificate must meet the following requirements:</span><span class="sxs-lookup"><span data-stu-id="aa47f-125">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="aa47f-126">The certificate must contain a private key.</span><span class="sxs-lookup"><span data-stu-id="aa47f-126">The certificate must contain a private key.</span></span>
* <span data-ttu-id="aa47f-127">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span><span class="sxs-lookup"><span data-stu-id="aa47f-127">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="aa47f-128">The certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span><span class="sxs-lookup"><span data-stu-id="aa47f-128">The certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="aa47f-129">For example, when creating a self-signed certificate using PowerShell, the `KeyUsage` flag must be set to `DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="aa47f-129">For example, when creating a self-signed certificate using PowerShell, the `KeyUsage` flag must be set to `DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-the-certificate-in-your-cluster"></a><span data-ttu-id="aa47f-130">Install the certificate in your cluster</span><span class="sxs-lookup"><span data-stu-id="aa47f-130">Install the certificate in your cluster</span></span>
<span data-ttu-id="aa47f-131">This certificate must be installed on each node in the cluster.</span><span class="sxs-lookup"><span data-stu-id="aa47f-131">This certificate must be installed on each node in the cluster.</span></span> <span data-ttu-id="aa47f-132">It will be used at runtime to decrypt values stored in a service's Settings.xml.</span><span class="sxs-lookup"><span data-stu-id="aa47f-132">It will be used at runtime to decrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="aa47f-133">See [how to create a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span><span class="sxs-lookup"><span data-stu-id="aa47f-133">See [how to create a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="aa47f-134">Encrypt application secrets</span><span class="sxs-lookup"><span data-stu-id="aa47f-134">Encrypt application secrets</span></span>
<span data-ttu-id="aa47f-135">The Service Fabric SDK has built-in secret encryption and decryption functions.</span><span class="sxs-lookup"><span data-stu-id="aa47f-135">The Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="aa47f-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span><span class="sxs-lookup"><span data-stu-id="aa47f-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="aa47f-137">The following PowerShell command is used to encrypt a secret.</span><span class="sxs-lookup"><span data-stu-id="aa47f-137">The following PowerShell command is used to encrypt a secret.</span></span> <span data-ttu-id="aa47f-138">This command only encrypts the value; it does **not** sign the cipher text.</span><span class="sxs-lookup"><span data-stu-id="aa47f-138">This command only encrypts the value; it does **not** sign the cipher text.</span></span> <span data-ttu-id="aa47f-139">You must use the same encipherment certificate that is installed in your cluster to produce ciphertext for secret values:</span><span class="sxs-lookup"><span data-stu-id="aa47f-139">You must use the same encipherment certificate that is installed in your cluster to produce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="aa47f-140">The resulting base-64 string contains both the secret ciphertext as well as information about the certificate that was used to encrypt it.</span><span class="sxs-lookup"><span data-stu-id="aa47f-140">The resulting base-64 string contains both the secret ciphertext as well as information about the certificate that was used to encrypt it.</span></span>  <span data-ttu-id="aa47f-141">The base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with the `IsEncrypted` attribute set to `true`:</span><span class="sxs-lookup"><span data-stu-id="aa47f-141">The base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with the `IsEncrypted` attribute set to `true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="aa47f-142">Inject application secrets into application instances</span><span class="sxs-lookup"><span data-stu-id="aa47f-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="aa47f-143">Ideally, deployment to different environments should be as automated as possible.</span><span class="sxs-lookup"><span data-stu-id="aa47f-143">Ideally, deployment to different environments should be as automated as possible.</span></span> <span data-ttu-id="aa47f-144">This can be accomplished by performing secret encryption in a build environment and providing the encrypted secrets as parameters when creating application instances.</span><span class="sxs-lookup"><span data-stu-id="aa47f-144">This can be accomplished by performing secret encryption in a build environment and providing the encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="aa47f-145">Use overridable parameters in Settings.xml</span><span class="sxs-lookup"><span data-stu-id="aa47f-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="aa47f-146">The Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span><span class="sxs-lookup"><span data-stu-id="aa47f-146">The Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="aa47f-147">Use the `MustOverride` attribute instead of providing a value for a parameter:</span><span class="sxs-lookup"><span data-stu-id="aa47f-147">Use the `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="aa47f-148">To override values in Settings.xml, declare an override parameter for the service in ApplicationManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="aa47f-148">To override values in Settings.xml, declare an override parameter for the service in ApplicationManifest.xml:</span></span>

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

<span data-ttu-id="aa47f-149">Now the value can be specified as an *application parameter* when creating an instance of the application.</span><span class="sxs-lookup"><span data-stu-id="aa47f-149">Now the value can be specified as an *application parameter* when creating an instance of the application.</span></span> <span data-ttu-id="aa47f-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span><span class="sxs-lookup"><span data-stu-id="aa47f-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="aa47f-151">Using PowerShell, the parameter is supplied to the `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="aa47f-151">Using PowerShell, the parameter is supplied to the `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="aa47f-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span><span class="sxs-lookup"><span data-stu-id="aa47f-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="aa47f-153">Decrypt secrets from service code</span><span class="sxs-lookup"><span data-stu-id="aa47f-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="aa47f-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access to certificates installed on the node without some extra setup.</span><span class="sxs-lookup"><span data-stu-id="aa47f-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access to certificates installed on the node without some extra setup.</span></span>

<span data-ttu-id="aa47f-155">When using a data encipherment certificate, you need to make sure NETWORK SERVICE or whatever user account the service is running under has access to the certificate's private key.</span><span class="sxs-lookup"><span data-stu-id="aa47f-155">When using a data encipherment certificate, you need to make sure NETWORK SERVICE or whatever user account the service is running under has access to the certificate's private key.</span></span> <span data-ttu-id="aa47f-156">Service Fabric will handle granting access for your service automatically if you configure it to do so.</span><span class="sxs-lookup"><span data-stu-id="aa47f-156">Service Fabric will handle granting access for your service automatically if you configure it to do so.</span></span> <span data-ttu-id="aa47f-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span><span class="sxs-lookup"><span data-stu-id="aa47f-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="aa47f-158">In the following example, the NETWORK SERVICE account is given read access to a certificate defined by its thumbprint:</span><span class="sxs-lookup"><span data-stu-id="aa47f-158">In the following example, the NETWORK SERVICE account is given read access to a certificate defined by its thumbprint:</span></span>

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> <span data-ttu-id="aa47f-159">When copying a certificate thumbprint from the certificate store snap-in on Windows, an invisible character is placed at the beginning of the thumbprint string.</span><span class="sxs-lookup"><span data-stu-id="aa47f-159">When copying a certificate thumbprint from the certificate store snap-in on Windows, an invisible character is placed at the beginning of the thumbprint string.</span></span> <span data-ttu-id="aa47f-160">This invisible character can cause an error when trying to locate a certificate by thumbprint, so be sure to delete this extra character.</span><span class="sxs-lookup"><span data-stu-id="aa47f-160">This invisible character can cause an error when trying to locate a certificate by thumbprint, so be sure to delete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="aa47f-161">Use application secrets in service code</span><span class="sxs-lookup"><span data-stu-id="aa47f-161">Use application secrets in service code</span></span>
<span data-ttu-id="aa47f-162">The API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have the `IsEncrypted` attribute set to `true`.</span><span class="sxs-lookup"><span data-stu-id="aa47f-162">The API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have the `IsEncrypted` attribute set to `true`.</span></span> <span data-ttu-id="aa47f-163">Since the encrypted text contains information about the certificate used for encryption, you do not need to manually find the certificate.</span><span class="sxs-lookup"><span data-stu-id="aa47f-163">Since the encrypted text contains information about the certificate used for encryption, you do not need to manually find the certificate.</span></span> <span data-ttu-id="aa47f-164">The certificate just needs to be installed on the node that the service is running on.</span><span class="sxs-lookup"><span data-stu-id="aa47f-164">The certificate just needs to be installed on the node that the service is running on.</span></span> <span data-ttu-id="aa47f-165">Simply call the `DecryptValue()` method to retrieve the original secret value:</span><span class="sxs-lookup"><span data-stu-id="aa47f-165">Simply call the `DecryptValue()` method to retrieve the original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="aa47f-166">Next Steps</span><span class="sxs-lookup"><span data-stu-id="aa47f-166">Next Steps</span></span>
<span data-ttu-id="aa47f-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="aa47f-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-application-secret-management/overview.png

