---
title: <idn> 要素 (Uri 設定)
ms.date: 03/30/2017
ms.assetid: 16c8e869-1791-4cf5-9244-3d3c738f60ec
ms.openlocfilehash: 5fe2eafee702be96bfdca80a06af4a040d9ef0f6
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69664118"
---
# <a name="idn-element-uri-settings"></a>\<idn> 要素 (Uri 設定)
国際化ドメイン名 (IDN) の解析がドメイン名に適用されるかどうかを指定します。  
  
## <a name="schema-hierarchy"></a>スキーマの階層  
 [\<configuration> 要素](../configuration-element.md)  
  
 [\<Uri> 要素 (Uri 設定)](uri-element-uri-settings.md)  
  
 [\<idn>](idn-element-uri-settings.md)  
  
## <a name="syntax"></a>構文  
  
```xml  
<idn  
  enabled="All|AllExceptIntranet|None"  
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|`enabled`|国際化ドメイン名 (IDN) の解析がドメイン名に適用されるかどうかを指定します。既定値は none です。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[uri](uri-element-uri-settings.md)|.NET Framework が、uniform resource identifier (Uri) を使用して表された web アドレスを処理する方法を指定する設定が含まれます。|  
  
## <a name="remarks"></a>Remarks  
 既存<xref:System.Uri>のクラスは .NET Framework 3.5 で拡張されています。 3.0 SP1 および 2.0 SP1 (国際リソース識別子 (IRI) と国際化ドメイン名 (IDN) をサポート)。 現在のユーザーには、IRI と IDN のサポートを明示的に有効にしない限り、.NET Framework 2.0 の動作からの変更は表示されません。 これにより、.NET Framework の以前のバージョンとのアプリケーションの互換性を保証します。  
  
 IRI のサポートを有効にするには、次の2つの変更が必要です。  
  
1. Machine.config ファイルの .NET Framework 2.0 ディレクトリの下に次の行を追加します。  
  
    ```xml  
    <section name="uri" type="System.Configuration.UriSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
    ```  
  
2. 国際化ドメイン名 (IDN) の解析をドメイン名に適用するかどうか、および IRI 解析規則を適用するかどうかを指定します。 これは、machine.config ファイルまたは app.config ファイルで指定できます。  
  
 IDN には、使用する DNS サーバーに応じて、次の3つの値を指定できます。  
  
- idn enabled = すべて  
  
     この値により、すべての Unicode ドメイン名が Punycode に相当する (IDN 名) に変換されます。  
  
- idn enabled = AllExceptIntranet  
  
     この値を指定すると、ローカルイントラネット上にないすべての Unicode ドメイン名が、Punycode に相当する (IDN 名) を使用するように変換されます。 この場合は、イントラネットで使用される DNS サーバーが Unicode 名前解決をサポートする必要があります。  
  
- idn enabled = なし  
  
     この値では、Unicode ドメイン名を変換して Punycode を使用することはできません。 これは、.NET Framework 2.0 の動作と一貫性のある既定値です。  
  
 IDN を有効にすると、ドメイン名に含まれるすべての Unicode のラベルが Punycode のラベルに変換されます。 Punycode 名には ASCII 文字のみが含まれ、常に xn-- プレフィックスで始まります。 この理由は、ほとんどの DNS サーバーは ASCII 文字しかサポートしていないため、インターネットで既存の DNS サーバーをサポートするためです (RFC 3940 を参照)。  
  
### <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例は、IRI 解析と IDN <xref:System.Uri>名をサポートするためにクラスによって使用される構成を示しています。  
  
### <a name="code"></a>コード  
  
```xml  
<configuration>  
  <uri>  
    <idn enabled="All" />  
    <iriParsing enabled="true" />  
  </uri>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Configuration.IdnElement?displayProperty=nameWithType>
- <xref:System.Configuration.UriSection?displayProperty=nameWithType>
- [ネットワーク設定スキーマ](index.md)
