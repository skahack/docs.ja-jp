---
title: '方法: 行をデータベースに挿入する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 44d99680-69c7-4879-a732-f6771b334211
ms.openlocfilehash: 2852b0593f8b213f8cad6f9a2ab8f08eeb2a4dec
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69943636"
---
# <a name="how-to-insert-rows-into-the-database"></a>方法: 行をデータベースに挿入する
データベースに行を挿入するには、関連付けら[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]れている<xref:System.Data.Linq.Table%601>コレクションにオブジェクトを追加し、変更をデータベースに送信します。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]では、変更内容が適切`INSERT`な SQL コマンドに変換されます。  
  
> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の `Insert`、`Update`、および `Delete` の既定のデータベース操作メソッドはオーバーライドできます。 詳細については、「[挿入、更新、および削除の操作をカスタマイズ](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md)する」を参照してください。  
>   
>  Visual Studio を使用する開発者は、オブジェクトリレーショナルデザイナーを使用して、同じ目的でストアドプロシージャを開発できます。  
  
 以下の手順では、有効な <xref:System.Data.Linq.DataContext> で Northwind データベースに接続されるものと想定しています。 詳細については、「[方法 :データベース](../../../../../../docs/framework/data/adonet/sql/linq/how-to-connect-to-a-database.md)に接続します。  
  
### <a name="to-insert-a-row-into-the-database"></a>行をデータベースに挿入するには  
  
1. 送信する列データを含む新しいオブジェクトを作成します。  
  
2. データベース内のターゲットテーブルに[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]関連付けられている`Table`コレクションに、新しいオブジェクトを追加します。  
  
3. データベースに変更内容を送信します。  
  
## <a name="example"></a>例  
 次のサンプル コードでは、`Order` 型の新しいオブジェクトを作成し、適切な値をこのオブジェクトに設定します。 その後で、新しいオブジェクトを `Order` コレクションに追加します。 最後にこの変更内容を `Orders` テーブルの新しい行としてデータベースに送信します。  
  
 [!code-csharp[System.Data.Linq.Table#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.table/cs/program.cs#1)]
 [!code-vb[System.Data.Linq.Table#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.table/vb/module1.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [方法: 変更の競合を管理する](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)
- [DataContext メソッド (O/R デザイナー)](/visualstudio/data-tools/datacontext-methods-o-r-designer)
- [方法: 更新、挿入、および削除を実行するストアド プロシージャを割り当てる (O/R デザイナー)](/visualstudio/data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer)
- [データの変更と変更の送信](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)
