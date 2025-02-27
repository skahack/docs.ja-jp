---
title: ストアド プロシージャでのデータの変更
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7d8e9a46-1af6-4a02-bf61-969d77ae07e0
ms.openlocfilehash: ebf5c61010a6f658d846ed435ea3a7d18d0d3832
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69934439"
---
# <a name="modifying-data-with-stored-procedures"></a>ストアド プロシージャでのデータの変更
ストアド プロシージャは、入力パラメーターとしてデータを受け取り、出力パラメーター、結果セット、または戻り値としてデータを返すことができます。 以下のサンプルでは、入力パラメーター、出力パラメーター、および戻り値が ADO.NET によってどのようにやり取りされるかを示したものです。 この例では、主キー列が SQL Server データベースの ID 列であるテーブルに新しいレコードを挿入しています。  
  
> [!NOTE]
> SQL Server のストアド プロシージャで、<xref:System.Data.SqlClient.SqlDataAdapter> を使用してデータを編集または削除する場合、ストアド プロシージャの定義に SET NOCOUNT ON は使用しないでください。 処理された行数がゼロとして返され、`DataAdapter` によってコンカレンシーの競合として解釈されてしまいます。 この場合、<xref:System.Data.DBConcurrencyException> がスローされます。  
  
## <a name="example"></a>例  
 このサンプルでは、次のストアドプロシージャを使用して、新しいカテゴリを**Northwind** **カテゴリ**テーブルに挿入します。 このストアドプロシージャは、 **[区分名]** 列の値を入力パラメーターとして受け取り、SCOPE_IDENTITY () 関数を使用して IDENTITY フィールドの新しい値を取得し、 **CategoryID**を出力パラメーターとして返します。 Return ステートメントでは、@@ROWCOUNT関数を使用して、挿入された行数を返します。  
  
```sql
CREATE PROCEDURE dbo.InsertCategory  
  @CategoryName nvarchar(15),  
  @Identity int OUT  
AS  
INSERT INTO Categories (CategoryName) VALUES(@CategoryName)  
SET @Identity = SCOPE_IDENTITY()  
RETURN @@ROWCOUNT  
```  
  
 上述の `InsertCategory` ストアド プロシージャを <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> の <xref:System.Data.SqlClient.SqlDataAdapter> のソースとして使用する例を次に示します。 `@Identity` 出力パラメーターは、<xref:System.Data.DataSet> の `Update` メソッドが呼び出され、データベースにレコードが挿入された後で <xref:System.Data.SqlClient.SqlDataAdapter> に反映されます。 戻り値も取得されます。  
  
> [!NOTE]
> を使用<xref:System.Data.OleDb.OleDbDataAdapter>する場合は、他のパラメーターより<xref:System.Data.ParameterDirection>も前に**戻り**があるパラメーターを指定する必要があります。  
  
 [!code-csharp[DataWorks SqlClient.SprocIdentityReturn#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.SprocIdentityReturn/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.SprocIdentityReturn#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.SprocIdentityReturn/VB/source.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [ADO.NET でのデータの取得および変更](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)
- [DataAdapter と DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)
- [コマンドの実行](../../../../docs/framework/data/adonet/executing-a-command.md)
- [ADO.NET のマネージド プロバイダーと DataSet デベロッパー センター](https://go.microsoft.com/fwlink/?LinkId=217917)
