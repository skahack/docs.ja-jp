---
title: <userNameAuthentication>
ms.date: 03/30/2017
ms.assetid: 24d8b398-770f-418f-ba23-c4325419cfa6
ms.openlocfilehash: 399158632d5c17a35ded02691ba35a231e6cdc6e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69940544"
---
# <a name="usernameauthentication"></a>\<userNameAuthentication>
ユーザー名とパスワードに基づいてサービスの資格情報を指定します。  
  
 \<system.ServiceModel >  
\<<behaviors>  
\<serviceBehaviors>  
\<behavior>  
\<serviceCredentials>  
\<userNameAuthentication>  
  
## <a name="syntax"></a>構文  
  
```xml  
<userNameAuthentication cacheLogonTokenLifetime="TimeSpan"
                        cacheLogonTokens="Boolean"
                        customUserNamePasswordValidatorType="String"
                        includeWindowsGroups="Boolean"
                        maxCacheLogonTokens="Integer"
                        membershipProviderName="String"
                        userNamePasswordValidationMode="Windows/MembershipProvider/Custom" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`cacheLogonTokenLifetime`|トークンがキャッシュ内に保持される最大時間を指定する <xref:System.TimeSpan>。 既定値は 00:15:00 です。|  
|`cacheLogonTokens`|ログオン トークンがキャッシュされるかどうかを指定するブール値。 既定値は `false` です。|  
|`customUserNamePasswordValidatorType`|使用されるカスタム ユーザー名およびパスワード検証の種類を指定する文字列。 既定値は空の文字列です。|  
|`includeWindowsGroups`|セキュリティ コンテキストに Windows グループが含まれるかどうかを指定するブール値。 既定値は `true` です。<br /><br /> この属性を `true` に設定すると、グループ全体が拡張されるため、パフォーマンスに影響が及びます。 ユーザーが属するグループの一覧を生成する必要がない場合は、このプロパティを `false` に設定します。|  
|`maxCacheLogonTokens`|キャッシュするログオン トークンの最大数を指定する整数。 この値は、ゼロより大きい値である必要があります。 既定値は 128 です。|  
|`membershipProviderName`|バインディングの `clientCredentialType` 属性が `username` に設定されている場合、ユーザー名は Windows アカウントにマップされます。 関連するパスワード検証機構を提供する <xref:System.Web.Security.MembershipProvider> 値の名前を含む文字列であるこの属性を使用して動作をオーバーライドできます。|  
|`userNamePasswordValidationMode`|ユーザー名とパスワードを検証する方法を指定します。 有効な値は、<br /><br /> -Windows<br />-MembershipProvider<br />-カスタム<br /><br /> 既定は Windows です。 この属性は <xref:System.ServiceModel.Security.UserNamePasswordValidationMode> 型です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<serviceCredentials>](servicecredentials.md)|サービスの認証に使用される資格情報と、クライアントの資格情報検証関連の設定を指定します。|  
  
## <a name="remarks"></a>Remarks  
 サービスで使用されるバインディングがユーザー名とパスワード ベースの認証を使用するように構成されていない場合、この要素の属性は無視されます。 これには、`customUserNamePasswordValidatorType`、`includeWindowsGroups`、`membershipProviderName`、および `userNamePasswordValidationMode` が含まれます。  
  
 サービスで使用されるバインディングが Windows 認証のユーザー名とパスワードを使用するように構成されていない場合、ログオン トークンのキャッシュに関連する設定は無視されます。 これには、`cacheLogonTokenLifetime`、`cacheLogonTokens`、および `maxCacheLogonTokens`、が含まれます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.UserNameServiceElement>
- <xref:System.ServiceModel.Description.ServiceCredentials.UserNameAuthentication%2A>
- <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential>
- <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.UserNameAuthentication%2A>
