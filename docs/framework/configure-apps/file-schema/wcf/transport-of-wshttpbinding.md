---
title: <transport> の <wsHttpBinding>
ms.date: 03/30/2017
ms.assetid: 21e38acf-450a-4bda-82b6-de305e1f7cd8
ms.openlocfilehash: 384267e3d018d714f95356461eb303bc9ec0cb3e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69934638"
---
# <a name="transport-of-wshttpbinding"></a>\<wsHttpBinding > の\<transport >

HTTP トランスポートの認証設定を定義します。

\<system.serviceModel>\
\<bindings>\
\<wsHttpBinding > \
\<バインド > \
\<セキュリティ > \
\<transport>

## <a name="syntax"></a>構文

```xml
<wsHttpBinding>
  <binding>
    <security mode="None|Transport|TransportWithMessageCredential|TransportCredentialOnly">
      <transport clientCredentialType="Basic|Certificate|Digest|None|Ntlm|Windows"
                 proxyCredentialType="Basic|Digest|None|Ntlm|Windows"
                 realm="string" />
        <extendedProtectionPolicy policyEnforcement="Never|WhenSupported|Always"
                                  protectionScenario="TransportSelected|TrustedProxy">
          <customServiceNames>
          </customServiceNames>
        </extendedProtectionPolicy>
      </transport>
    </security>
  </binding>
</wsHttpBinding>
```

## <a name="type"></a>型

<xref:System.ServiceModel.HttpTransportSecurity>

## <a name="attributes-and-elements"></a>属性および要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`clientCredentialType`|サービスに対するクライアントの認証に使用される資格情報を指定します。 この属性は <xref:System.ServiceModel.HttpClientCredentialType> 型です。|
|`proxyCredentialType`|ドメイン プロキシに対するクライアントの認証に使用される資格情報を指定します。 この属性は <xref:System.ServiceModel.HttpProxyCredentialType> 型です。|
|`realm`|ダイジェストまたは基本認証の認証レルムを指定する文字列。 既定値は空の文字列です。<br /><br /> 認証レルムでは、少なくとも、認証を実行するホストの名前を指定します。 アクセス権のあるユーザーのコレクションも指定できます。 ユーザーは、認証レルムを照会して、複数のユーザー名およびパスワードの候補のうち、どれを使用できるかを確認することができます。|
|`policyEnforcement`|この列挙体は、<xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy> を適用するタイミングを指定します。<br /><br /> 1. Never – ポリシーが適用されることはありません (拡張保護は無効になります)。<br />2. WhenSupported – ポリシーが適用されるのは、クライアントが拡張保護をサポートしている場合のみです。<br />3.Always – ポリシーは常に適用されます。 拡張保護をサポートしていないクライアントは認証に失敗します。|

## <a name="clientcredentialtype-attribute"></a>clientCredentialType 属性

|値|説明|
|-----------|-----------------|
|`None`|セキュリティを無効にします。|
|`Basic`|基本認証を使用します。|
|`Digest`|ダイジェスト認証を使用します。|
|`Ntlm`|Windows ドメインのフォールバックとして NTLM 認証を使用します。|
|`Windows`|統合 Windows 認証を使用します。|
|`Certificate`|X.509 証明書を使用して、クライアントを認証します。|

## <a name="proxycredentialtype-attribute"></a>proxyCredentialType 属性

|値|説明|
|-----------|-----------------|
|`None`|セキュリティを無効にします。|
|`Basic`|基本認証を使用します。|
|`Digest`|ダイジェスト認証を使用します。|
|`Ntlm`|Windows ドメインのフォールバックとして NTLM を使用します。|
|`Windows`|統合 Windows 認証を使用します。|
|`Certificate`|X.509 証明書を使用して、クライアントを認証します。|

### <a name="child-elements"></a>子要素

なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[\<security>](security-of-wshttpbinding.md)|[ \<WsHttpBinding >](wshttpbinding.md)のセキュリティ機能を表します。|

## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.HttpTransportSecurity>
- <xref:System.ServiceModel.WSHttpSecurity.Transport%2A>
- <xref:System.ServiceModel.Configuration.WSHttpSecurityElement.Transport%2A>
- <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement>
- [サービスおよびクライアントのセキュリティ保護](../../../wcf/feature-details/securing-services-and-clients.md)
- [バインディング](../../../wcf/bindings.md)
- [システムが提供するバインディングの構成](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [サービスとクライアントを構成するためのバインディングの使用](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
