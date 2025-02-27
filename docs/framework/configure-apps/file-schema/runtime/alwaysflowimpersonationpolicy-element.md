---
title: <alwaysFlowImpersonationPolicy> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/alwaysFlowImpersonationPolicy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#alwaysFlowImpersonationPolicy
helpviewer_keywords:
- alwaysFlowImpersonationPolicy element
- <alwaysFlowImpersonationPolicy> element
ms.assetid: ee622801-9e46-470b-85ab-88c4b1dd2ee1
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b42c141362d99090db922d3a6b429f05592130cd
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69659015"
---
# <a name="alwaysflowimpersonationpolicy-element"></a>\<alwaysFlowImpersonationPolicy > 要素
偽装の実行方法に関係なく、Windows ID が常に非同期ポイント間でフローすることを指定します。  
  
 \<configuration>  
\<ランタイム >  
\<alwaysFlowImpersonationPolicy>  
  
## <a name="syntax"></a>構文  
  
```xml  
<alwaysFlowImpersonationPolicy    
  enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`enabled`|必須の属性です。<br /><br /> Windows id が非同期ポイント間でフローするかどうかを示します。|  
  
## <a name="enabled-attribute"></a>enabled 属性  
  
|値|説明|  
|-----------|-----------------|  
|`false`|など<xref:System.Security.Principal.WindowsIdentity.Impersonate%2A>のマネージメソッドを使用して偽装を実行しない限り、Windows id は非同期ポイント間ではフローしません。 既定値です。|  
|`true`|Windows id は、偽装がどのように実行されたかに関係なく、常に非同期のポイント間でフローします。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`runtime`|アセンブリのバインディングとガベージ コレクションに関する情報が含まれています。|  
  
## <a name="remarks"></a>Remarks  
 .NET Framework バージョン1.0 および1.1 では、Windows id は非同期ポイント間ではフローしません。 .NET Framework バージョン2.0 では、現在実行中<xref:System.Threading.ExecutionContext>のスレッドに関する情報を格納するオブジェクトがあり、アプリケーションドメイン内の非同期ポイント間でフローします。 また<xref:System.Security.Principal.WindowsIdentity> 、は、非同期ポイント全体をフローする情報の一部としてもフローします。これは、など<xref:System.Security.Principal.WindowsIdentity.Impersonate%2A>のマネージメソッドを使用して偽装が行われた場合に、ネイティブメソッドへのプラットフォーム呼び出しなどの他の方法を使用して行われなかった場合に限ります。 この要素は、偽装がどのように実現されたかに関係なく、Windows id が非同期ポイント間でフローすることを指定するために使用されます。  
  
 この既定の動作は、次の2つの方法で変更できます。  
  
1. マネージコード内で、スレッド単位で。  
  
     <xref:System.Threading.ExecutionContext.SuppressFlow%2A?displayProperty=nameWithType>、 <xref:System.Threading.ExecutionContext> <xref:System.Security.SecurityContext> 、また<xref:System.Security.SecurityContext.SuppressFlow%2A?displayProperty=nameWithType>はメソッドを使用しておよび設定を変更することで、スレッド単位でフローを抑制できます。 <xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity%2A?displayProperty=nameWithType>  
  
2. アンマネージホストインターフェイスを呼び出して、共通言語ランタイム (CLR) を読み込みます。  
  
     アンマネージホストインターフェイス (単純なマネージ実行可能ファイルではなく) を使用して CLR を読み込む場合は、 [Corbindtoruntimeex 関数](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)関数の呼び出しで特別なフラグを指定できます。 プロセス全体で互換モードを有効にするには、 `flags` [corbindtoruntimeex 関数](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)のパラメーターを`STARTUP_ALWAYSFLOW_IMPERSONATION`に設定します。  
  
## <a name="configuration-file"></a>構成ファイル  
 .NET Framework アプリケーションでは、この要素はアプリケーション構成ファイルでのみ使用できます。  
  
 ASP.NET アプリケーションの場合、偽装フローは、 \<Windows フォルダー > \Microsoft.NET\Framework\vx.x.xxxx ディレクトリにある aspnet ファイルで構成できます。  
  
 ASP.NET は、既定では、次の構成設定を使用して、aspnet ファイル内の偽装フローを無効にします。  
  
```xml
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="true"/>  
      <alwaysFlowImpersonationPolicy enabled="false"/>  
   </runtime>  
</configuration>  
```  
  
 ASP.NET で、代わりに偽装のフローを許可する場合は、次の構成設定を明示的に使用する必要があります。  
  
```xml  
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="false"/>  
      <alwaysFlowImpersonationPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="example"></a>例  
 次の例では、マネージメソッド以外の方法で権限借用が行われた場合でも、Windows id を非同期ポイント間でフローするように指定する方法を示します。  
  
```xml  
<configuration>  
  <runtime>  
    <alwaysFlowImpersonationPolicy enabled="true"/>  
  </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [ランタイム設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
- [\<legacyImpersonationPolicy > 要素](legacyimpersonationpolicy-element.md)
