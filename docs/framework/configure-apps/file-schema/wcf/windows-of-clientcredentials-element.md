---
title: <windows> <clientCredentials>要素
ms.date: 03/30/2017
ms.assetid: 793e41c2-31ea-4159-abbc-2123bf097233
ms.openlocfilehash: e9f0ed9879cc42ea25b83e6b626139a40a593112
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69940309"
---
# <a name="windows-of-clientcredentials-element"></a>\<clientCredentials > 要素\<の windows >
クライアントを表すために使用される Windows 資格情報の設定を指定します。  
  
 \<system.ServiceModel >  
\<<behaviors>  
\<endpointBehaviors>  
\<behavior>  
\<clientCredentials>  
\<windows >  
  
## <a name="syntax"></a>構文  
  
```xml  
<windows allowedImpersonationLevel="Identification/Impersonation/Delegation/Anonymous/None"
         allowNtlm="Boolean" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`allowedImpersonationLevel`|クライアントがサーバーと通信する偽装設定を設定します。 クライアントが選択する偽装モードは、サーバーでは適用されません。 以下の値が有効です。<br /><br /> 番号サーバーはクライアントの id と特権を取得できますが、クライアントの権限を借用することはできません。<br />偽造サーバーは、ローカルシステム上のクライアントのセキュリティコンテキストを偽装できます。<br />-委任:サーバーは、リモートシステム上のクライアントのセキュリティコンテキストを偽装できます。<br />非同期サーバーは、クライアントの権限を借用または識別できません。<br />存在偽装レベルが割り当てられていません。<br /><br /> 既定値は Identification です。 この属性は <xref:System.Security.Principal.TokenImpersonationLevel> 型です。|  
|`allowNtlm`|このプロパティを `true` に設定すると、Kerberos 認証を利用できない場合、NTLM 認証にダウングレードできます。<br /><br /> このプロパティをに`false`設定すると、NTLM が使用されている場合に Windows Communication Foundation (WCF) がベストエフォートで例外をスローするようになります。 ただし、このプロパティを `false` に設定しても、ネットワーク経由で NTLM 資格情報が送信されなくなるとは限りません。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<clientCredentials>](clientcredentials.md)|サービスに対するクライアントの認証に使用される資格情報を指定します。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.WindowsClientElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.Windows%2A>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ClientCredentials.Windows%2A>
- <xref:System.ServiceModel.Security.WindowsClientCredential>
- [クライアントのセキュリティ保護](../../../wcf/securing-clients.md)
- [証明書の使用](../../../wcf/feature-details/working-with-certificates.md)
- [サービスおよびクライアントのセキュリティ保護](../../../wcf/feature-details/securing-services-and-clients.md)
