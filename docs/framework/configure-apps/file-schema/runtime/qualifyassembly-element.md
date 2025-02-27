---
title: <qualifyAssembly> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#qualifyAssembly
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/qualifyAssembly
helpviewer_keywords:
- container tags, <qualifyAssembly> element
- <qualifyAssembly> element
- qualifyAssembly element
ms.assetid: ad6442f6-1a9d-43b6-b733-04ac1b7f9b82
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4aa90a378630c9aff74923d8e8600aed15a77a5e
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69663502"
---
# <a name="qualifyassembly-element"></a>\<qualifyAssembly > 要素
部分名が使用された場合に動的に読み込む必要があるアセンブリの完全名を指定します。  
  
 \<configuration>  
\<ランタイム >  
\<assemblyBinding>  
\<qualifyAssembly>  
  
## <a name="syntax"></a>構文  
  
```xml  
      <qualifyAssembly partialName=  
      "PartialAssemblyName"  
                 fullName="FullAssemblyName"/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`partialName`|必須の属性です。<br /><br /> コードに表示されるアセンブリの名前の一部を指定します。|  
|`fullName`|必須の属性です。<br /><br /> グローバルアセンブリキャッシュに表示されるアセンブリの完全名を指定します。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`assemblyBinding`|アセンブリ バージョンのリダイレクトおよびアセンブリの位置に関する情報が含まれます。|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`runtime`|アセンブリのバインディングとガベージ コレクションに関する情報が含まれています。|  
  
## <a name="remarks"></a>Remarks  
 部分的なアセンブリ名を使用してメソッドを呼び出すと、共通言語ランタイムによって、アプリケーションのベースディレクトリでのみアセンブリが検索されます。<xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> アプリケーション構成ファイルの **qualifyAssembly>要素を使用してアセンブリの完全な情報(名前、バージョン、公開キートークン、およびカルチャ)を指定すると、共通言語ランタイムによって、\<** グローバルアセンブリキャッシュ。  
  
 **FullName**属性には、アセンブリ id の4つのフィールド (名前、バージョン、公開キートークン、およびカルチャ) を含める必要があります。 **Partialname**属性は、アセンブリを部分的に参照する必要があります。 少なくともアセンブリのテキスト名 (最も一般的なケース) を指定する必要がありますが、バージョン、公開キートークン、またはカルチャ (または4つすべての4つの組み合わせを含む) を含めることもできます。 **Partialname**は、呼び出しで指定された名前と一致する必要があります。 たとえば、構成ファイルで**partialname**属性としてを指定`Assembly.Load("math, Version=3.3.3.3")` `"math"`し、コードでを呼び出すことはできません。  
  
## <a name="example"></a>例  
 次の例では、呼び出し`Assembly.Load("math")`を`Assembly.Load("math,version=1.0.0.0,publicKeyToken=a1690a5ea44bab32,culture=neutral")`論理的にに変換します。  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <qualifyAssembly partialName="math"   
                         fullName=  
"math,version=1.0.0.0,publicKeyToken=a1690a5ea44bab32,culture=neutral"/>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [ランタイム設定スキーマ](index.md)
- [ランタイムがアセンブリを検索する方法](../../../deployment/how-the-runtime-locates-assemblies.md)
- [部分アセンブリ参照](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/0a7zy9z5(v=vs.100))
