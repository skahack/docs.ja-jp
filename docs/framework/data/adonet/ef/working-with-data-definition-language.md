---
title: データ定義言語の操作
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ec50083d-44f4-4093-9b23-5eacd601f96e
ms.openlocfilehash: c2812e261278af7763bc6b2e1a493b97cb35e3ab
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69911634"
---
# <a name="working-with-data-definition-language"></a>データ定義言語の操作
.NET Framework version 4 以降では、は[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]データ定義言語 (DDL) をサポートしています。 これにより、接続文字列、およびストレージ (SSDL) モデルのメターデータに基づいて、データベース インスタンスを作成または削除できます。  
  
 <xref:System.Data.Objects.ObjectContext> の次のメソッドでは、接続文字列と SSDL の内容を使用して、データベースの作成と削除、データベースが存在するかどうかの確認、生成された DDL スクリプトの表示を実行します。  
  
- <xref:System.Data.Objects.ObjectContext.CreateDatabase%2A>  
  
- <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A>  
  
- <xref:System.Data.Objects.ObjectContext.DatabaseExists%2A>  
  
- <xref:System.Data.Objects.ObjectContext.CreateDatabaseScript%2A>  
  
> [!NOTE]
> DDL コマンドを実行するには、十分なアクセス許可が必要です。  
  
 上記に示したメソッドは、ほとんどの作業を基になる ADO.NET データ プロバイダーに委任します。 データベース オブジェクトの生成に使用される名前付け規則が、照会および更新に使用される規則と一致していることは、プロバイダーによって保証されています。  
  
 次の例は、既存のモデルを基にデータベースを生成する方法を示しています。 また、新しいエンティティ オブジェクトはオブジェクト コンテキストに追加され、データベースに保存されます。  
  
## <a name="procedures"></a>手順  
  
### <a name="to-define-a-database-based-on-the-existing-model"></a>既存のモデルに基づいてデータベースを定義するには  
  
1. コンソール アプリケーションを作成します。  
  
2. 既存のモデルをアプリケーションに追加します。  
  
    1. という名前`SchoolModel`の空のモデルを追加します。 空のモデルを作成する方法に[ついては、「方法:新しい .edmx ファイル](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716703(v=vs.100))のトピックを作成します。  
  
     SchoolModel.edmx ファイルがプロジェクトに追加されます。  
  
    1. School モデルの概念、ストレージ、およびマッピングの内容を[School モデル](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100))のトピックからコピーします。  
  
    2. SchoolModel.edmx ファイルを開き、`edmx:Runtime` タグ内にその内容を貼り付けます。  
  
3. main 関数に次のコードを追加します。 このコードでは、データベース サーバーへの接続文字列を初期化し、DDL スクリプトを表示して、データベースを作成します。さらに、コンテキストに新しいエンティティを追加して、データベースに変更内容を保存します。  
  
     [!code-csharp[DP ObjectServices Concepts#DDL](../../../../../samples/snippets/csharp/VS_Snippets_Data/DP ObjectServices Concepts/CS/Source.cs#ddl)]
     [!code-vb[DP ObjectServices Concepts#DDL](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP ObjectServices Concepts/VB/Source.vb#ddl)]
