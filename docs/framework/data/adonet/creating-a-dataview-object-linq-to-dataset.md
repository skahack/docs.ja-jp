---
title: DataView オブジェクトの作成 (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 76057508-e12d-4779-a707-06a4c2568acf
ms.openlocfilehash: afa760d890cf2857737372af5a9d3ba7c2749e6c
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69949419"
---
# <a name="creating-a-dataview-object-linq-to-dataset"></a>DataView オブジェクトの作成 (LINQ to DataSet)
LINQ to DataSet コンテキストでを作成するに<xref:System.Data.DataView>は、次の2つの方法があります。 を使用して<xref:System.Data.DataView> LINQ to DataSet クエリ<xref:System.Data.DataTable>からを作成することも、型指定されたまたは型指定<xref:System.Data.DataTable>されていないから作成することもできます。 どちらの場合も、 <xref:System.Data.DataView> <xref:System.Data.DataTableExtensions.AsDataView%2A>拡張メソッドのいずれかを使用してを作成します。<xref:System.Data.DataView>は、LINQ to DataSet コンテキストで直接構築することはできません。  
  
 <xref:System.Data.DataView> を作成した後に、Windows フォーム アプリケーションまたは ASP.NET アプリケーションの UI コントロールにバインドしたり、フィルターおよび並べ替えの設定を変更したりできます。  
  
 <xref:System.Data.DataView> は、インデックスを構築します。これにより、フィルター処理や並べ替えなど、インデックスを使用できる操作のパフォーマンスが大幅に向上します。 <xref:System.Data.DataView> のインデックスは、<xref:System.Data.DataView> の作成時に構築されるほか、並べ替えまたはフィルター処理の情報が変更されたときにも構築されます。 <xref:System.Data.DataView> を作成した後で、並べ替えまたはフィルター処理の情報を設定した場合、インデックスが最低でも 2 回 (<xref:System.Data.DataView> の作成時と、並べ替えまたはフィルターのプロパティの変更時) 構築されることになります。  
  
 を使用した<xref:System.Data.DataView>フィルター処理と並べ替えの詳細については、「 [dataview によるフィルター処理](../../../../docs/framework/data/adonet/filtering-with-dataview-linq-to-dataset.md)」と「 [dataview による並べ替え](../../../../docs/framework/data/adonet/sorting-with-dataview-linq-to-dataset.md)」を参照してください。  
  
## <a name="creating-dataview-from-a-linq-to-dataset-query"></a>LINQ to DataSet クエリの結果からの DataView の作成  
 オブジェクトは、LINQ to DataSet クエリの結果から作成できます。この場合、結果はオブジェクトの<xref:System.Data.DataRow>射影になります。 <xref:System.Data.DataView> 新しく作成される <xref:System.Data.DataView> は、その基となるクエリからのフィルター処理および並べ替え情報を継承します。  
  
> [!NOTE]
> ほとんどの場合、フィルターに使用する式は、副作用のない確定的な式である必要があります。 また、並べ替えおよびフィルター処理は任意の回数実行されるため、特定の実行回数に依存するロジックが式に含まれないようにしてください。  
  
 匿名型を返すクエリまたは結合操作を実行するクエリからの <xref:System.Data.DataView> の作成はサポートされていません。  
  
 <xref:System.Data.DataView> の作成に使用されるクエリでは、次のクエリ演算子のみがサポートされます。  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.Cast%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.OrderBy%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.OrderByDescending%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.Select%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.ThenBy%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.ThenByDescending%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.Where%2A>  
  
 <xref:System.Data.DataView> LINQtoDataSet<xref:System.Data.EnumerableRowCollectionExtensions.Select%2A>クエリからを作成する場合、メソッドは、クエリで呼び出される最後のメソッドである必要があることに注意してください。 これを次の例に示します。この例<xref:System.Data.DataView>では、合計期限によって並べ替えられたオンライン注文のを作成しています。  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQuery1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromquery1)]
 [!code-vb[DP DataView Samples#CreateLDVFromQuery1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromquery1)]  
  
 また、文字列ベース<xref:System.Data.DataView.RowFilter%2A>のプロパティと<xref:System.Data.DataView.Sort%2A>プロパティを使用して、クエリから<xref:System.Data.DataView>作成されたをフィルター処理したり並べ替えたりすることもできます。 この操作を行うと、クエリから継承された並べ替えおよびフィルター情報がクリアされます。 次の例では<xref:System.Data.DataView> 、' ' で始まる姓によってフィルター処理する LINQ to DataSet クエリからを作成します。 文字列ベースの <xref:System.Data.DataView.Sort%2A> プロパティは、姓を昇順に並べ替え、名を降順に並べ替えるように設定されています。  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromquerystringsort)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromquerystringsort)]  
  
## <a name="creating-a-dataview-from-a-datatable"></a>DataTable からの DataView の作成  
 LINQ to DataSet クエリから作成されるだけでなく、 <xref:System.Data.DataView> <xref:System.Data.DataTableExtensions.AsDataView%2A>メソッドを使用し<xref:System.Data.DataTable>てからオブジェクトを作成することもできます。  
  
 次の例では、<xref:System.Data.DataView> を SalesOrderDetail テーブルから作成した後、<xref:System.Windows.Forms.BindingSource> オブジェクトのデータ ソースとして設定します。 このオブジェクトは、<xref:System.Windows.Forms.DataGridView> コントロールのプロキシとして動作します。  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromTable](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromtable)]
 [!code-vb[DP DataView Samples#CreateLDVFromTable](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromtable)]  
  
 <xref:System.Data.DataView> から <xref:System.Data.DataTable> を作成した後、フィルターおよび並べ替えを設定できます。 次の例では、<xref:System.Data.DataView> を Contact テーブルから作成した後、姓を昇順に並べ替え、名を降順に並べ替えるための <xref:System.Data.DataView.Sort%2A> プロパティを設定します。  
  
 [!code-csharp[DP DataView Samples#LDVStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvstringsort)]
 [!code-vb[DP DataView Samples#LDVStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvstringsort)]  
  
 ただし、<xref:System.Data.DataView.RowFilter%2A> をクエリから作成した後に <xref:System.Data.DataView.Sort%2A> プロパティまたは <xref:System.Data.DataView> プロパティを設定する操作を行うと、パフォーマンスが低下します。なぜなら、<xref:System.Data.DataView> により、フィルター処理および並べ替え処理をサポートするためのインデックスが構築されるからです。 <xref:System.Data.DataView.RowFilter%2A> プロパティまたは <xref:System.Data.DataView.Sort%2A> プロパティを設定すると、データのインデックスが再構築され、アプリケーションのオーバーヘッドが増加してパフォーマンスの低下を招きます。 可能な場合は、<xref:System.Data.DataView> を最初に作成するときにフィルター処理および並べ替え情報を指定して、後で情報を変更するのを避けてください。  
  
## <a name="see-also"></a>関連項目

- [データ バインディングと LINQ to DataSet](../../../../docs/framework/data/adonet/data-binding-and-linq-to-dataset.md)
- [DataView によるフィルター処理](../../../../docs/framework/data/adonet/filtering-with-dataview-linq-to-dataset.md)
- [DataView による並べ替え](../../../../docs/framework/data/adonet/sorting-with-dataview-linq-to-dataset.md)
