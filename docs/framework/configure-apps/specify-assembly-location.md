---
title: アセンブリの場所の指定
ms.date: 03/30/2017
helpviewer_keywords:
- configuration [.NET Framework], applications
- application configuration [.NET Framework]
- assemblies [.NET Framework], specifying location
ms.assetid: 1cb92bd7-6bab-44cf-8fd3-36303ce84fea
ms.openlocfilehash: 43cd1d0edbb607f69f27661aae3372e93564b3b7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69932332"
---
# <a name="specifying-an-assemblys-location"></a>アセンブリの場所の指定
アセンブリの場所を指定するには、次の2つの方法があります。  
  
- [ \<コードベースの >](./file-schema/runtime/codebase-element.md)要素を使用します。  
  
- プローブ > 要素を使用します。 [ \<](./file-schema/runtime/probing-element.md)  
  
 また、 [.NET Framework 構成ツール (mscorcfg.msc)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/2bc0cxhc(v=vs.100))を使用して、アセンブリの場所を指定したり、共通言語ランタイムがアセンブリをプローブする場所を指定したりすることもできます。  
  
## <a name="using-the-codebase-element"></a>コードベース\<の > 要素の使用  
 **\<コードベース >** 要素は、アセンブリのバージョンをリダイレクトするマシン構成または発行者ポリシーファイルでのみ使用できます。 使用するアセンブリバージョンをランタイムが決定すると、バージョンを決定するファイルのコードベース設定が適用されます。 コードベースが指定されていない場合、ランタイムは通常の方法でアセンブリをプローブします。 詳細については、「[ランタイムがアセンブリを検索する方法](../deployment/how-the-runtime-locates-assemblies.md)」を参照してください。  
  
 アセンブリの場所を指定する方法を次の例に示します。  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
       <dependentAssembly>  
         <assemblyIdentity name="myAssembly"  
                           publicKeyToken="32ab4ba45e0a69a1"  
                           culture="en-us" />  
         <codeBase version="2.0.0.0"  
                   href="http://www.litwareinc.com/myAssembly.dll"/>  
       </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 **Version**属性は、厳密な名前を持つすべてのアセンブリに必要ですが、厳密な名前ではないアセンブリでは省略する必要があります。 **\<CodeBase>** 要素が必要です、 **href** 属性。 コードベースの > 要素で **\<** バージョン範囲を指定することはできません。  
  
> [!NOTE]
> 厳密な名前が付けられていないアセンブリのコードベースヒントを指定する場合、ヒントはアプリケーションベースディレクトリのアプリケーションベースまたはサブディレクトリをポイントする必要があります。  
  
## <a name="using-the-probing-element"></a>プローブ > \<要素の使用  
 実行時に、プローブによってコードベースのないアセンブリが検索されます。 プローブの詳細については、「[ランタイムがアセンブリを検索する方法](../deployment/how-the-runtime-locates-assemblies.md)」を参照してください。  
  
 アプリケーション構成ファイルの[ \<プローブ >](./file-schema/runtime/probing-element.md)要素を使用して、アセンブリを検索するときにランタイムが検索する必要があるサブディレクトリを指定できます。 次の例は、ランタイムが検索するディレクトリを指定する方法を示しています。  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <probing privatePath="bin;bin2\subbin;bin3"/>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 **PrivatePath**属性には、ランタイムがアセンブリを検索するディレクトリが含まれています。 アプリケーションが C:\Program Files\MyApp に配置されている場合、ランタイムは C:\Program Files\MyApp\Bin、C:\Program Files\MyApp\Bin2\Subbin、および C:\Program Files\MyApp\Bin3. でコードベースを指定していないアセンブリを検索します。 **PrivatePath**に指定されたディレクトリは、アプリケーションのベースディレクトリのサブディレクトリである必要があります。  
  
## <a name="see-also"></a>関連項目

- [共通言語ランタイムのアセンブリ](../app-domains/assemblies-in-the-common-language-runtime.md)
- [アセンブリを使用したプログラミング](../app-domains/programming-with-assemblies.md)
- [ランタイムがアセンブリを検索する方法](../deployment/how-the-runtime-locates-assemblies.md)
- [構成ファイルを使用したアプリの構成](index.md)
