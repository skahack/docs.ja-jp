---
title: 属性ベースの対応付け
ms.date: 03/30/2017
ms.assetid: 6dd89999-f415-4d61-b8c8-237d23d7924e
ms.openlocfilehash: 41152aa81ab84a2ab77e9a4ebf16e102ee5c0e3f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964095"
---
# <a name="attribute-based-mapping"></a>属性ベースの対応付け
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]属性を適用するか、 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]または外部マッピングファイルを使用して、SQL Server データベースをオブジェクトモデルにマップします。 このトピックでは、属性ベースの方法について説明します。  
  
 大部分の基本フォームでは、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、データベースと <xref:System.Data.Linq.DataContext>、テーブルとクラス、列およびリレーションシップとそのクラスのプロパティを、それぞれ対応付けています。 属性を使用して、オブジェクト モデル内の継承階層を対応付けることもできます。 詳細については、「[方法 :Visual Basic またはC# ](../../../../../../docs/framework/data/adonet/sql/linq/how-to-generate-the-object-model-in-visual-basic-or-csharp.md)でオブジェクトモデルを生成します。  
  
 Visual Studio を使用する開発者は、通常、オブジェクトリレーショナルデザイナーを使用して属性ベースの対応付けを実行します。 また、SQLMetal コマンド ライン ツールを使用したり、自分で属性をハンド コードしたりすることもできます。 詳細については、「[方法 :Visual Basic またはC# ](../../../../../../docs/framework/data/adonet/sql/linq/how-to-generate-the-object-model-in-visual-basic-or-csharp.md)でオブジェクトモデルを生成します。  
  
> [!NOTE]
> 外部 XML ファイルを使用して対応付けることもできます。 詳細については、「[外部マッピング](../../../../../../docs/framework/data/adonet/sql/linq/external-mapping.md)」を参照してください。  
  
 以下のセクションでは、属性ベースの対応付けについて詳しく説明します。 詳細については、「<xref:System.Data.Linq.Mapping>」を参照してください。  
  
## <a name="databaseattribute-attribute"></a>DatabaseAttribute 属性  
 この属性は、接続によってデータベースの名前が提供されない場合に、データベースの既定の名前を指定するために使用します。 この属性は省略可能ですが、この属性を使用する場合は、次の表に示されているように、<xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A> プロパティを適用する必要があります。  
  
|プロパティ|種類|既定値|説明|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A>|String|「<xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A>」を参照してください。|<xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A> プロパティを使用して、データベースの名前を指定します。|  
  
 詳細については、「<xref:System.Data.Linq.Mapping.DatabaseAttribute>」を参照してください。  
  
## <a name="tableattribute-attribute"></a>TableAttribute 属性  
 この属性は、クラスを、データベース テーブルまたはビューに関連付けられたエンティティ クラスとして指定するために使用します。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、この属性を持つクラスを、永続的なクラスとして扱います。 次の表は、<xref:System.Data.Linq.Mapping.TableAttribute.Name%2A> プロパティについての説明です。  
  
|プロパティ|種類|既定値|説明|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.TableAttribute.Name%2A>|String|クラス名と同じ文字列|クラスを、データベース テーブルに関連付けられたエンティティ クラスとして指定します。|  
  
 詳細については、「<xref:System.Data.Linq.Mapping.TableAttribute>」を参照してください。  
  
## <a name="columnattribute-attribute"></a>ColumnAttribute 属性  
 この属性は、データベース テーブルの列を表すエンティティ クラスのメンバーを指定するために使用します。 この属性は、フィールドまたはプロパティに適用できます。  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] がデータベースへの変更を保存すると、列として指定したメンバーのみが取得および保持されます。 この属性を持たないメンバーは非永続的であると見なされ、挿入や更新の場合に送信されません。  
  
 この属性のプロパティを次の表に示します。  
  
|プロパティ|種類|既定値|説明|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A>|AutoSync|Never|共通言語ランタイム (CLR) に対して、挿入または更新操作の後に値を取得することを指示します。<br /><br /> オプション:Always、Never、OnUpdate、OnInsert。|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.CanBeNull%2A>|ブール型|`true`|列に null 値を含めることができることを示します。|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A>|String|推論によるデータベース列型|データベースの型と修飾子を使用して、データベース列の型を指定します。|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.Expression%2A>|String|Empty|データベースの計算列を定義します。|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A>|Boolean|`false`|データベースが自動生成する値が、列に含まれることを示します。|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.IsDiscriminator%2A>|Boolean|`false`|[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 継承階層の識別子の値が列に含まれることを示します。|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A>|Boolean|`false`|このクラス メンバーが、テーブルの主キーの列、または主キーの一部である列を表すことを指定します。|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A>|Boolean|`false`|メンバーの列の型を、データベースのタイムスタンプまたはバージョン番号として指定します。|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A>|UpdateCheck|`Always` (メンバーの <xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A> が `true` の場合は除く)|[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] がオプティミスティック同時実行競合を検出する方法を指定します。|  
  
 詳細については、「<xref:System.Data.Linq.Mapping.ColumnAttribute>」を参照してください。  
  
> [!NOTE]
> AssociationAttribute プロパティ値と ColumnAttribute Storage プロパティ値では大文字と小文字が区別されます。 たとえば、AssociationAttribute.Storage  プロパティの属性に使用されている値は、コード内の別の場所で使用されている対応するプロパティ名と、大文字と小文字が一致するようにしてください。 これは、Visual Basic など、通常は大文字と小文字が区別されないすべての .NET プログラミング言語に適用されます。 Storage プロパティの詳細については、「<xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A?displayProperty=nameWithType>」を参照してください。  
  
## <a name="associationattribute-attribute"></a>AssociationAttribute 属性  
 この属性は、外部キーと主キーのリレーションシップなど、データベース内の関連付けを表すプロパティを指定するために使用します。 リレーションシップの詳細については[、「」を参照してください。データベース リレーションシップを割り当てる](../../../../../../docs/framework/data/adonet/sql/linq/how-to-map-database-relationships.md)」をご覧ください。  
  
 この属性のプロパティを次の表に示します。  
  
|プロパティ|種類|既定値|説明|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.DeleteOnNull%2A>|Boolean|`false`|外部キー メンバーがすべて null 非許容の関連付けの場合、関連付けが null に設定されるとオブジェクトを削除します。|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.DeleteRule%2A>|String|なし|関連付けに削除の動作を追加します。|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.IsForeignKey%2A>|Boolean|`false`|true の場合、データベースのリレーションシップを表す関連付けの中で、メンバーを外部キーとして指定します。|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.IsUnique%2A>|Boolean|`false`|true の場合、外部キーの一意性の制約を示します。|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.OtherKey%2A>|String|関連クラスの ID|ターゲット エンティティ クラスの 1 つ以上のメンバーを、関連付けの他方の側のキー値として指定します。|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.ThisKey%2A>|String|包含クラスの ID|関連付けのこちら側のキー値を表す、このエンティティ クラスのメンバーを指定します。|  
  
 詳細については、「<xref:System.Data.Linq.Mapping.AssociationAttribute>」を参照してください。  
  
> [!NOTE]
> AssociationAttribute プロパティ値と ColumnAttribute Storage プロパティ値では大文字と小文字が区別されます。 たとえば、AssociationAttribute.Storage  プロパティの属性に使用されている値は、コード内の別の場所で使用されている対応するプロパティ名と、大文字と小文字が一致するようにしてください。 これは、Visual Basic など、通常は大文字と小文字が区別されないすべての .NET プログラミング言語に適用されます。 Storage プロパティの詳細については、「<xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A?displayProperty=nameWithType>」を参照してください。  
  
## <a name="inheritancemappingattribute-attribute"></a>InheritanceMappingAttribute 属性  
 この属性は、継承階層を対応付けるために使用します。  
  
 この属性のプロパティを次の表に示します。  
  
|プロパティ|種類|既定値|説明|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.InheritanceMappingAttribute.Code%2A>|String|なし。 値を指定する必要があります。|識別子のコード値を指定します。|  
|<xref:System.Data.Linq.Mapping.InheritanceMappingAttribute.IsDefault%2A>|Boolean|`false`|true の場合、ストア内の識別子の値が、指定された値に一致しないときは、この型のオブジェクトをインスタンス化します。|  
|<xref:System.Data.Linq.Mapping.InheritanceMappingAttribute.Type%2A>|種類|なし。 値を指定する必要があります。|階層内のクラスの型を指定します。|  
  
 詳細については、「<xref:System.Data.Linq.Mapping.InheritanceMappingAttribute>」を参照してください。  
  
## <a name="functionattribute-attribute"></a>FunctionAttribute 属性  
 この属性は、データベース内のストアド プロシージャまたはユーザー定義関数として表すメソッドを指定するために使用します。  
  
 この属性のプロパティを次の表に示します。  
  
|プロパティ|種類|既定値|説明|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.FunctionAttribute.IsComposable%2A>|Boolean|`false`|false の場合、ストアド プロシージャへの対応付けを表します。 true の場合、ユーザー定義関数への対応付けを表します。|  
|<xref:System.Data.Linq.Mapping.FunctionAttribute.Name%2A>|String|データベース内の名前と同じ文字列|ストアド プロシージャまたはユーザー定義関数の名前を指定します。|  
  
 詳細については、「<xref:System.Data.Linq.Mapping.FunctionAttribute>」を参照してください。  
  
## <a name="parameterattribute-attribute"></a>ParameterAttribute 属性  
 この属性は、ストアド プロシージャ メソッドの入力パラメーターを対応付けるために使用します。  
  
 この属性のプロパティを次の表に示します。  
  
|プロパティ|種類|既定値|説明|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.ParameterAttribute.DbType%2A>|String|なし|データベースの型を指定します。|  
|<xref:System.Data.Linq.Mapping.ParameterAttribute.Name%2A>|String|データベース内のパラメーター名と同じ文字列|パラメーターの名前を指定します。|  
  
 詳細については、「<xref:System.Data.Linq.Mapping.ParameterAttribute>」を参照してください。  
  
## <a name="resulttypeattribute-attribute"></a>ResultTypeAttribute 属性  
 この属性は、結果の型を指定するために使用します。  
  
 この属性のプロパティを次の表に示します。  
  
|プロパティ|種類|既定値|説明|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.ResultTypeAttribute.Type%2A>|種類|(なし)|<xref:System.Data.Linq.IMultipleResults> を返すストアド プロシージャに対応付けられているメソッドで使用します。 ストアド プロシージャの有効な型マッピングまたは期待される型マッピングを宣言します。|  
  
 詳細については、「<xref:System.Data.Linq.Mapping.ResultTypeAttribute>」を参照してください。  
  
## <a name="dataattribute-attribute"></a>DataAttribute 属性  
 この属性は、名前およびプライベート ストレージ フィールドを指定するために使用します。  
  
 この属性のプロパティを次の表に示します。  
  
|プロパティ|種類|既定値|説明|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.DataAttribute.Name%2A>|String|データベース内の名前と同じ|テーブル、列などの名前を指定します。|  
|<xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A>|String|パブリック アクセサー|基になるストレージ フィールドの名前を指定します。|  
  
 詳細については、「 <xref:System.Data.Linq.Mapping.DataAttribute> 」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [参照](../../../../../../docs/framework/data/adonet/sql/linq/reference.md)
