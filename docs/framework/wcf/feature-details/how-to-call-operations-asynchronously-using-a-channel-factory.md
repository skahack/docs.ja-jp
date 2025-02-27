---
title: '方法: チャネル ファクトリを使用して、非同期的に操作を呼び出す'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: cc17dd47-b9ad-451c-a362-e36e0aac7ba0
ms.openlocfilehash: 3080514d06119a2f1b621cff16056ac7577c30b3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966802"
---
# <a name="how-to-call-operations-asynchronously-using-a-channel-factory"></a>方法: チャネル ファクトリを使用して、非同期的に操作を呼び出す
ここでは、<xref:System.ServiceModel.ChannelFactory%601> ベースのクライアント アプリケーションを使用する場合に、クライアントからサービス操作に非同期にアクセスする方法について説明します。 サービスを呼び出すために <xref:System.ServiceModel.ClientBase%601?displayProperty=nameWithType> オブジェクトを使用する場合は、イベント ドリブンの非同期呼び出しモデルを使用できます。 詳細については、「[方法 :サービス操作を非同期](../../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)に呼び出します。 イベントベースの非同期呼び出しモデルの詳細については、「[イベントベースの非同期パターン (EAP)](../../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)」を参照してください。  
  
 このトピックのサービスは、`ICalculator` インターフェイスを実装しています。 クライアントはこのインターフェイスにある操作を非同期に呼び出すことができます。これはたとえば `Add` という操作を `BeginAdd` と `EndAdd` の 2 つのメソッドに分割できることを意味します。前者によって呼び出しを開始し、後者によって操作の完了時に結果を取得します。 サービスで操作を非同期に実装する方法を示す例について[は、「方法:非同期サービス操作](../../../../docs/framework/wcf/how-to-implement-an-asynchronous-service-operation.md)を実装します。 同期操作と非同期操作の詳細については、「[同期操作と非同期操作](../../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md)」を参照してください。  
  
## <a name="procedure"></a>プロシージャ  
  
#### <a name="to-call-wcf-service-operations-asynchronously"></a>WCF サービス操作を非同期に呼び出すには  
  
1. 次のコマンドに示すように、 `/async`オプションを指定して[ServiceModel メタデータユーティリティツール (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)ツールを実行します。  
  
    ```  
    svcutil /n:http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples http://localhost:8000/servicemodelsamples/service/mex /a  
    ```  
  
     これにより、操作の非同期クライアント版のサービス コントラクトが生成されます。  
  
2. 次のサンプル コードに示すように、非同期操作の完了時に呼び出されるコールバック関数を作成します。  
  
     [!code-csharp[C_How_To_CF_Async#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/client.cs#2)]
     [!code-vb[C_How_To_CF_Async#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/client.vb#2)]  
  
3. サービス操作に非同期にアクセスするには、次のサンプル コードに示すように、クライアントを作成して `Begin[Operation]` (たとえば `BeginAdd`) を呼び出し、コールバック関数を指定します。  
  
     [!code-csharp[C_How_To_CF_Async#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/client.cs#3)]
     [!code-vb[C_How_To_CF_Async#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/client.vb#3)]  
  
     コールバック関数が実行されると、クライアントは `End<operation>` (`EndAdd` など) を呼び出して結果を取得します。  
  
## <a name="example"></a>例  
 上記の手順で使用したクライアント コードで使用するサービスは、次のコードに示すように `ICalculator` インターフェイスを実装しています。 サービス側`Add`では、前の`Subtract`クライアントの手順がクライアント上で非同期に呼び出されている場合でも、コントラクトの操作と操作は、Windows Communication Foundation (WCF) の実行時によって同期的に呼び出されます。 `Multiply` 操作と `Divide` 操作は、クライアントで同期して呼び出される場合でも、サービス側ではサービスを非同期に呼び出すように使用されます。 この例では、<xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> プロパティを `true` に設定します。 このプロパティ設定は、.NET Framework 非同期パターンの実装と組み合わせて、操作を非同期的に呼び出すように実行時に指示します。  
  
 [!code-csharp[C_How_To_CF_Async#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/service.cs#4)]
 [!code-vb[C_How_To_CF_Async#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/service.vb#4)]  
