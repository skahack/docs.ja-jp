---
title: '方法: 非同期データサービスクエリの実行 (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, asynchronous operations
- asynchronous operations [WCF Data Services]
ms.assetid: 902a2dc1-d0e9-4b00-90a8-becc4cb1f6a7
ms.openlocfilehash: b5530dea50a6fab8478639def9624f8715ae3f3e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69952394"
---
# <a name="how-to-execute-asynchronous-data-service-queries-wcf-data-services"></a>方法: 非同期データサービスクエリの実行 (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] クライアント ライブラリを使用して、クエリの実行や変更の保存などのクライアント サーバー操作を非同期で実行できます。 詳細については、「[非同期操作](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)」を参照してください。  
  
> [!NOTE]
> 特定のスレッドでコールバックが呼び出される必要のあるアプリケーションでは、<xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A> メソッドの実行を明示的にマーシャリングする必要があります。 詳細については、「[非同期操作](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)」を参照してください。  
  
 このトピックの例では、Northwind サンプル データ サービスおよび自動生成されたクライアント データ サービス クラスを使用します。 このサービスとクライアントデータクラスは、 [WCF Data Services のクイックスタート](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)を完了したときに作成されます。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> メソッドを呼び出してクエリを開始することで、非同期クエリを実行する方法を示します。 インライン デリゲートは、<xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A> メソッドを呼び出してクエリ結果を表示します。  
  
 [!code-csharp[Astoria Northwind Client#ExecuteQueryAsync](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#executequeryasync)]
 [!code-vb[Astoria Northwind Client#ExecuteQueryAsync](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#executequeryasync)]  
  
## <a name="see-also"></a>関連項目

- [WCF Data Services クライアント ライブラリ](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)
