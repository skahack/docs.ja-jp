---
title: <proxy> 要素 (ネットワーク設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/proxy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#proxy
helpviewer_keywords:
- <proxy> element
- proxy element
ms.assetid: 37a548d8-fade-4ac5-82ec-b49b6c6cb22a
ms.openlocfilehash: a183c4160c4cd55b05c5c23f7a10e3a1d1c74ea4
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69659287"
---
# <a name="proxy-element-network-settings"></a>\<proxy> 要素 (ネットワーク設定)
プロキシ サーバーを定義します。  
  
 \<configuration>  
\<system.net>  
\<defaultProxy>  
\<proxy>  
  
## <a name="syntax"></a>構文  
  
```xml  
<proxy
  autoDetect="true|false|unspecified" 
  bypassonlocal="true|false|unspecified"
  proxyaddress="uriString"
  scriptLocation="uriString"
  usesystemdefault="true|false|unspecified"
/>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|**属性**|**説明**|  
|-------------------|---------------------|  
|`autoDetect`|プロキシが自動的に検出されるかどうかを指定します。 既定値は `unspecified` です。|  
|`bypassonlocal`|ローカルリソースに対してプロキシをバイパスするかどうかを指定します。 ローカルリソースには、ローカルサーバー`http://localhost`( `http://loopback`、、 `http://127.0.0.1`または) と、ピリオドなしの`http://webserver`URI () が含まれます。 既定値は `unspecified` です。|  
|`proxyaddress`|使用するプロキシ URI を指定します。|  
|`scriptLocation`|構成スクリプトの場所を指定します。 この属性には`bypassonlocal`属性を使用しないでください。 |  
|`usesystemdefault`|Internet Explorer のプロキシ設定を使用するかどうかを指定します。 に設定する`true`と、それ以降の属性は Internet Explorer のプロキシ設定よりも優先されます。 既定値は `unspecified` です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[defaultProxy](defaultproxy-element-network-settings.md)|ハイパーテキスト転送プロトコル (HTTP: Hypertext Transfer Protocol) プロキシ サーバーを構成します。|  
  
## <a name="text-value"></a>テキスト値  
  
## <a name="remarks"></a>Remarks  
 要素`proxy`は、アプリケーションのプロキシサーバーを定義します。 この要素が構成ファイルにない場合、.NET Framework は Internet Explorer のプロキシ設定を使用します。  
  
 `proxyaddress`属性の値は、整形式の Uniform resource Indicator (URI) である必要があります。  
  
 属性`scriptLocation`は、プロキシ構成スクリプトの自動検出を参照します。 Internet Explorer で **[自動構成スクリプトを使用する]** オプションが選択されている場合、クラスは、(通常はwpad.datという名前の)構成スクリプトの検索を試みます。<xref:System.Net.WebProxy> が`bypassonlocal`任意の値に設定さ`scriptLocation`れている場合、は無視されます。
  
 バージョン 2.0 `usesystemdefault`に移行する .NET Framework バージョン1.1 アプリケーションの場合は、属性を使用します。  
  
 属性が無効な既定の`proxyaddress`プロキシを指定している場合は、例外がスローされます。 例外の <xref:System.Exception.InnerException%2A> プロパティに、このエラーの根本原因に関する詳細情報が含まれています。  
  
## <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="example"></a>例  
 次の例では、Internet Explorer プロキシの既定値を使用して、プロキシアドレスを指定し、ローカルアクセスのためにプロキシをバイパスします。  
  
```xml  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <proxy  
        usesystemdefault="true"  
        proxyaddress="http://192.168.1.10:3128"  
        bypassonlocal="true"  
      />  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.WebProxy?displayProperty=nameWithType>
- [ネットワーク設定スキーマ](index.md)
