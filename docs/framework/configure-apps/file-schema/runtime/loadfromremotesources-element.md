---
title: <loadFromRemoteSources> 要素
ms.date: 05/24/2018
helpviewer_keywords:
- loadFromRemoteSources element
- <loadFromRemoteSources> element
ms.assetid: 006d1280-2ac3-4db6-a984-a3d4e275046a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2268d07fb643621c944ef9bf561156b5332aaafc
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69920718"
---
# <a name="loadfromremotesources-element"></a>\<loadFromRemoteSources > 要素
リモートソースから読み込まれたアセンブリに .NET Framework 4 以降で完全信頼を付与するかどうかを指定します。
  
> [!NOTE]
> Visual Studio プロジェクトの [エラー一覧] またはビルドエラーのエラーメッセージが原因でこの記事にリダイレクトされた[場合は、「方法:Visual Studio](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ee890038(v=vs.100))で Web からのアセンブリを使用します。  
  
 \<configuration>  
\<ランタイム >  
\<loadFromRemoteSources>  
  
## <a name="syntax"></a>構文  
  
```xml  
<loadFromRemoteSources    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`enabled`|必須の属性です。<br /><br /> リモートソースから読み込まれたアセンブリに完全信頼を付与するかどうかを指定します。|  
  
## <a name="enabled-attribute"></a>enabled 属性  
  
|値|説明|  
|-----------|-----------------|  
|`false`|リモートソースからアプリケーションへの完全な信頼を付与しないでください。 既定値です。|  
|`true`|リモートソースからアプリケーションへの完全な信頼を付与します。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`runtime`|ランタイム初期化オプションに関する情報を含んでいます。|  
  
## <a name="remarks"></a>Remarks

.NET Framework 3.5 以前のバージョンでは、リモートの場所からアセンブリを読み込む場合、アセンブリ内のコードは、読み込み元のゾーンに依存する許可セットを使用して部分信頼で実行されます。 たとえば、web サイトからアセンブリを読み込むと、インターネットゾーンに読み込まれ、インターネットのアクセス許可セットが付与されます。 つまり、インターネットサンドボックスで実行されます。

.NET Framework 4 以降では、コードアクセスセキュリティ (CAS) ポリシーが無効になり、アセンブリが完全信頼で読み込まれます。 通常、これは、以前にサンドボックス化され<xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType>たメソッドで読み込まれたアセンブリに対して完全な信頼を付与します。 これを回避するために、リモートソースから読み込まれたアセンブリ内のコードを実行する機能は、既定では無効になっています。 既定では、リモートアセンブリを読み込もうとすると、次<xref:System.IO.FileLoadException>のような例外メッセージを含むがスローされます。

```text
System.IO.FileNotFoundException: Could not load file or assembly 'file:assem.dll' or one of its dependencies. Operation is not supported. 
(Exception from HRESULT: 0x80131515)
File name: 'file:assem.dll' ---> 
System.NotSupportedException: An attempt was made to load an assembly from a network location which would have caused the assembly 
to be sandboxed in previous versions of the .NET Framework. This release of the .NET Framework does not enable CAS policy by default, 
so this load may be dangerous. If this load is not intended to sandbox the assembly, please enable the loadFromRemoteSources switch. 
```

アセンブリを読み込んでコードを実行するには、次のいずれかを行う必要があります。

- アセンブリのサンドボックスを明示的に作成[します (「方法:サンドボックス](../../../misc/how-to-run-partially-trusted-code-in-a-sandbox.md)で部分信頼コードを実行します)。

- アセンブリのコードを完全信頼で実行します。 これを行うには、 `<loadFromRemoteSources>`要素を構成します。 以前のバージョンの .NET Framework で部分信頼で実行されるアセンブリが、.NET Framework 4 以降のバージョンで完全信頼で実行されるように指定できます。

> [!IMPORTANT]
> アセンブリを完全信頼で実行しない場合は、この構成要素を設定しないでください。 代わりに、アセンブリを読み<xref:System.AppDomain>込むためのサンドボックスを作成します。

要素の属性は、 `enabled`コードアクセスセキュリティ (CAS) が無効になっている場合にのみ有効です。 `<loadFromRemoteSources>` 既定では、CAS ポリシーは .NET Framework 4 以降のバージョンで無効になっています。 をに`enabled` `true`設定した場合、リモートアセンブリには完全な信頼が付与されます。

が`enabled`に`true`設定されていない場合は、次のいずれかの条件でがスロー<xref:System.IO.FileLoadException>されます。

- 現在のドメインのサンドボックスの動作は、.NET Framework 3.5 の動作とは異なります。 これには、CAS ポリシーを無効にし、現在のドメインをサンドボックス化しないようにする必要があります。

- 読み込まれているアセンブリが`MyComputer`ゾーンからのものではありません。

要素を`<loadFromRemoteSources>`に設定`true`すると、この例外はスローされません。 これにより、共通言語ランタイムに依存しないように指定して、読み込まれたアセンブリのセキュリティをサンドボックス化することができます。また、完全信頼での実行を許可することもできます。

## <a name="notes"></a>メモ

- .NET Framework 4.5 以降のバージョンでは、ローカルネットワーク共有上のアセンブリは既定で完全信頼で実行されます。`<loadFromRemoteSources>`要素を有効にする必要はありません。

- アプリケーションが web からコピーされた場合、ローカルコンピューターに存在する場合でも、web アプリケーションとして Windows によってフラグが設定されます。 そのようなファイルのプロパティを変更することで、その指定を変更`<loadFromRemoteSources>`できます。また、要素を使用して、アセンブリに完全信頼を付与することもできます。 別の<xref:System.Reflection.Assembly.UnsafeLoadFrom%2A>方法として、メソッドを使用して、オペレーティングシステムによって web から読み込まれたとしてフラグが設定されているローカルアセンブリを読み込むことができます。

- Windows 仮想 PC アプリケーション<xref:System.IO.FileLoadException>で実行されているアプリケーションで、が取得される場合があります。 これは、ホストコンピューター上のリンクフォルダーからファイルを読み込もうとした場合に発生する可能性があります。 また、[リモートデスクトップサービス](https://go.microsoft.com/fwlink/?LinkId=182775)(ターミナルサービス) にリンクされているフォルダーからファイルを読み込もうとした場合にも発生することがあります。 この例外を回避するに`enabled`は`true`、をに設定します。

## <a name="configuration-file"></a>構成ファイル

この要素は通常、アプリケーション構成ファイルで使用されますが、コンテキストに応じて他の構成ファイルで使用することもできます。 詳細については、.NET セキュリティブログの「 [CAS Policy: loadFromRemoteSources の暗黙的な使用方法](https://go.microsoft.com/fwlink/p/?LinkId=266839)」を参照してください。  

## <a name="example"></a>例

次の例は、リモートソースから読み込まれたアセンブリに完全信頼を付与する方法を示しています。

```xml
<configuration>  
   <runtime>  
      <loadFromRemoteSources enabled="true"/>  
   </runtime>  
</configuration>  
```

## <a name="see-also"></a>関連項目

- [CAS ポリシーの暗黙的な使用方法: loadFromRemoteSources](https://go.microsoft.com/fwlink/p/?LinkId=266839)
- [方法: サンドボックスで部分信頼コードを実行する](../../../misc/how-to-run-partially-trusted-code-in-a-sandbox.md)
- [ランタイム設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
- <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType>
