---
title: <CompatSortNLSVersion> 要素
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- <CompatSortNLSVersion> element
- CompatSortNLSVersion element
ms.assetid: 782cc82e-83f7-404a-80b7-6d3061a8b6e3
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e3a348ac8da855e458b6208c51f9c51b48da3134
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927444"
---
# <a name="compatsortnlsversion-element"></a>\<CompatSortNLSVersion > 要素
文字列比較の実行時に、ランタイムがレガシ並べ替え順序を使用するように指定します。  
  
 \<configuration>  
\<ランタイム >  
\<CompatSortNLSVersion > 要素  
  
## <a name="syntax"></a>構文  
  
```xml  
<CompatSortNLSVersion    
   enabled="4096"/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`enabled`|必須の属性です。<br /><br /> 並べ替え順序が使用されるロケール ID を指定します。|  
  
## <a name="enabled-attribute"></a>enabled 属性  
  
|値|説明|  
|-----------|-----------------|  
|4096|代替の並べ替え順序を表すロケール ID。 この場合、4096は .NET Framework 3.5 以前のバージョンの並べ替え順序を表します。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`runtime`|ランタイム初期化オプションに関する情報を含んでいます。|  
  
## <a name="remarks"></a>Remarks  
 .NET Framework 4 の<xref:System.Globalization.CompareInfo?displayProperty=nameWithType>クラスによって実行される文字列比較、並べ替え、および大文字と小文字の区別の操作は Unicode 5.1 標準に準拠して<xref:System.String.LastIndexOf%28System.String%29?displayProperty=nameWithType>いるため、やなど<xref:System.String.Compare%28System.String%2CSystem.String%29?displayProperty=nameWithType>の文字列比較メソッドの結果は、以前のバージョンの .NET Framework。 アプリケーションが従来の動作に依存している場合は、アプリケーションの構成ファイルに要素を`<CompatSortNLSVersion>`含めることによって、.NET Framework 3.5 以前のバージョンで使用されている文字列比較規則および並べ替え規則を復元できます。  
  
> [!IMPORTANT]
> 文字列の比較および並べ替えのレガシ規則を復元する場合は、ローカル システムで sort00001000.dll ダイナミック リンク ライブラリも使用できるようにする必要があります。  
  
 アプリケーション ドメインを作成するときに、文字列 "NetFx40_Legacy20SortingBehavior" を <xref:System.AppDomainSetup.SetCompatibilitySwitches%2A> メソッドに渡すことで、文字列の比較および並べ替えのレガシ規則を特定のアプリケーション ドメインで使用することもできます。  
  
## <a name="example"></a>例  
 次の例では、2 つの <xref:System.String> オブジェクトをインスタンス化して、<xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> メソッドを呼び出し、現在のカルチャの規則を使用してそれらのオブジェクトを比較する方法を示します。  
  
 [!code-csharp[String.BreakingChanges#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/string.breakingchanges/cs/example1.cs#1)]
 [!code-vb[String.BreakingChanges#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/string.breakingchanges/vb/example1.vb#1)]  
  
 .NET Framework 4 でこの例を実行すると、次の出力が表示されます。  
  
```  
sta follows a in the sort order.  
```  
  
 これは、.NET Framework 3.5 で例を実行したときに表示される出力とはまったく異なります。  
  
```  
sta equals a in the sort order.  
```  
  
 ただし、次の構成ファイルを例のディレクトリに追加し、.NET Framework 4 でこの例を実行すると、出力は、.NET Framework 3.5 で実行された場合に例で生成されたものと同じになります。  
  
```xml  
<?xml version ="1.0"?>  
<configuration>  
   <runtime>  
      <CompatSortNLSVersion enabled="4096"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [ランタイム設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
