---
title: トランザクションとバルク コピー操作
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f6f0cbc9-f7bf-4d6e-875f-ad1ba0b4aa62
ms.openlocfilehash: fb27e11f81451d6a982edcf5b88b23861bef3c37
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69938436"
---
# <a name="transaction-and-bulk-copy-operations"></a>トランザクションとバルク コピー操作
バルク コピー操作は、単独の操作として、または、手順が複数あるトランザクションの 1 手順として実行されます。 手順が複数あるトランザクションの 1 手順として実行する場合、同一トランザクション内でバルク コピー操作を複数回実行することができます。また、挿入、更新、削除などの他のデータベース操作を実行していても、トランザクション全体をコミットまたはロールバックできます。  
  
 既定では、バルク コピー操作は単独の操作として実行されます。 このバルク コピー操作は非トランザクション方式で処理され、ロールバックできません。 エラーが発生したときに一括コピーのすべてまたは一部をロールバックする必要がある場合<xref:System.Data.SqlClient.SqlBulkCopy>は、管理されたトランザクションを使用するか、既存のトランザクション内で一括コピー操作を実行するか、または**システムトランザクション**<xref:System.Transactions.Transaction>に参加することができます。  
  
## <a name="performing-a-non-transacted-bulk-copy-operation"></a>非トランザクション処理のバルク コピー操作の実行  
 次のコンソール アプリケーションでは、非トランザクション処理のバルク コピー操作で処理中にエラーが検出されたときに、そのエラーの内容を表示します。  
  
 この例では、基になるテーブルとターゲットテーブルに`Identity`それぞれ、 **ProductID**という名前の列が含まれています。 このコードでは、まず、すべての行を削除し、ソーステーブルに存在することがわかっている単一の行を挿入することによって、変換先テーブルを準備します。 既定では、`Identity` 列の新しい値は追加した各行のコピー先のテーブル内で生成されます。 この例では、代わりに、コピー元のテーブルからの `Identity` 値を使用するバルク ロード処理を強制的に行う接続が開かれている場合、オプションが設定されます。  
  
 このバルク コピー操作は、<xref:System.Data.SqlClient.SqlBulkCopy.BatchSize%2A> プロパティを 10 に設定して実行されます。 処理中に無効な行が検出されると、例外がスローされます。 この最初の例では、バルク コピー操作はトランザクション処理ではありません。 エラー発生ポイントまでにコピーされたバッチはすべてコミットされ、重複キーが含まれるバッチはロールバックされます。また、バルク コピー操作は、他のバッチを処理する前に中止されます。  
  
> [!NOTE]
> このサンプルは、「[一括コピーの例のセットアップ](../../../../../docs/framework/data/adonet/sql/bulk-copy-example-setup.md)」で説明されているように作業テーブルを作成しない限り、実行されません。 このコードは、 **SqlBulkCopy**のみを使用する構文を示すために用意されています。 コピー元とコピー先のテーブルが同じ SQL Server インスタンスに配置されている場合は、transact-sql`INSERT … SELECT`ステートメントを使用してデータをコピーする方が簡単で高速です。  
  
 [!code-csharp[DataWorks SqlBulkCopy.DefaultTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.DefaultTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.DefaultTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.DefaultTransaction/VB/source.vb#1)]  
  
## <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>トランザクションでの専用のバルク コピー操作の実行  
 既定では、バルク コピー操作は専用のトランザクションで実行されます。 専用のバルク コピー操作を実行する場合は、接続文字列を使用して <xref:System.Data.SqlClient.SqlBulkCopy> のインスタンスを新しく作成するか、またはアクティブなトランザクションは使用せずに既存の <xref:System.Data.SqlClient.SqlConnection> オブジェクトを使用します。 いずれの場合も、バルク コピー操作によってトランザクションを作成し、コミットするかまたはロールバックします。  
  
 <xref:System.Data.SqlClient.SqlBulkCopyOptions.UseInternalTransaction> クラス コンストラクターの <xref:System.Data.SqlClient.SqlBulkCopy> オプションを明示的に指定することで、バルク コピー操作を専用のトランザクションで実行でき、バルク コピー操作の各バッチを別々のトランザクション内で実行できます。  
  
> [!NOTE]
> 異なるバッチは別々のトランザクション内で実行されます。このため、バルク コピー操作中にエラーが発生した場合、現在処理中のバッチの行はすべてロールバックされますが、エラーの発生前にバッチでコピーされた行はデータベースに残ります。  
  
 次のコンソールアプリケーションは、前の例と似ていますが、例外が1つあります。この例では、一括コピー操作で独自のトランザクションを管理しています。 エラー発生ポイントまでにコピーされたバッチはすべてコミットされ、重複キーが含まれるバッチはロールバックされます。また、バルク コピー操作は、他のバッチを処理する前に中止されます。  
  
> [!IMPORTANT]
> このサンプルは、「[一括コピーの例のセットアップ](../../../../../docs/framework/data/adonet/sql/bulk-copy-example-setup.md)」で説明されているように作業テーブルを作成しない限り、実行されません。 このコードは、 **SqlBulkCopy**のみを使用する構文を示すために用意されています。 コピー元とコピー先のテーブルが同じ SQL Server インスタンスに配置されている場合は、transact-sql`INSERT … SELECT`ステートメントを使用してデータをコピーする方が簡単で高速です。  
  
 [!code-csharp[DataWorks SqlBulkCopy.InternalTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.InternalTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.InternalTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.InternalTransaction/VB/source.vb#1)]  
  
## <a name="using-existing-transactions"></a>既存のトランザクションの使用  
 既存の <xref:System.Data.SqlClient.SqlTransaction> コンストラクターの <xref:System.Data.SqlClient.SqlBulkCopy> オブジェクトをパラメーターとして指定できます。 この場合、バルク コピー操作は既存のトランザクションで実行されます。このトランザクションの状態は変更されません (つまり、コミットも中止もされません)。 これにより、アプリケーションは他のデータベース操作を行うトランザクションでバルク コピー操作を行うことができます。 ただし、<xref:System.Data.SqlClient.SqlTransaction> オブジェクトを指定しない場合、null 参照を渡した場合、接続にアクティブなトランザクションがある場合は、例外がスローされます。  
  
 エラーが発生したためすべてのバルク コピー操作をロールバックする必要がある場合、または、ロールバック可能な大きな処理の一部としてバルク コピー処理を実行する場合、<xref:System.Data.SqlClient.SqlTransaction> オブジェクトを <xref:System.Data.SqlClient.SqlBulkCopy> コンストラクターに指定することができます。  
  
 次のコンソール アプリケーションは最初の (トランザクションのない) 例とほぼ同じですが、バルク コピー操作がより大きな外部トランザクションに含まれている点が異なります。 主キーの違反エラーが発生した場合、トランザクションはすべてロールバックされ、コピー先のテーブルに行は追加されません。  
  
> [!IMPORTANT]
> このサンプルは、「[一括コピーの例のセットアップ](../../../../../docs/framework/data/adonet/sql/bulk-copy-example-setup.md)」で説明されているように作業テーブルを作成しない限り、実行されません。 このコードは、 **SqlBulkCopy**のみを使用する構文を示すために用意されています。 コピー元とコピー先のテーブルが同じ SQL Server インスタンスに配置されている場合は、transact-sql`INSERT … SELECT`ステートメントを使用してデータをコピーする方が簡単で高速です。  
  
 [!code-csharp[DataWorks SqlBulkCopy.SqlTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.SqlTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.SqlTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.SqlTransaction/VB/source.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [SQL Server でのバルク コピー操作](../../../../../docs/framework/data/adonet/sql/bulk-copy-operations-in-sql-server.md)
- [ADO.NET のマネージド プロバイダーと DataSet デベロッパー センター](https://go.microsoft.com/fwlink/?LinkId=217917)
