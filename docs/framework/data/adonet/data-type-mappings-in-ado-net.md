---
title: ADO.NET でのデータ型のマッピング
ms.date: 03/30/2017
ms.assetid: d4afab94-ada6-4c77-a73c-41f17bae6b5a
ms.openlocfilehash: ddb3c1c5551336ace66bab53af3beb83b6cd2d34
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950410"
---
# <a name="data-type-mappings-in-adonet"></a>ADO.NET でのデータ型のマッピング
.NET Framework は共通型システムを基にしています。このシステムは実行時の型の宣言、使用、および管理方法を定義するものです。 値型と参照型の両方から構成されており、これらはすべて <xref:System.Object> 基本型から派生します。 データ ソースを操作するときは、データ型が明示的に指定されていない場合はデータ プロバイダーから推論されます。 たとえば、<xref:System.Data.DataSet> オブジェクトは、特定のデータ ソースには依存しません。 `DataSet` 内のデータはデータ ソースから取得され、変更は `DataAdapter` によってデータ ソースに反映されます。 これは、がデータ`DataAdapter`ソースの<xref:System.Data.DataTable>値`DataSet`を使用してのに fill を行うときに、内の列の`DataTable`結果として得られるデータ型が、.NET Framework データプロバイダーに固有の型ではなく、.NET Framework 型であることを意味します。は、データソースへの接続に使用されます。  
  
 同様に、が`DataReader`データソースから値を返す場合、結果の値は .NET Framework 型のローカル変数に格納されます。 の`Fill`操作`DataAdapter` と`Get`のメソッドの両方について、.NETFramework型は.NETFrameworkデータプロバイダーから返された値から推論されます。`DataReader`  
  
 返される値の型がわかっている場合は、推論されるデータ型を使用するのではなく、`DataReader` の型指定されたアクセサー メソッドを使用できます。 型指定されたアクセサーメソッドを使用すると、特定の .NET Framework 型として値を返すことで、より優れたパフォーマンスが得られます。これにより、追加の型変換が不要になります。  
  
> [!NOTE]
> .NET Framework データプロバイダーのデータ型の Null 値は、 `DBNull.Value`によって表されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [SQL Server データ型のマッピング](../../../../docs/framework/data/adonet/sql-server-data-type-mappings.md)  
 推論されたデータ型マッピングおよび <xref:System.Data.SqlClient> のデータ アクセサー メソッドを一覧で示します。  
  
 [OLE DB データ型のマッピング](../../../../docs/framework/data/adonet/ole-db-data-type-mappings.md)  
 推論されたデータ型マッピングおよび <xref:System.Data.OleDb> のデータ アクセサー メソッドを一覧で示します。  
  
 [ODBC データ型のマッピング](../../../../docs/framework/data/adonet/odbc-data-type-mappings.md)  
 推論されたデータ型マッピングおよび <xref:System.Data.Odbc> のデータ アクセサー メソッドを一覧で示します。  
  
 [Oracle データ型のマッピング](../../../../docs/framework/data/adonet/oracle-data-type-mappings.md)  
 推論されたデータ型マッピングおよび <xref:System.Data.OracleClient> のデータ アクセサー メソッドを一覧で示します。  
  
 [浮動小数点数](../../../../docs/framework/data/adonet/floating-point-numbers.md)  
 開発者が浮動小数点数を扱う際の発生頻度の高い問題について説明します。  
  
## <a name="see-also"></a>関連項目

- [SQL Server データ型と ADO.NET](../../../../docs/framework/data/adonet/sql/sql-server-data-types.md)
- [パラメーターおよびパラメーター データ型の構成](../../../../docs/framework/data/adonet/configuring-parameters-and-parameter-data-types.md)
- [データベース スキーマ情報の取得](../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)
- [共通型システム](../../../standard/base-types/common-type-system.md)
- [変換 (型を)](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/t8s7t9bf(v=vs.90))
- [ADO.NET のマネージド プロバイダーと DataSet デベロッパー センター](https://go.microsoft.com/fwlink/?LinkId=217917)
