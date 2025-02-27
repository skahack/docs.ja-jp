---
title: <requestCaching> 要素 (ネットワーク設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#requestCaching
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/requestCaching
helpviewer_keywords:
- requestCaching element
- <requestCaching> element
ms.assetid: 9962a2fe-cbda-41a6-9377-571811eaea84
ms.openlocfilehash: 2a3d0b182acad2351ed095934ca97c6194d344fc
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69659131"
---
# <a name="requestcaching-element-network-settings"></a>\<requestCaching> 要素 (ネットワーク設定)
ネットワーク要求のキャッシュメカニズムを制御します。  
  
 \<configuration>  
\<system.net>  
\<requestCaching>  
  
## <a name="syntax"></a>構文  
  
```xml  
<requestCaching  
  isPrivateCache ="true|false"  
  disableAllCaching="true|false"  
  defaultPolicyLevel="BypassCache|Default|CacheOnly|CacheIfAvailable|Revalidate|Reload|NoCacheNoStore|Revalidate"  
  unspecifiedMaximumAge= "d.hh.mm.ss">  
    <defaultHttpCachePolicy>...</defaultHttpCachePolicy>  
    <defaultFtpCachePolicy>...</defaultFtpCachePolicy>  
</requestCaching>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`isPrivateCache`|キャッシュがさまざまなユーザーの情報の分離を提供するかどうかを指定します。 既定値は `true` です。 中間層アプリケーションの`false`場合は、この値をにする必要があります。|  
|`disableAllCaching`|すべての Web 応答に対してキャッシュを無効にし、プログラムでオーバーライドすることはできないことを指定します。|  
|`defaultPolicyLevel`|<xref:System.Net.Cache.RequestCacheLevel> 列挙値の値の 1 つ。 既定値は `BypassCache` です。|  
|`unspecifiedMaximumAge`|コンテンツが期限切れとしてマークされるまでの既定の時間を指定します。|  
  
## <a name="policylevel-attribute"></a>policyLevel 属性  
  
|値|説明|  
|-----------|-----------------|  
|`Default`|リソースが最新で、コンテンツの長さが正確で、有効期限、変更、およびコンテンツの長さの属性が存在する場合、キャッシュされたリソースを返します。|  
|`BypassCache`|サーバーからリソースを返します。|  
|`CacheOnly`|コンテンツの長さが存在し、エントリのサイズと一致する場合、キャッシュされたリソースを返します。|  
|`CacheIfAvailable`|コンテンツの長さが指定され、エントリのサイズと一致する場合に、キャッシュされたリソースを返します。それ以外の場合は、リソースがサーバーからダウンロードされ、呼び出し元に返されます。|  
|`Revalidate`|キャッシュされたリソースのタイムスタンプがサーバー上のリソースのタイムスタンプと同じ場合は、キャッシュされたリソースを返します。それ以外の場合は、リソースがサーバーからダウンロードされ、キャッシュに格納されて、呼び出し元に返されます。|  
|`Reload`|サーバーからリソースをダウンロードし、キャッシュに格納して、リソースを呼び出し元に返します。|  
|`NoCacheNoStore`|キャッシュされたリソースが存在する場合は、削除されます。 リソースはサーバーからダウンロードされ、呼び出し元に返されます。|  
|`Revalidate`|タイムスタンプがサーバー上のリソースのタイムスタンプと同じ場合は、リソースのキャッシュされたコピーを使用して要求を満たします。それ以外の場合、リソースはサーバーからダウンロードされ、呼び出し元に渡され、キャッシュに格納されます。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[defaultHttpCachePolicy](defaulthttpcachepolicy-element-network-settings.md)|省略可能な要素です。<br /><br /> HTTP キャッシュがアクティブかどうか、および既定のキャッシュポリシーについて説明します。|  
|[\<defaultFtpCachePolicy> 要素 (ネットワーク設定](defaultftpcachepolicy-element-network-settings.md)|省略可能な要素です。<br /><br /> FTP キャッシュがアクティブでかどうかし、既定のキャッシュ ポリシーを記述について説明します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[system.net](system-net-element-network-settings.md)|.NET Framework がネットワークに接続する方法を指定するための設定が含まれています。|  
  
## <a name="example"></a>例  
 次の例では、すべてのキャッシュを無効にする方法を示します。  
  
```xml  
<configuration>  
  <system.net>  
    <requestCaching  
      disableAllCaching="true"  
    />  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.Cache?displayProperty=nameWithType>
- [ネットワーク設定スキーマ](index.md)
