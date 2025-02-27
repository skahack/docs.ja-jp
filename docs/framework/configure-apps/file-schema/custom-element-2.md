---
title: NameValueSectionHandler および DictionarySectionHandler の Custom 要素
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/sectionName
helpviewer_keywords:
- custom element
ms.assetid: 2303031f-4c1d-4df4-bca1-e9bd96ca40dc
author: rpetrusha
ms.author: mairaw
ms.openlocfilehash: 890269857aaa00ce62195ccb2f4cb184b363b61e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69921035"
---
# <a name="custom-element-for-namevaluesectionhandler-and-dictionarysectionhandler"></a>NameValueSectionHandler および DictionarySectionHandler の Custom 要素

クラス<xref:System.Configuration.NameValueSectionHandler> および<xref:System.Configuration.DictionarySectionHandler>クラスを使用するカスタム構成セクションの設定を定義します。

[ **\<configuration>** ](configuration-element.md)\
&nbsp;&nbsp; **\<sectionName>**

## <a name="attributes"></a>属性

なし

## <a name="parent-element"></a>親要素

|     | 説明 |
| --- | ----------- |
| [ **\<configuration>** ](configuration-element.md) | 共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。 |

## <a name="child-elements"></a>子要素

|     | 説明 |
| --- | ----------- |
| およびの<xref:System.Configuration.NameValueSectionHandler> > を[ **\<追加**](add-element-for-custom-2.md)します。<xref:System.Configuration.DictionarySectionHandler>  | カスタムアプリケーション設定を追加します。 |
| およびの<xref:System.Configuration.NameValueSectionHandler> > を[ **\<削除**](remove-element-for-custom-2.md)します。<xref:System.Configuration.DictionarySectionHandler> | 以前に定義した設定を削除します。 |
| およびの<xref:System.Configuration.NameValueSectionHandler> > を[ **\<クリア**](clear-element-for-custom-2.md)します。<xref:System.Configuration.DictionarySectionHandler> | セクションで以前に定義したすべての設定を消去します。 |

## <a name="remarks"></a>Remarks

**\<SectionName>** 要素がによって定義されるカスタム要素、  **\<セクション>** にタグを付ける、  **\<configSections>** 要素。

次の表は、ConfigurationSettings. GetConfig メソッドが各構成セクションハンドラーに対して返すオブジェクトの種類を示しています。

| 構成セクションハンドラー                        | 戻り値の型                                                |
| ---------------------------------------------------- | ---------------------------------------------------------- |
| <xref:System.Configuration.NameValueSectionHandler>  | <xref:System.Collections.Specialized.NameValueCollection>  |
| <xref:System.Configuration.DictionarySectionHandler> | <xref:System.Collections.IDictionary>                      |

## <a name="example"></a>例

次の例は、クラス<xref:System.Configuration.DictionarySectionHandler>と<xref:System.Configuration.NameValueSectionHandler>クラスを使用するセクションを宣言する方法を示しています。

最初のカスタム要素は、 `System.dll`アセンブリ内の<xref:System.Configuration.DictionarySectionHandler>クラスによって読み取られた設定を含む **\<dictionarySample >** です。 2番目のカスタム要素は **\<mysection >** です。この要素に<xref:System.Configuration.NameValueSectionHandler>は、 `System.dll`アセンブリのクラスによって読み込まれる設定が含まれます。

```xml
<configuration>
  <configSections>
    <section name="dictionarySample" type="System.Configuration.DictionarySectionHandler,System" />
    <sectionGroup name="mySectionGroup">
      <section name="mySection" type="System.Configuration.NameValueSectionHandler,System" />
    </sectionGroup>
  </configSections>
  <dictionarySample>
    <add key="myKey" value="myValue" />
  </dictionarySample>
  <mySectionGroup>
    <mySection>
      <add key="key1" value="value1" />
    </mySection>
  </mySectionGroup>
</configuration>
```

## <a name="configuration-file"></a>構成ファイル

この要素は、アプリケーション構成ファイル、コンピューター構成ファイル (machine.config)、およびアプリケーションディレクトリレベルではない web.config ファイルで使用できます。

## <a name="see-also"></a>関連項目

- [.NET Framework の構成ファイルスキーマ](index.md)
