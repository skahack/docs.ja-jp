---
title: SQL XML 列値
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d97ce4da-f09c-4d1e-85b7-a0ccedd7246a
ms.openlocfilehash: 29e9ac5b95b62ef2a4467bf41484c3740d550abd
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964949"
---
# <a name="sql-xml-column-values"></a>SQL XML 列値
SQL Server は`xml`データ型をサポートし、開発者は<xref:System.Data.SqlClient.SqlCommand>クラスの標準動作を使用して、この型を含む結果セットを取得できます。 `xml` 列は、その他の列と同じようにして (<xref:System.Data.SqlClient.SqlDataReader> などに) 取得することができますが、その列の内容を XML として使用する場合は、<xref:System.Xml.XmlReader> を使用する必要があります。  
  
## <a name="example"></a>例  
 次のコンソールアプリケーションでは、 `xml` **AdventureWorks**データベースの<xref:System.Data.SqlClient.SqlDataReader> **Sales. Store**テーブルからインスタンスに、列を含む2つの行を選択します。 それぞれの行について、`xml` 列の値は、<xref:System.Data.SqlClient.SqlDataReader.GetSqlXml%2A> の <xref:System.Data.SqlClient.SqlDataReader> メソッドを使用して読み取ります。 値は、<xref:System.Xml.XmlReader> に格納されます。 内容を <xref:System.Data.SqlClient.SqlDataReader.GetSqlXml%2A> 変数に設定する場合は、<xref:System.Data.IDataRecord.GetValue%2A> メソッドではなく <xref:System.Data.SqlTypes.SqlXml> を使用する必要があることに注意してください。<xref:System.Data.IDataRecord.GetValue%2A> は、`xml` 列の値を文字列として返します。  
  
> [!NOTE]
> SQL Server をインストールした場合、既定では、 **AdventureWorks**サンプルデータベースはインストールされません。 SQL Server Setup を実行してインストールします。  
  
 [!code-csharp[DataWorks SqlClient.GetXmlDataReader#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.GetXmlDataReader/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.GetXmlDataReader#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.GetXmlDataReader/VB/source.vb#1)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.SqlTypes.SqlXml>
- [SQL Server における XML データ](../../../../../docs/framework/data/adonet/sql/xml-data-in-sql-server.md)
- [ADO.NET のマネージド プロバイダーと DataSet デベロッパー センター](https://go.microsoft.com/fwlink/?LinkId=217917)
