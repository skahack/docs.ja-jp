---
title: <shadowCopyVerifyByTimestamp> 要素
ms.date: 03/30/2017
helpviewer_keywords:
- <shadowCopyTimeStampVerification> element
- shadowCopyTimeStampVerification element
ms.assetid: 2f1648e5-997b-435e-a4f9-d236c574c66c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6f3ea57364832553d16c7e34fc887b1c9f821602
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69663449"
---
# <a name="shadowcopyverifybytimestamp-element"></a>\<shadowCopyVerifyByTimestamp> 要素
シャドウコピーで .NET Framework 4 で導入された既定の起動動作を使用するか、以前のバージョンの .NET Framework の起動動作に戻すかを指定します。  
  
 \<configuration> 要素  
\<runtime> 要素  
\<shadowCopyVerifyByTimestamp> 要素  
  
## <a name="syntax"></a>構文  
  
```xml  
<shadowCopyVerifyByTimestamp enabled="true|false" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|enabled|必須の属性です。<br /><br /> シャドウコピーを使用するアプリケーションドメインが起動時にアセンブリのタイムスタンプを比較するかどうかを指定し、アセンブリをシャドウコピーする前に更新したかどうかを確認します。|  
  
## <a name="enabled-attribute"></a>enabled 属性  
  
|値|説明|  
|-----------|-----------------|  
|true|起動時に、はシャドウコピーディレクトリに最後にコピーされてから更新されたアセンブリのみをコピーします。 これは .NET Framework 4 の既定値です。|  
|False|以前のバージョンの .NET Framework の起動動作に戻ります。これは、起動時にすべてのファイルをコピーすることでした。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`runtime`|アセンブリのバインディングとガベージ コレクションに関する情報が含まれています。|  
  
## <a name="remarks"></a>Remarks  
 .NET Framework 4 以降、アセンブリはシャドウコピーディレクトリに最後にコピーされてから変更されたことを示すタイムスタンプがある場合にのみ、シャドウコピーされます。 これにより、「[アセンブリのシャドウコピー](../../../app-domains/shadow-copy-assemblies.md)」で説明されているように、シャドウコピーを使用する多くのアプリケーションの起動時間が短縮されます。 アセンブリ更新の割合と頻度が高いアプリケーションでは、この動作の変更によるメリットが得られない場合があります。 その場合は、この要素を使用して、.NET Framework の以前のバージョンの動作を復元できます。  
  
## <a name="example"></a>例  
 次の例は、.NET Framework 4 でシャドウコピーの既定の起動動作を無効にして、以前のバージョンの .NET Framework の起動動作に戻す方法を示しています。  
  
```xml  
<configuration>  
   <runtime>  
      <shadowCopyVerifyByTimestamp enabled="false" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [ランタイム設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
- [アセンブリのシャドウ コピー](../../../app-domains/shadow-copy-assemblies.md)
