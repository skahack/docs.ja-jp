---
title: DbProviderFactory の取得
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a16e4a4d-6a5b-45db-8635-19570e4572ae
ms.openlocfilehash: dd4bca48c35b9b636a96fe5d4a724272abc4f71d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69934398"
---
# <a name="obtaining-a-dbproviderfactory"></a>DbProviderFactory の取得
<xref:System.Data.Common.DbProviderFactory> を取得する過程では、データ プロバイダーに関する情報が <xref:System.Data.Common.DbProviderFactories> クラスに渡されます。 <xref:System.Data.Common.DbProviderFactories.GetFactory%2A> メソッドはこの情報に基づいて、厳密に型指定されたプロバイダー ファクトリを作成します。 たとえば、<xref:System.Data.SqlClient.SqlClientFactory> を作成するには、`GetFactory` の引数にプロバイダー名 System.Data.SqlClient を文字列として指定します。 `GetFactory` には、<xref:System.Data.DataRow> を引数として受け取るオーバーロードも存在します。 プロバイダー ファクトリを作成すると、対応するメソッドを使って他のオブジェクトを作成できるようになります。 `SqlClientFactory` のメソッドには、<xref:System.Data.SqlClient.SqlClientFactory.CreateConnection%2A>、<xref:System.Data.SqlClient.SqlClientFactory.CreateCommand%2A>、<xref:System.Data.SqlClient.SqlClientFactory.CreateDataAdapter%2A> などがあります。  
  
> [!NOTE]
> 同様の機能は、.NET Framework の <xref:System.Data.OracleClient.OracleClientFactory> クラス、<xref:System.Data.Odbc.OdbcFactory> クラス、および <xref:System.Data.OleDb.OleDbFactory> クラスにも用意されています。  
  
## <a name="registering-dbproviderfactories"></a>DbProviderFactory の登録  
 ファクトリベースのクラスをサポートする各 .NET Framework データプロバイダーは、ローカルコンピューター上の**machine.config**ファイルの**DbProviderFactories**セクションに構成情報を登録します。 次の構成ファイル フラグメントは、<xref:System.Data.SqlClient> の構文と形式を示しています。  
  
```xml  
<system.data>  
  <DbProviderFactories>  
    <add name="SqlClient Data Provider"  
     invariant="System.Data.SqlClient"   
     description=".Net Framework Data Provider for SqlServer"   
     type="System.Data.SqlClient.SqlClientFactory, System.Data,   
     Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
    />  
  </DbProviderFactories>  
</system.data>  
```  
  
 **インバリアント**属性は、基になるデータプロバイダーを識別します。 この 3 つの部分から成る命名構文は、新しいファクトリを作成するときのほか、プロバイダー名とそれに関連付けられた接続文字列を実行時に取得できるようにするために、アプリケーションの構成ファイルでプロバイダーを指定するときにも使用されます。  
  
## <a name="retrieving-provider-information"></a>プロバイダー情報の取得  
 <xref:System.Data.Common.DbProviderFactories.GetFactoryClasses%2A> メソッドを使用すると、ローカル コンピューターにインストールされているすべてのデータ プロバイダーに関する情報を取得できます。 次の表<xref:System.Data.DataTable>で説明する列を含む、 **DbProviderFactories**という名前のを返します。  
  
|列の序数|列名|サンプルの出力|説明|  
|--------------------|-----------------|--------------------|-----------------|  
|0|**Name**|SqlClient Data Provider|データ プロバイダーの読み取り可能な名前|  
|1|**説明**|.Net Framework Data Provider for SqlServer|データ プロバイダーの読み取り可能な説明|  
|2|**InvariantName**|System.Data.SqlClient|プログラムでデータ プロバイダーの参照に使用できる名前|  
|3|**AssemblyQualifiedName**|System.Data.SqlClient.SqlClientFactory, System.Data, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089|オブジェクトをインスタンス化するための十分な情報を保持している、ファクトリ クラスの完全修飾名|  
  
 この `DataTable` を使用して、ユーザーに実行時に <xref:System.Data.DataRow> を選択してもらうことができます。 次に、選択された `DataRow` を <xref:System.Data.Common.DbProviderFactories.GetFactory%2A> メソッドに渡すことで、厳密に型指定された <xref:System.Data.Common.DbProviderFactory> を作成できます。 選択された <xref:System.Data.DataRow> を `GetFactory` メソッドに渡すことによって、目的の `DbProviderFactory` オブジェクトを作成できます。  
  
## <a name="listing-the-installed-provider-factory-classes"></a>インストールされているプロバイダー ファクトリ クラスの一覧表示  
 次の例では、インストールされているプロバイダーの情報を含んだ <xref:System.Data.Common.DbProviderFactories.GetFactoryClasses%2A> を、<xref:System.Data.DataTable> メソッドを使用して取得します。 このコードは、`DataTable` 内の各行を反復処理しながら、インストールされている各プロバイダーの情報をコンソール ウィンドウに表示します。  
  
 [!code-csharp[DataWorks DbProviderFactories#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DbProviderFactories/CS/source.cs#1)]
 [!code-vb[DataWorks DbProviderFactories#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DbProviderFactories/VB/source.vb#1)]  
  
## <a name="using-application-configuration-files-to-store-factory-information"></a>アプリケーション構成ファイルを使用したファクトリ情報の保存  
 ファクトリを操作するために使用されるデザインパターンでは、プロバイダーと接続文字列の情報をアプリケーション構成ファイルに格納することがあります。たとえば、Windows アプリケーションの場合は app.config、ASP.NET アプリケーションの場合は web.config です。  
  
 次の構成ファイル フラグメントは、2 つの名前付き接続文字列 (SQL Server の Northwind データベースに接続するための "NorthwindSQL" と、Access/Jet の Northwind データベースに接続するための "NorthwindAccess") を保存する例を示したものです。 この**不変**名は、 **providerName**属性に使用されます。  
  
```xml  
<configuration>  
  <connectionStrings>  
    <clear/>  
    <add name="NorthwindSQL"   
     providerName="System.Data.SqlClient"   
     connectionString=  
     "Data Source=MSSQL1;Initial Catalog=Northwind;Integrated Security=true"  
    />  
  
    <add name="NorthwindAccess"   
     providerName="System.Data.OleDb"   
     connectionString=  
     "Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Data\Northwind.mdb;"  
    />  
  </connectionStrings>  
</configuration>  
```  
  
### <a name="retrieving-a-connection-string-by-provider-name"></a>プロバイダー名による接続文字列の取得  
 プロバイダー ファクトリを作成するには、プロバイダー名だけでなく接続文字列も指定する必要があります。 この例では、プロバイダー名を "system.string" というインバリアント形式で渡すことによって、アプリケーション構成ファイルから接続文字列を取得する方法を示します。 このコードでは、<xref:System.Configuration.ConnectionStringSettingsCollection> を反復処理しています。 成功した場合には <xref:System.Configuration.ConnectionStringSettings.ProviderName%2A> が、それ以外の場合は `null` (Visual Basic の場合は `Nothing`) が返されます。 プロバイダーに複数のエントリが存在した場合は、最初に見つかったエントリが返されます。 構成ファイルから接続文字列を取得する方法の詳細と例については、「[接続文字列と構成ファイル](../../../../docs/framework/data/adonet/connection-strings-and-configuration-files.md)」を参照してください。  
  
> [!NOTE]
> このコードを実行するには、`System.Configuration.dll` を参照設定する必要があります。  
  
 [!code-csharp[DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider/CS/source.cs#1)]
 [!code-vb[DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider/VB/source.vb#1)]  
  
## <a name="creating-the-dbproviderfactory-and-dbconnection"></a>DbProviderFactory および DbConnection の作成  
 この例では、"system.string <xref:System.Data.Common.DbProviderFactory> " <xref:System.Data.Common.DbConnection>形式のプロバイダー名と接続文字列を渡して、オブジェクトとオブジェクトを作成する方法を示します。 成功した場合には `DbConnection` オブジェクトが返されます。エラーが発生した場合は `null` (Visual Basic の場合は `Nothing`) が返されます。  
  
 このコードでは、`DbProviderFactory` を呼び出すことによって <xref:System.Data.Common.DbProviderFactories.GetFactory%2A> を取得しています。 次に、<xref:System.Data.Common.DbProviderFactory.CreateConnection%2A> メソッドで <xref:System.Data.Common.DbConnection> オブジェクトを作成し、<xref:System.Data.Common.DbConnection.ConnectionString%2A> プロパティに接続文字列を設定します。  
  
 [!code-csharp[DataWorks DbProviderFactories.GetFactory#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.GetFactory/CS/source.cs#1)]
 [!code-vb[DataWorks DbProviderFactories.GetFactory#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.GetFactory/VB/source.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [DbProviderFactories](../../../../docs/framework/data/adonet/dbproviderfactories.md)
- [接続文字列](../../../../docs/framework/data/adonet/connection-strings.md)
- [構成クラスの使用](https://docs.microsoft.com/previous-versions/aspnet/ms228063(v=vs.100))
- [ADO.NET の概要](ado-net-overview.md)
