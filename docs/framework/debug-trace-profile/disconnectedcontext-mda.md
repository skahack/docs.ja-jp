---
title: disconnectedContext MDA
ms.date: 03/30/2017
helpviewer_keywords:
- DisconnectedContext MDA
- MDAs (managed debugging assistants), disconnected context
- dead context
- transitioning disconnected apartment or context
- context disconnections
- managed debugging assistants (MDAs), disconnected context
ms.assetid: 1887d31d-7006-4491-93b3-68fd5b05f71d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1819fffaf2eccb6a26578eaf993100b8eca7c76e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966431"
---
# <a name="disconnectedcontext-mda"></a>disconnectedContext MDA
CLR が COM オブジェクトに関する要求を処理中に、切断しているアパートメントまたはコンテキストに遷移しようとすると、`disconnectedContext` マネージド デバッグ アシスタント (MDA) がアクティブ化されます。  
  
## <a name="symptoms"></a>症状  
 [ランタイム呼び出し可能ラッパー](../../standard/native-interop/runtime-callable-wrapper.md) (RCW) に対する呼び出しは、その呼び出しが存在する COM コンポーネントではなく、現在のアパートメントまたはコンテキスト内の基になる COM コンポーネントへ送られます。 シングル スレッド アパートメント (STA) コンポーネントのように、COM コンポーネントがマルチスレッド化されていない場合、これが原因で破損やデータ損失が発生する可能性があります。 あるいは RCW 自体がプロキシである場合、呼び出しの結果として <xref:System.Runtime.InteropServices.COMException> がスローされ、HRESULT が RPC_E_WRONG_THREAD になる可能性があります。  
  
## <a name="cause"></a>原因  
 OLE アパートメントまたはコンテキストは、CLR が遷移を試行しようとしたときに、既にシャットダウンしています。 ほとんどの場合これは、STA アパートメントが所有するすべての COM コンポーネントが完全に解放される前に、それらの STA アパートメントがシャットダウンしたことが原因で発生します。また、RCW でユーザー コードからの明示的な呼び出しが実行された結果として発生することや、CLR 自体が COM コンポーネントを操作している場合 (たとえば関連する RCW がガーベージ コレクションされているのに CRL が COM コンポーネントを解放する場合など) にも発生する可能性があります。  
  
## <a name="resolution"></a>解決策  
 この問題を回避するには、アプリケーションがアパートメントに存在するすべてのオブジェクトの処理を完了する前に、STA を所有するスレッドが強制終了しないようにします。 コンテキストの場合も同様に、アプリケーションがコンテキスト内部に存在するすべての COM コンポーネントの処理を完了するまでは、コンテキストがシャットダウンしないようにします。  
  
## <a name="effect-on-the-runtime"></a>ランタイムへの影響  
 この MDA は CLR に影響しません。 接続していないコンテキストに関するデータを報告するだけです。  
  
## <a name="output"></a>Output  
 非接続アパートメントまたはコンテキストのコンテキスト Cookie を報告します。  
  
## <a name="configuration"></a>構成  
  
```xml  
<mdaConfig>  
  <assistants>  
    <disconnectedContext />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [マネージド デバッグ アシスタントによるエラーの診断](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
- [相互運用マーシャリング](../../../docs/framework/interop/interop-marshaling.md)
