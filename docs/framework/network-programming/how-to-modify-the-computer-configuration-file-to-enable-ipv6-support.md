---
title: '方法: IPv6 のサポートを有効にするようにコンピューター構成ファイルを変更する'
ms.date: 03/30/2017
ms.assetid: 5611b677-b9cc-43b8-a434-60e18d89aada
ms.openlocfilehash: af6eb8a334108c988967a555024b524e27d40f58
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69959078"
---
# <a name="how-to-modify-the-computer-configuration-file-to-enable-ipv6-support"></a>方法: IPv6 のサポートを有効にするようにコンピューター構成ファイルを変更する
次のコード例では、IPv6 のサポートを有効にするようにコンピューター構成ファイルの *machine.config* を変更する方法を示します。 *machine.config* ファイルは、Windows がインストールされたディレクトリの *%Windir%\Microsoft.NET\Framework* フォルダーに格納されます。 コンピューターにインストールされた .NET Framework のバージョンごとに、 *%Windir%\Microsoft.NET\Framework* の下のフォルダーに別々の *machine.config* ファイルがあります (たとえば、*C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\machine.config*)。  
  
 これらの設定は、コンピューター構成ファイルよりも優先されるアプリケーション構成ファイルでも行うことができます。  
  
 .NET Framework バージョン 1.1 以前では、**ipv6 enabled** 構成スイッチの値で <xref:System.Net.Dns?displayProperty=nameWithType> クラスのメンバーが IPv6 アドレスを返すかどうかを指定します。  
  
 .NET Framework バージョン 2.0 以降では、Windows が IPv6 をサポートしている場合、<xref:System.Net.Dns?displayProperty=nameWithType> クラスのすべてのメンバー (<xref:System.Net.Dns.GetHostEntry%2A?displayProperty=nameWithType> メソッドなど) が 1 つの制限付きで IPv6 アドレスを返します。 <xref:System.Net.Dns?displayProperty=nameWithType> クラスの古いメンバー (<xref:System.Net.Dns.Resolve%2A?displayProperty=nameWithType> メソッドなど) は、構成ファイル内の値を読み取り、認識します。  
  
> [!NOTE]
> .NET Framework バージョン 2.0 以降では、IPv6 は既定で有効になります。 .NET Framework バージョン 1.1 以前では、IPv6 は既定で無効になります。  
  
## <a name="example"></a>例  
  
```xml  
<system.net>  
    …………  
    <settings>  
        …………  
        <ipv6 enabled="true"/>   
    ……………  
    </settings>  
    ………………  
<system.net>  
```  
  
## <a name="see-also"></a>関連項目

- [IPv6 アドレス指定](../../../docs/framework/network-programming/ipv6-addressing.md)
- [ネットワーク設定スキーマ](../../../docs/framework/configure-apps/file-schema/network/index.md)
- [\<ipv6> 要素 (ネットワーク設定)](../../../docs/framework/configure-apps/file-schema/network/ipv6-element-network-settings.md)
