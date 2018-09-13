---
title: Protect HLS content with Microsoft PlayReady or Apple FairPlay - Azure | Microsoft Docs
description: This topic gives an overview and shows how to use Azure Media Services to dynamically encrypt your HTTP Live Streaming (HLS) content with Apple FairPlay. It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 77d75362352221a0bd08e878ec4f84897bc14a9f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661342"
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a>Protect your HLS content with Apple FairPlay or Microsoft PlayReady
Azure Media Services enables you to dynamically encrypt your HTTP Live Streaming (HLS) content by using the following formats:  

* **AES-128 envelope clear key**

    The entire chunk is encrypted by using the **AES-128 CBC** mode. The decryption of the stream is supported by iOS and OS X player natively. For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).
* **Apple FairPlay**

    The individual video and audio samples are encrypted by using the **AES-128 CBC** mode. **FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV. Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.
* **Microsoft PlayReady**

The following image shows the **HLS + FairPlay or PlayReady dynamic encryption** workflow.

![Diagram of dynamic encryption workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

This topic demonstrates how to use Media Services to dynamically encrypt your HLS content with Apple FairPlay. It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.

> [!NOTE]
> If you also want to encrypt your HLS content with PlayReady, you need to create a common content key and associate it with your asset. You also need to configure the content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).
>
>

## <a name="requirements-and-considerations"></a>Requirements and considerations

The following are required when using Media Services to deliver HLS encrypted with FairPlay, and to deliver FairPlay licenses:

  * An Azure account. For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
  * A Media Services account. To create one, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).
  * Sign up with [Apple Development Program](https://developer.apple.com/).
  * Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/). State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package. There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK). You use ASK to configure FairPlay.
  * Azure Media Services .NET SDK version **3.6.0** or later.

The following things must be set on Media Services key delivery side:

  * **App Cert (AC)**: This is a .pfx file that contains the private key. You create this file and encrypt it with a password.

       When you configure a key delivery policy, you must provide that password and the .pfx file in Base64 format.

      The following steps describe how to generate a .pfx certificate file for FairPlay:

    1. Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.

        Go to the folder where the FairPlay certificate and other files delivered by Apple are.
    2. Run the following command from the command line. This converts the .cer file to a .pem file.

        "C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem
    3. Run the following command from the command line. This converts the .pem file to a .pfx file with the private key. The password for the .pfx file is then asked by OpenSSL.

        "C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt
  * **App Cert password**: The password for creating the .pfx file.
  * **App Cert password ID**: You must upload the password, similar to how they upload other Media Services keys. Use the **ContentKeyType.FairPlayPfxPassword** enum value to get the Media Services ID. This is what they need to use inside the key delivery policy option.
  * **iv**: This is a random value of 16 bytes. It must match the iv in the asset delivery policy. You generate the iv, and put it in both places: the asset delivery policy and the key delivery policy option.
  * **ASK**: This key is received when you generate the certification by using the Apple Developer portal. Each development team will receive a unique ASK. Save a copy of the ASK, and store it in a safe place. You will need to configure ASK as FairPlayAsk to Media Services later.
  * **ASK ID**: This ID is obtained when you upload ASK into Media Services. You must upload ASK by using the **ContentKeyType.FairPlayAsk** enum value. As the result, the Media Services ID is returned, and this is what should be used when setting the key delivery policy option.

The following things must be set by the FPS client side:

  * **App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload. Media Services needs to know about it because it is required by the player. The key delivery service decrypts it using the corresponding private key.

To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate. That process creates all three parts:

  * .der file
  * .pfx file
  * password for the .pfx

The following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a>Configure FairPlay dynamic encryption and license delivery services
The following are general steps for protecting your assets with FairPlay by using the Media Services license delivery service, and also by using dynamic encryption.

1. Create an asset, and upload files into the asset.
2. Encode the asset that contains the file to the adaptive bitrate MP4 set.
3. Create a content key, and associate it with the encoded asset.  
4. Configure the content key’s authorization policy. Specify the following:

   * The delivery method (in this case, FairPlay).
   * FairPlay policy options configuration. For details on how to configure FairPlay, see the **ConfigureFairPlayPolicyOptions()** method in the sample below.

     > [!NOTE]
     > Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.
     >
     >
   * Restrictions (open or token).
   * Information specific to the key delivery type that defines how the key is delivered to the client.
5. Configure the asset delivery policy. The delivery policy configuration includes:

   * The delivery protocol (HLS).
   * The type of dynamic encryption (common CBC encryption).
   * The license acquisition URL.

     > [!NOTE]
     > If you want to deliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have to configure separate delivery policies:
     >
     > * One IAssetDeliveryPolicy to configure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady
     > * Another IAssetDeliveryPolicy to configure FairPlay for HLS
     >
     >
6. Create an OnDemand locator to get a streaming URL.

## <a name="use-fairplay-key-delivery-by-player-apps"></a>Use FairPlay key delivery by player apps
You can develop player apps by using the iOS SDK. To be able to play FairPlay content, you have to implement the license exchange protocol. This protocol is not specified by Apple. It is up to each app how to send key delivery requests. The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:

    spc=<Base64 encoded SPC>

> [!NOTE]
> Azure Media Player doesn’t support FairPlay playback out of the box. To get FairPlay playback on MAC OS X, obtain the sample player from the Apple developer account.
>
>

## <a name="streaming-urls"></a>Streaming URLs
If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').

The following considerations apply:

* Only zero or one encryption type can be specified.
* The encryption type doesn't have to be specified in the URL if only one encryption was applied to the asset.
* The encryption type is case insensitive.
* The following encryption types can be specified:  
  * **cenc**:  Common encryption (PlayReady or Widevine)
  * **cbcs-aapl**: FairPlay
  * **cbc**: AES envelope encryption

## <a name="net-example-deliver-your-content-encrypted-with-fairplay"></a>.NET example: deliver your content encrypted with FairPlay
The following sample demonstrates the ability to use Media Services to deliver your content encrypted with FairPlay. This functionality was introduced in the Azure Media Services SDK for .NET version 3.6.0. The following NuGet package command was used to install the package:

    PM> Install-Package windowsazure.mediaservices -Version 3.6.0


1. Create a Console project.
2. Use NuGet to install and add the Azure Media Services .NET SDK.
3. Add additional references: System.Configuration.
4. Add a config file that contains the account name and key information:

        <?xml version="1.0" encoding="utf-8"?>
        <configuration>
            <startup>
                <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
            </startup>
              <appSettings>

                <add key="MediaServicesAccountName" value="AccountName"/>
                <add key="MediaServicesAccountKey" value="AccountKey"/>

                <add key="Issuer" value="http://testacs.com"/>
                <add key="Audience" value="urn:test"/>
              </appSettings>
        </configuration>
7. Overwrite the code in your Program.cs file with the code shown in this section.

    >[!NOTE]
    >There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy). You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies). For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.

        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
        using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
        using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
        using Newtonsoft.Json;
        using System.Security.Cryptography.X509Certificates;

        namespace DynamicEncryptionWithFairPlay
        {
            class Program
            {
                // Read values from the App.config file.
                private static readonly string _mediaServicesAccountName =
                    ConfigurationManager.AppSettings["MediaServicesAccountName"];
                private static readonly string _mediaServicesAccountKey =
                    ConfigurationManager.AppSettings["MediaServicesAccountKey"];

                private static readonly Uri _sampleIssuer =
                    new Uri(ConfigurationManager.AppSettings["Issuer"]);
                private static readonly Uri _sampleAudience =
                    new Uri(ConfigurationManager.AppSettings["Audience"]);

                // Field for service context.
                private static CloudMediaContext _context = null;
                private static MediaServicesCredentials _cachedCredentials = null;

                private static readonly string _mediaFiles =
                    Path.GetFullPath(@"../..\Media");

                private static readonly string _singleMP4File =
                    Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    // Create and cache the Media Services credentials in a static class variable.
                    _cachedCredentials = new MediaServicesCredentials(
                                    _mediaServicesAccountName,
                                    _mediaServicesAccountKey);
                    // Used the cached credentials to create CloudMediaContext.
                    _context = new CloudMediaContext(_cachedCredentials);

                    bool tokenRestriction = false;
                    string tokenTemplateString = null;

                    IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
                    Console.WriteLine("Uploaded asset: {0}", asset.Id);

                    IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
                    Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

                    IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
                    Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
                    Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
                    Console.WriteLine();

                    if (tokenRestriction)
                        tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
                    else
                        AddOpenAuthorizationPolicy(key);

                    Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
                    Console.WriteLine();

                    CreateAssetDeliveryPolicy(encodedAsset, key);
                    Console.WriteLine("Created asset delivery policy. \n");
                    Console.WriteLine();

                    if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
                    {
                        // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
                        // back into a TokenRestrictionTemplate class instance.
                        TokenRestrictionTemplate tokenTemplate =
                            TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

                        // Generate a test token based on the the data in the given TokenRestrictionTemplate.
                        // Note, you need to pass the key id Guid because we specified
                        // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
                        Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
                        string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                                                                DateTime.UtcNow.AddDays(365));
                        Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
                        Console.WriteLine();
                    }

                    string url = GetStreamingOriginLocator(encodedAsset);
                    Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

                    Console.ReadLine();
                }

                static public IAsset UploadFileAndCreateAsset(string singleFilePath)
                {
                    if (!File.Exists(singleFilePath))
                    {
                        Console.WriteLine("File does not exist.");
                        return null;
                    }

                    var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
                    IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return inputAsset;
                }

                static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
                {
                    var encodingPreset = "Adaptive Streaming";

                    IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

                    var mediaProcessors =
                        _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

                    var latestMediaProcessor =
                        mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

                    ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
                    encodeTask.InputAssets.Add(inputAsset);
                    encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset),     AssetCreationOptions.StorageEncrypted);

                    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
                    job.Submit();
                    job.GetExecutionProgressTask(CancellationToken.None).Wait();

                    return job.OutputMediaAssets[0];
                }

                static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
                {
                    // Create HLS SAMPLE AES encryption content key
                    Guid keyId = Guid.NewGuid();
                    byte[] contentKey = GetRandomBuffer(16);

                    IContentKey key = _context.ContentKeys.Create(
                                            keyId,
                                            contentKey,
                                            "ContentKey",
                                            ContentKeyType.CommonEncryptionCbcs);

                    // Associate the key with the asset.
                    asset.ContentKeys.Add(key);

                    return key;
                }


                static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
                {
                    // Create ContentKeyAuthorizationPolicy with Open restrictions
                    // and create authorization policy          

                    List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                            {
                                new ContentKeyAuthorizationPolicyRestriction
                                {
                                    Name = "Open",
                                    KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                                    Requirements = null
                                }
                            };


                    // Configure FairPlay policy option.
                    string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

                    IContentKeyAuthorizationPolicyOption FairPlayPolicy =
                        _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.FairPlay,
                        restrictions,
                        FairPlayConfiguration);


                    IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                                Result;

                    contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

                    // Associate the content key authorization policy with the content key.
                    contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                    contentKey = contentKey.UpdateAsync().Result;
                }

                public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
                {
                    string tokenTemplateString = GenerateTokenRequirements();

                    List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                            {
                                new ContentKeyAuthorizationPolicyRestriction
                                {
                                    Name = "Token Authorization Policy",
                                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                                    Requirements = tokenTemplateString,
                                }
                            };

                    // Configure FairPlay policy option.
                    string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


                    IContentKeyAuthorizationPolicyOption FairPlayPolicy =
                        _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                               ContentKeyDeliveryType.FairPlay,
                               restrictions,
                               FairPlayConfiguration);

                    IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                                Result;

                    contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

                    // Associate the content key authorization policy with the content key
                    contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                    contentKey = contentKey.UpdateAsync().Result;

                    return tokenTemplateString;
                }

                private static string ConfigureFairPlayPolicyOptions()
                {
                    // For testing you can provide all zeroes for ASK bytes together with the cert from Apple FPS SDK.
                    // However, for production you must use a real ASK from Apple bound to a real prod certificate.
                    byte[] askBytes = Guid.NewGuid().ToByteArray();
                    var askId = Guid.NewGuid();
                    // Key delivery retrieves askKey by askId and uses this key to generate the response.
                    IContentKey askKey = _context.ContentKeys.Create(
                                            askId,
                                            askBytes,
                                            "askKey",
                                            ContentKeyType.FairPlayASk);

                    //Customer password for creating the .pfx file.
                    string pfxPassword = "<customer password for creating the .pfx file>";
                    // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key to generate the response.
                    var pfxPasswordId = Guid.NewGuid();
                    byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
                    IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                                            pfxPasswordId,
                                            pfxPasswordBytes,
                                            "pfxPasswordKey",
                                            ContentKeyType.FairPlayPfxPassword);

                    // iv - 16 bytes random value, must match the iv in the asset delivery policy.
                    byte[] iv = Guid.NewGuid().ToByteArray();

                    //Specify the .pfx file created by the customer.
                    var appCert = new X509Certificate2("path to the .pfx file created by the customer", pfxPassword, X509KeyStorageFlags.Exportable);

                    string FairPlayConfiguration =
                        Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                            appCert,
                            pfxPassword,
                            pfxPasswordId,
                            askId,
                            iv);

                    return FairPlayConfiguration;
                }

                static private string GenerateTokenRequirements()
                {
                    TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

                    template.PrimaryVerificationKey = new SymmetricVerificationKey();
                    template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
                    template.Audience = _sampleAudience.ToString();
                    template.Issuer = _sampleIssuer.ToString();
                    template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

                    return TokenRestrictionTemplateSerializer.Serialize(template);
                }

                static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
                {
                    var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

                    var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

                    FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

                    // Get the FairPlay license service URL.
                    Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

                    // The reason the below code replaces "https://" with "skd://" is because
                    // in the IOS player sample code which you obtained in Apple developer account,
                    // the player only recognizes a Key URL that starts with skd://.
                    // However, if you are using a customized player,
                    // you can choose whatever protocol you want.
                    // For example, "https".

                    Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
                        new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
                        {
                            {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                            {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
                        };

                    var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                            "AssetDeliveryPolicy",
                        AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
                        AssetDeliveryProtocol.HLS,
                        assetDeliveryPolicyConfiguration);

                    // Add AssetDelivery Policy to the asset
                    asset.DeliveryPolicies.Add(assetDeliveryPolicy);

                }


                /// <summary>
                /// Gets the streaming origin locator.
                /// </summary>
                /// <param name="assets"></param>
                /// <returns></returns>
                static public string GetStreamingOriginLocator(IAsset asset)
                {

                    // Get a reference to the streaming manifest file from the  
                    // collection of files in the asset.

                    var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                                 EndsWith(".ism")).
                                                 FirstOrDefault();

                    // Create a 30-day readonly access policy.
                    IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
                        TimeSpan.FromDays(30),
                        AccessPermissions.Read);

                    // Create a locator to the streaming content on an origin.
                    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
                        policy,
                        DateTime.UtcNow.AddMinutes(-5));

                    // Create a URL to the manifest file.
                    return originLocator.Path + assetFile.Name;
                }

                static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
                {
                    Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
                        ((IJob)sender).Name,
                        e.CurrentState,
                        DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
                }

                static private byte[] GetRandomBuffer(int length)
                {
                    var returnValue = new byte[length];

                    using (var rng =
                        new System.Security.Cryptography.RNGCryptoServiceProvider())
                    {
                        rng.GetBytes(returnValue);
                    }

                    return returnValue;
                }
            }
        }


## <a name="next-steps-media-services-learning-paths"></a>Next steps: Media Services learning paths
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

