---
title: 接続の確立
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3af512f3-87d9-4005-9e2f-abb1060ff43f
ms.openlocfilehash: b4a61306cd9b61f84eff16ffaac302317b6dfe44
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69959190"
---
# <a name="establishing-the-connection"></a>接続の確立
Microsoft SQL Server に接続する場合は、.NET Framework Data Provider for SQL Server の <xref:System.Data.SqlClient.SqlConnection> オブジェクトを使用します。 OLE DB データ ソースに接続する場合は、.NET Framework Data Provider for OLE DB の <xref:System.Data.OleDb.OleDbConnection> オブジェクトを使用します。 ODBC データ ソースに接続する場合は、.NET Framework Data Provider for ODBC の <xref:System.Data.Odbc.OdbcConnection> オブジェクトを使用します。 Oracle データ ソースに接続する場合は、.NET Framework Data Provider for Oracle の <xref:System.Data.OracleClient.OracleConnection> オブジェクトを使用します。 接続文字列を安全に格納および取得する方法については、「[接続情報の保護](../../../../docs/framework/data/adonet/protecting-connection-information.md)」を参照してください。  
  
## <a name="closing-connections"></a>接続の終了  
 接続がプールに返されるようにするために、接続を使い終えたら必ず接続を終了することをお勧めします。 Visual Basic または C# の `Using` ブロックは、コードがこのブロックを終了したときに接続を破棄します。これは、未処理の例外の場合でも実行されます。 詳細については、「 [Using ステートメント](../../../csharp/language-reference/keywords/using-statement.md)」および「 [using ステートメント](../../../visual-basic/language-reference/statements/using-statement.md)」を参照してください。  
  
 また、使用しているプロバイダーの接続オブジェクトの `Close` または `Dispose` メソッドを使用することもできます。 明示的に終了されていない接続は、プールに追加したり返したりすることができないことがあります。 たとえば、スコープ外に出ても、明示的に終了されていない接続は、最大プール サイズに達した時点でその接続がまだ有効である場合にだけ接続プールに返されます。 詳細については、「 [OLE DB、ODBC、および Oracle 接続プール](../../../../docs/framework/data/adonet/ole-db-odbc-and-oracle-connection-pooling.md)」を参照してください。  
  
> [!NOTE]
> クラスの`Close` メソッド`Finalize`で`Dispose` 、**接続**、 **DataReader**、またはその他のマネージオブジェクトでまたはを呼び出さないでください。 終了処理では、クラスに直接所有されているアンマネージ リソースだけを解放してください。 クラスがアンマネージ リソースを所有していない場合は、クラス定義に `Finalize` メソッドを含めないでください。 詳細については、「[ガベージコレクション](../../../standard/garbage-collection/index.md)」を参照してください。  
  
> [!NOTE]
> 接続が接続プールからフェッチされたり接続プールに返されたりしたとき、ログイン イベントとログアウト イベントはサーバーで発生しません。これは、接続プールに返されても接続は実際には終了していないためです。 詳しくは、「[SQL Server の接続プール (ADO.NET)](../../../../docs/framework/data/adonet/sql-server-connection-pooling.md)」をご覧ください。  
  
## <a name="connecting-to-sql-server"></a>SQL Server への接続  
 .NET Framework Data Provider for SQL Server は、OLE DB (ADO) 接続文字列フォーマットに似た接続文字列フォーマットをサポートします。 有効な文字列フォーマットの名前および値については、<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> オブジェクトの <xref:System.Data.SqlClient.SqlConnection> プロパティを参照してください。 また、<xref:System.Data.SqlClient.SqlConnectionStringBuilder> クラスを使用すると、構文的に正しい接続文字列を実行時に作成できます。 詳細については、「[接続文字列ビルダー](../../../../docs/framework/data/adonet/connection-string-builders.md)」をご覧ください。  
  
 SQL Server のデータベースへの接続を開いて確立する方法を次のサンプル コードに示します。  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New SqlConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (SqlConnection connection = new SqlConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
### <a name="integrated-security-and-aspnet"></a>統合セキュリティと ASP.NET  
 SQL Server 統合セキュリティ (信頼関係接続とも呼ばれます) は、SQL Server への接続を保護します。接続文字列でユーザー ID とパスワードを公開することがなく、接続の認証用に推奨されている方法でもあるためです。 統合セキュリティでは、実行中のプロセスの現在のセキュリティ ID またはトークンを使用します。 これは、デスクトップ アプリケーションでは通常、現在ログオンしているユーザーの ID です。  
  
 ASP.NET アプリケーションのセキュリティ ID は、他のオプションのうちのいずれかに設定することもできます。 ASP.NET アプリケーションが SQL Server に接続するときに使用するセキュリティ id について理解を深めるには、「 [ASP.NET Impersonation](https://docs.microsoft.com/previous-versions/aspnet/xh507fc5(v=vs.100))」、「 [ASP.NET Authentication](https://docs.microsoft.com/previous-versions/aspnet/eeyk640h(v=vs.100)) [」、「How to:Windows 統合セキュリティ](https://docs.microsoft.com/previous-versions/aspnet/bsz5788z(v=vs.100))を使用して SQL Server にアクセスします。  
  
## <a name="connecting-to-an-ole-db-data-source"></a>OLE DB データ ソースへの接続  
 OLE DB の .NET Framework Data Provider は、 **OleDbConnection**オブジェクトを使用して、OLE DB を使用して公開されるデータソースへの接続を提供します (SQLOLEDB、OLE DB プロバイダー)。  
  
 .NET Framework Data Provider for OLE DB で使用される接続文字列フォーマットは ADO で使用される接続文字列フォーマットと同じですが、次の例外があります。  
  
- **Provider**キーワードが必要です。  
  
- **URL**、**リモートプロバイダー**、および**リモートサーバー**のキーワードはサポートされていません。  
  
 OLE DB 接続文字列の詳細については、「<xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A>」を参照してください。 また、<xref:System.Data.OleDb.OleDbConnectionStringBuilder> を使用すると、接続文字列を実行時に作成できます。  
  
> [!NOTE]
> **OleDbConnection**オブジェクトは、OLE DB プロバイダーに固有の動的プロパティの設定または取得をサポートしていません。 OLE DB プロバイダーに接続文字列で渡すことができるプロパティだけがサポートされています。  
  
 OLE DB データ ソースへの接続を作成し確立する方法を次のサンプル コードに示します。  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OleDbConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OleDbConnection connection =   
  new OleDbConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
## <a name="do-not-use-universal-data-link-files"></a>Universal Data Link ファイルは使用しない  
 ユニバーサルデータリンク (UDL) ファイルの**OleDbConnection**の接続情報を指定することができます。ただし、この操作は避けてください。 UDL ファイルは暗号化されないため、接続文字列をテキスト形式で表現してしまいます。 UDL ファイルは、アプリケーションにとって外部ファイルをベースにしたリソースであるため、.NET Framework でセキュリティ保護できません。  
  
## <a name="connecting-to-an-odbc-data-source"></a>ODBC データ ソースへの接続  
 ODBC の .NET Framework Data Provider は、 **OdbcConnection**オブジェクトを使用して odbc を使用して公開されるデータソースへの接続を提供します。  
  
 .NET Framework Data Provider for ODBC で使用される接続文字列フォーマットは、できるだけ ODBC の接続文字列フォーマットと一致するようにデザインされています。 ODBC データ ソース名 (DSN) を指定することもできます。 **OdbcConnection**の詳細については、「 <xref:System.Data.Odbc.OdbcConnection>」を参照してください。  
  
 ODBC データ ソースへの接続を作成し確立する方法を次のサンプル コードに示します。  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OdbcConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OdbcConnection connection =   
  new OdbcConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
## <a name="connecting-to-an-oracle-data-source"></a>Oracle データ ソースへの接続  
 Oracle 用の .NET Framework Data Provider は、 **OracleConnection**オブジェクトを使用して oracle データソースへの接続を提供します。  
  
 .NET Framework Data Provider for Oracle で使用される接続文字列フォーマットは、できるだけ MSDAORA (OLE DB Provider for Oracle) の接続文字列フォーマットと一致するようにデザインされています。 **OracleConnection**の詳細については、「 <xref:System.Data.OracleClient.OracleConnection>」を参照してください。  
  
 Oracle データ ソースへの接続を作成し確立する方法を次のサンプル コードに示します。  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OracleConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OracleConnection connection =   
  new OracleConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
OracleConnection nwindConn = new OracleConnection("Data Source=MyOracleServer;Integrated Security=yes;");  
nwindConn.Open();  
```  
  
## <a name="see-also"></a>関連項目

- [データ ソースへの接続](../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)
- [接続文字列](../../../../docs/framework/data/adonet/connection-strings.md)
- [OLE DB、ODBC、および Oracle 接続プール](../../../../docs/framework/data/adonet/ole-db-odbc-and-oracle-connection-pooling.md)
- [ADO.NET のマネージド プロバイダーと DataSet デベロッパー センター](https://go.microsoft.com/fwlink/?LinkId=217917)
