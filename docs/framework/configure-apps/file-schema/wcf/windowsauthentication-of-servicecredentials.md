---
title: <windowsAuthentication> の <serviceCredentials>
ms.date: 03/30/2017
ms.assetid: e0709473-0997-4de3-8f49-783527309a48
ms.openlocfilehash: 81793b0d58a95166bc23f98d46ce94a5f1e1d018
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69940290"
---
# <a name="windowsauthentication-of-servicecredentials"></a>\<serviceCredentials > の\<windowsauthentication >
Windows サービス資格情報の設定を指定します。  
  
 \<system.ServiceModel >  
\<<behaviors>  
\<serviceBehaviors>  
\<behavior>  
\<serviceCredentials>  
\<windowsAuthentication >  
  
## <a name="syntax"></a>構文  
  
```xml  
<windowsAuthentication allowAnonymousLogons="Boolean"
                       includeWindowsGroups="Boolean" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`includeWindowsGroups`|セキュリティ コンテキストに Windows グループが含まれるかどうかを指定する省略可能なブール属性。 既定値は `true` です。<br /><br /> この属性を `true` に設定すると、グループ全体が拡張されるため、パフォーマンスに影響が及びます。 ユーザーが属するグループの一覧を生成する必要がない場合は、この属性を `false` に設定します。|  
|`allowAnonymousLogons`|認証されていない匿名の呼び出し元を許可するかどうかを指定する省略可能なブール属性。 既定値は `false` です。<br /><br /> バインディングの `clientCredentialType` 属性が `Windows` に設定されている場合、匿名の呼び出し元は許可されません。 これは、ドメインまたはワークグループの認証済み呼び出し元だけがシステムへのアクセスを許可されていることを示します。 この動作は、この属性を使用してオーバーライドできます。<br /><br /> この設定を使用するときは十分に注意してください。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<serviceCredentials>](servicecredentials.md)|サービスの認証に使用される資格情報と、クライアントの資格情報検証関連の設定を指定します。|  
  
## <a name="remarks"></a>Remarks  
 匿名の Windows ユーザーのアクセスを許可するかどうかを指定するには、この要素を使用して、`allowAnonymousLogons` 属性を設定します。 また、`includeWindowsGroups` 属性を設定すると、ユーザーが属するグループの情報を AuthorizationContext に含めるかどうかも指定できます。 この属性が `true` (既定値) に設定されている場合、サービスはクライアントが属している Windows グループを特定できます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.WindowsServiceElement>
- <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.WindowsAuthentication%2A>
- <xref:System.ServiceModel.Description.ServiceCredentials.WindowsAuthentication%2A>
- <xref:System.ServiceModel.Security.WindowsServiceCredential>
