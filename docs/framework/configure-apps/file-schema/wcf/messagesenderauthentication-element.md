---
title: <messageSenderAuthentication> 要素
ms.date: 03/30/2017
ms.assetid: 8d979dfc-a6f9-42ec-96d5-7fbc13a48118
ms.openlocfilehash: 1e63b6fa93e1abfa87c83da4b5d46f492c59b9bc
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69931373"
---
# <a name="messagesenderauthentication-element"></a>\<> 要素の認証の認証
ピアツーピア メッセージ送信者の認証オプションを指定します。  
  
 ピアツーピアプログラミングの詳細については、「[ピアツーピアネットワーク](../../../wcf/feature-details/peer-to-peer-networking.md)」を参照してください。  
  
 \<system.ServiceModel >  
\<<behaviors>  
\<endpointBehaviors>  
\<behavior>  
\<clientCredentials>  
\<ピア >  
\<messageSenderAuthentication>  
  
## <a name="syntax"></a>構文  
  
```xml  
<messageSenderAuthentication customCertificateValidatorType= "namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"
                             certificateValidationMode = "ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"
                             revocationMode="NoCheck/Online/Offline"
                             trustedStoreLocation="CurrentUser/LocalMachine" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`customCertificateValidatorType`|カスタム型の検証に使用される型およびアセンブリです。 `certificateValidationMode` が `Custom` に設定されている場合は、この属性を設定する必要があります。|  
|`certificateValidationMode`|資格情報の検証に使用される 3 つのモードのいずれかを指定します。 `Custom` に設定されている場合、`customCertificateValidator` も指定する必要があります。|  
|`revocationMode`|証明書失効リスト (CRL) のチェックに使用されるモードのいずれかです。|  
|`trustedStoreLocation`|2 つのシステム格納場所 (`LocalMachine` または `CurrentUser`) のいずれかです。 この値は、サービス証明書がクライアントにネゴシエートされるときに使用されます。 指定されたストアの場所にある**信頼さ**れた People ストアに対して検証が実行されます。|  
  
## <a name="customcertificatevalidatortype-attribute"></a>customCertificateValidatorType 属性  
  
|値|説明|  
|-----------|-----------------|  
|String|省略可能です。 タイプ名およびアセンブリと、タイプの検索に使用される他のデータを指定します。 少なくとも、名前空間とタイプ名が必要です。 省略可能な情報は、アセンブリ名、バージョン番号、カルチャ、および公開キー トークンです。|  
  
## <a name="certificatevalidationmode-attribute"></a>certificateValidationMode 属性  
  
|値|説明|  
|-----------|-----------------|  
|列挙型|省略可能です。 `None`、`PeerTrust`、`ChainTrust`、`PeerOrChainTrust`、`Custom` のいずれかの値にします。 既定値は、`ChainTrust` です。 既定値は `ChainTrust` です。<br /><br /> 詳細については、「[証明書の使用](../../../wcf/feature-details/working-with-certificates.md)」を参照してください。|  
  
## <a name="revocationmode-attribute"></a>revocationMode 属性  
  
|値|説明|  
|-----------|-----------------|  
|列挙型|`NoCheck`、`Online`、`Offline` のいずれかの値にします。 既定値は `Online` です。<br /><br /> 詳細については、「[証明書の使用](../../../wcf/feature-details/working-with-certificates.md)」を参照してください。|  
  
## <a name="trustedstorelocation-attribute"></a>trustedStoreLocation 属性  
  
|値|説明|  
|-----------|-----------------|  
|列挙型|`LocalMachine` または `CurrentUser` のいずれかの値にします。 既定値は、`CurrentUser` です。 クライアント アプリケーションがシステム アカウントで実行されている場合、証明書は通常 `LocalMachine` の下にあります。 クライアント アプリケーションがユーザー アカウントで実行されている場合、証明書は通常 `CurrentUser` の下にあります。 既定値は `CurrentUser` です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<peer>](peer-of-clientcredentials-element.md)|ピア サービスに対するクライアントの認証に使用される資格情報を指定します。|  
  
## <a name="remarks"></a>Remarks  
 メッセージ認証を選択した場合は、この要素を構成する必要があります。 出力チャネルの場合、各メッセージは、 [ \<証明書 >](certificate-element.md)によって提供される証明書を使用して署名されます。 すべてのメッセージは、アプリケーションに配信される前に、この要素の `customCertificateValidatorType` 属性で指定した検証を使用してメッセージ資格情報がチェックされます。 検証は、資格情報を受け入れることも拒否することもできます。  
  
## <a name="example"></a>例  
 次のコードは、メッセージ送信者検証モードを `PeerOrChainTrust` に設定します。  
  
```xml  
<behaviors>
  <endpointBehaviors>
    <behavior name="MyEndpointBehavior">
      <clientCredentials>
        <peer>
          <certificate findValue="www.contoso.com"
                       storeLocation="LocalMachine"
                       x509FindType="FindByIssuerName" />
          <messageSenderAuthentication certificateValidationMode="PeerOrChainTrust" />
          <messageSenderAuthentication certificateValidationMode="None" />
        </peer>
      </clientCredentials>
    </behavior>
  </endpointBehaviors>
</behaviors>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>
- <xref:System.ServiceModel.Security.PeerCredential.MessageSenderAuthentication%2A>
- <xref:System.ServiceModel.Configuration.PeerCredentialElement.MessageSenderAuthentication%2A>
- <xref:System.ServiceModel.Configuration.X509PeerCertificateAuthenticationElement>
- [証明書の使用](../../../wcf/feature-details/working-with-certificates.md)
- [ピアツーピア ネットワーク](../../../wcf/feature-details/peer-to-peer-networking.md)
- [ピアチャネルメッセージの認証](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/aa967730(v=vs.90))
- [ピアチャネルのカスタム認証](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751447(v=vs.90))
- [セキュリティによるピア チャネル アプリケーションの保護](../../../wcf/feature-details/securing-peer-channel-applications.md)
