---
title: <clientCredentials>
ms.date: 03/30/2017
ms.assetid: 1e6eef0d-a34e-4d74-b0f7-f65d2181858d
ms.openlocfilehash: c3e756f49b7054d6553eb6c3f1850f0fbce14943
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69926103"
---
# <a name="clientcredentials"></a>\<clientCredentials>
サービスに対するクライアントの認証に使用される資格情報を指定します。  
  
 \<system.ServiceModel >  
\<<behaviors>  
\<endpointBehaviors>  
\<behavior>  
\<clientCredentials>  
  
## <a name="syntax"></a>構文  
  
```xml  
<clientCredentials type="String"
                   supportInteractive="Boolean" >
  <clientCertificate>
  </clientCertificate>
  <digest>
  </digest>
  <isuedToken>
  </isuedToken>
  <peer>
  </peer>
  <serviceCertificate>
  </serviceCertificate>
  <windowsAuthentication>
  </windowsAuthentication>
</clientCredentials>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`supportInteractive`|実行時にクライアントの資格情報を選択する際に、対話型ユーザーを含めるかどうかを指定するブール値。 既定値は `true` です。|  
|`type`|この設定要素の種類を指定する文字列です。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<clientCertificate>](clientcertificate-of-clientcredentials-element.md)|サービスに対するクライアントの認証に使用される証明書を指定します。 この要素は <xref:System.ServiceModel.Configuration.X509InitiatorCertificateClientElement> 型です。|  
|[\<httpDigest >](httpdigest-element.md)|サービスに対するクライアントの認証に使用されるダイジェストを指定します。 この要素は <xref:System.ServiceModel.Configuration.HttpDigestClientElement> 型です。|  
|[\<issuedToken >](issuedtoken.md)|セキュリティ トークン サービス (STS) に対するクライアントの認証に使用されるカスタム トークンの種類を指定します。 この要素は <xref:System.ServiceModel.Configuration.IssuedTokenClientElement> 型です。|  
|[\<peer>](peer-of-clientcredentials-element.md)|現在のピア資格情報を指定します。 この要素は <xref:System.ServiceModel.Configuration.PeerCredentialElement> 型です。|  
|[\<serviceCertificate >](servicecertificate-of-clientcredentials-element.md)|クライアントに対するサービスの認証に使用される証明書を指定し、証明書オプションを設定するための構造を提供します。 この証明書は、クライアントに対するサービスの帯域外に提供される必要があります。 この要素は <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement> 型です。|  
|[\<windows>](windows-of-clientcredentials-element.md)|Windows 資格情報を指定します。 既定値は、現在のスレッドの資格情報です。 この要素は <xref:System.ServiceModel.Configuration.WindowsClientElement> 型です。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|エンドポイントの動作を指定します。|  
  
## <a name="remarks"></a>Remarks  
 クライアント資格情報は、相互認証が必要な場合にサービスに対するクライアントの認証に使用されます。 また、この構成セクションを使用して、クライアントがサービスの証明書によってサービスへのメッセージをセキュリティで保護する必要がある場合に使用するサービス証明書を指定することもできます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Description.ClientCredentials>
- [セキュリティ動作](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [クライアントのセキュリティ保護](../../../wcf/securing-clients.md)
