---
title: .NET Framework のネットワークのトレース
ms.date: 03/30/2017
helpviewer_keywords:
- debugging [.NET Framework], network tracing
- methods, network tracing
- Networking
- trace enabled debugging
- network tracing, about network tracing
- network tracing
- network, network tracing
- traffic tracing
- tracing [.NET Framework], network
- deploying applications [.NET Framework], network traffic
- capturing network traffic
- Internet, network tracing
- Network Resources
- output, network tracing
- method invocations
ms.assetid: e993b7c3-087f-45d8-9c02-9dded936d804
ms.openlocfilehash: 3d556bc3b8746fe2d05a8e225b91ecf59bd404fd
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963938"
---
# <a name="network-tracing-in-the-net-framework"></a>.NET Framework のネットワークのトレース
.NET Framework のネットワークのトレースでは、メソッド呼び出しについての情報、およびマネージド アプリケーションによって生成されるネットワーク トラフィックについての情報にアクセスできます。 この機能は、開発中のアプリケーションのデバッグや、配置済みのアプリケーションの分析に役立ちます。 ネットワークのトレースの出力は、開発時および稼動環境でのさまざまな使用方法をサポートするようにカスタマイズできます。  
  
 .NET Framework でのネットワークのトレースを有効にするには、トレースの出力先を選択し、アプリケーションまたはコンピューターの構成ファイルにネットワークのトレースの構成設定を追加する必要があります。 構成ファイルの内容、およびそれらの使用方法については、「[構成ファイル](../../../docs/framework/configure-apps/index.md)」を参照してください。 ネットワークのトレースを有効にする方法については、「[ネットワークのトレースを有効にする](../../../docs/framework/network-programming/enabling-network-tracing.md)」を参照してください。 構成ファイルに追加する必要がある設定については、「[方法:ネットワークのトレースを構成する](../../../docs/framework/network-programming/how-to-configure-network-tracing.md)」をご覧ください。  
  
 トレースが有効なときは、**System.Net** クラスによって出力されるトレース情報をキャプチャできます。 トレース情報を生成するネットワーク クラスのメンバーについては、.NET Framework クラス ライブラリのドキュメントの「解説」セクションに次のメモが含まれます。  
  
> [!NOTE]
> このメンバーは、アプリケーションでネットワーク トレースが有効にされている場合にトレース情報を出力します。 詳細については、「ネットワークのトレース」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [ネットワークのトレースの有効化](../../../docs/framework/network-programming/enabling-network-tracing.md)
- [方法: ネットワークのトレースを構成する](../../../docs/framework/network-programming/how-to-configure-network-tracing.md)
- [ネットワークのトレースの解釈](../../../docs/framework/network-programming/interpreting-network-tracing.md)
- [アプリケーションのトレースとインストルメント](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)
