---
title: SQL と CLR のカスタム型マッピング
ms.date: 03/30/2017
ms.assetid: d916c7fb-4b56-4214-acbe-5e23365047b2
ms.openlocfilehash: 5aff9a78349cbf9443c5b663a41d7c13a109e625
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69945053"
---
# <a name="sql-clr-custom-type-mappings"></a>SQL と CLR のカスタム型マッピング
SQL Server と共通言語ランタイム (CLR) 間の型マッピングは、SQLMetal コマンド ライン ツールのオブジェクト リレーショナル デザイナー (O/R デザイナー) を使用すると、自動的に指定されます。  
  
 カスタマイズしたマッピングが実行されない場合、これらのツールでは、「 [SQL CLR 型マッピング](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)」で説明されているように、既定の型マッピングが割り当てられます。 これらの既定とは異なる型マッピングを使用する場合は、型マッピングをカスタマイズする必要があります。  
  
 型マッピングをカスタマイズする場合は、中間の DBML ファイルに変更を加える方法が推奨されます。 次に、SQLMetal または O/R デザイナーでカスタマイズした DBML ファイルを使用して、コード ファイルとマッピング ファイルを作成します。  
  
 コード ファイルとマッピング ファイルから <xref:System.Data.Linq.DataContext> オブジェクトをインスタンス化すると、指定した型マッピングに従って <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> メソッドがデータベースを作成します。 マッピングに CLR の `type` 属性が指定されていない場合は、既定の型マッピングが使用されます。  
  
## <a name="customization-with-sqlmetal-or-or-designer"></a>SQLMetal または O/R デザイナーを使用したカスタマイズ  
 SQLMetal と O/R デザイナーを使用すると、コード ファイルの内外の型マッピング情報を含むオブジェクト ファイルを自動作成できます。 これらのファイルはマッピングを再作成するたびに SQLMetal または O/R デザイナーによって上書きされるため、カスタム型マッピングを指定する場合は DBML ファイルをカスタマイズする方法をお勧めします。  
  
 SQLMetal または O/R デザイナーで型マッピングをカスタマイズするには、最初に DBML ファイルを生成します。 次に、コード ファイルやマッピング ファイルを生成する前に、DBML ファイルを変更して適切な型マッピングを指定します。 SQLMetal では、DBML ファイルの `Type` 属性と `DbType` 属性を手動で変更して、型マッピングをカスタマイズする必要があります。 O/R デザイナーでは、デザイナー内で変更を加えることができます。 O/R デザイナーの使用方法の詳細については、「 [Visual Studio の LINQ to SQL ツール](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)」を参照してください。  
  
> [!NOTE]
> 一部の型マッピングでは、データベースに対する変換操作中にオーバーフローやデータ損失の例外が発生することがあります。 カスタマイズを行う前に、「 [SQL CLR 型マッピング](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)」の「型マッピングの実行時動作のマトリックス」をよく確認してください。  
  
 型マッピングのカスタマイズが SQLMetal または O/R デザイナーで認識されるためには、コード ファイルや外部のマッピング ファイルを生成するときに、必ずこれらのツールにカスタム DBML ファイルのパスを提供する必要があります。 型マッピングのカスタマイズでは必須ではありませんが、常に型マッピング情報をコード ファイルから分離し、外部の型マッピング ファイルを追加生成することをお勧めします。 コード ファイルの再コンパイルを要求しないことで、柔軟性を残しておくことができます。  
  
## <a name="incorporating-database-changes"></a>データベースの変更の組み込み  
 データベースを変更すると、DBML ファイルを更新して、これらの変更を反映する必要があります。 その 1 つの方法として、新しい DBML ファイルを自動作成してから型マッピングのカスタマイズをやり直します。 もう 1 つは、新しい DBML ファイルとカスタマイズした DBML ファイルを比較し、カスタム DBML ファイルを手動で更新してデータベースの変更を反映させる方法です。  
  
## <a name="see-also"></a>関連項目

- [SQL と CLR の型マッピング](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)
- [LINQ to SQL でのコード生成](../../../../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md)
