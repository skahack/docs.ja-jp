---
title: <security> の <netPeerBinding>
ms.date: 03/30/2017
ms.assetid: 1ef40d8c-f903-4426-9b08-da81462766d8
ms.openlocfilehash: be5ebacec466caf8d8a77bf552f42da1861e77a1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69936625"
---
# <a name="security-of-netpeerbinding"></a>\<netpeerbinding \<> のセキュリティ >
[ \<Netpeertcpbinding >](netpeertcpbinding.md)のセキュリティ設定を定義します。これには、使用する認証の種類や、メッセージトランスポートに使用するセキュリティなどが含まれます。  
  
 \<system.ServiceModel >  
\<bindings>  
\<netPeerBinding>  
\<binding>  
\<セキュリティ >  
  
## <a name="syntax"></a>構文  
  
```xml  
<netPeerBinding>
  <binding>
    <security mode="Message/None/Transport//TransportWithMessageCredential">
      <transport credentialType="Certificate/Password" />
    </security>
  </binding>
</netPeerBinding>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|モード|任意。 このバインディングで構成されたピアが使用するセキュリティの種類を指定します。 既定値は `Message` です。 この属性は <xref:System.ServiceModel.SecurityMode> 型です。|  
  
## <a name="mode-attribute"></a>mode 属性  
  
|値|説明|  
|-----------|-----------------|  
|Message|SOAP セキュリティにより、認証、整合性、および機密性が実現します。|  
|なし|セキュリティを無効にします。|  
|Transport|セキュリティは、HTTPS を使用して確保されます。|  
|TransportWithMessageCredential|HTTPS により、認証および機密性が実現します。 SOAP メッセージには、豊富な資格情報の種類が用意されています。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<transport>](transport-of-netpeertcpbinding.md)|このバインディングで構成されたピアが送信するセキュリティで保護されたメッセージのトランスポートの型を定義します。 この要素は <xref:System.ServiceModel.Configuration.PeerTransportSecurityElement> 型です。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<binding>](../../../misc/binding.md)|Netpeertcpbinding > のすべてのバインド機能を[ \<](netpeertcpbinding.md)定義します。|  
  
## <a name="remarks"></a>Remarks  
 セキュリティは、メッセージ固有にすることも、トランスポート固有にすることもできます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.PeerSecurityElement>
- <xref:System.ServiceModel.NetPeerTcpBinding.Security%2A>
- <xref:System.ServiceModel.Configuration.NetPeerTcpBindingElement.Security%2A>
- <xref:System.ServiceModel.PeerSecuritySettings>
- [サービスおよびクライアントのセキュリティ保護](../../../wcf/feature-details/securing-services-and-clients.md)
- [資格情報の種類の選択](../../../wcf/feature-details/selecting-a-credential-type.md)
- [バインディング](../../../wcf/bindings.md)
- [システムが提供するバインディングの構成](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [サービスとクライアントを構成するためのバインディングの使用](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
