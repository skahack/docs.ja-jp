---
title: 非ジェネリックの ParallelForEach
ms.date: 03/30/2017
ms.assetid: de17e7a2-257b-48b3-91a1-860e2e9bf6e6
ms.openlocfilehash: 52b851686ea2fdc8c573a0622fe91ca5e205edeb
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65637736"
---
# <a name="non-generic-parallelforeach"></a>非ジェネリックの ParallelForEach

[!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] のツールボックスには、制御フロー アクティビティのセットが用意されています。これには、<xref:System.Activities.Statements.ParallelForEach%601> コレクションを反復処理できる <xref:System.Collections.Generic.IEnumerable%601> が含まれています。

<xref:System.Activities.Statements.ParallelForEach%601> 必要があります、<xref:System.Activities.Statements.ParallelForEach%601.Values%2A>プロパティの型を<xref:System.Collections.Generic.IEnumerable%601>します。 このため、ユーザーは、<xref:System.Collections.Generic.IEnumerable%601> インターフェイス (<xref:System.Collections.ArrayList> など) を実装するデータ構造を反復処理できません。 <xref:System.Activities.Statements.ParallelForEach%601> の非ジェネリック バージョンにはこの要件はありませんが、コレクション内の値の型の互換性を確保するために実行時の複雑さが増します。

このサンプルでは、非ジェネリックの <xref:System.Activities.Statements.ParallelForEach%601> アクティビティとそのデザイナーを実装する方法を示します。 このアクティビティは、<xref:System.Collections.ArrayList> の反復処理に使用できます。

## <a name="parallelforeach-activity"></a>ParallelForEach アクティビティ

C# および VB の `foreach` ステートメントは、コレクションの要素を列挙し、コレクションの各要素に対して埋め込みステートメントを実行します。 このステートメントに相当する [!INCLUDE[wf1](../../../../includes/wf1-md.md)] のアクティビティは、<xref:System.Activities.Statements.ForEach%601> および <xref:System.Activities.Statements.ParallelForEach%601> です。 <xref:System.Activities.Statements.ForEach%601> アクティビティには、値のリストと本体が含まれます。 実行時に、リストが反復処理されて、リスト内の値ごとに本体が実行されます。

<xref:System.Activities.Statements.ParallelForEach%601> には <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> があります。そのため、<xref:System.Activities.Statements.ParallelForEach%601> の評価が <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> を返した場合、`true` アクティビティは早期に完了することがあります。 <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> は、各イテレーションの完了後に評価されます。

ほとんどの場合、ジェネリック バージョンのアクティビティを使用することをお勧めします。ジェネリック バージョンのアクティビティは、そのアクティビティを使用するシナリオの大半に対応し、コンパイル時の型チェックを提供するためです。 非ジェネリック バージョンは、非ジェネリックの <xref:System.Collections.IEnumerable> インターフェイスを実装する型を反復処理するために使用できます。

## <a name="class-definition"></a>クラスの定義

次のコード例は、非ジェネリックの `ParallelForEach` アクティビティの定義を示しています。

```csharp
[ContentProperty("Body")]
public class ParallelForEach : NativeActivity
{
    [RequiredArgument]
    [DefaultValue(null)]
    InArgument<IEnumerable> Values { get; set; }

    [DefaultValue(null)]
    [DependsOn("Values")]
    public Activity<bool> CompletionCondition
    [DefaultValue(null)]
    [DependsOn("CompletionCondition")]
    ActivityAction<object> Body { get; set; }
}
```

Body (省略可能) \
コレクション内の要素ごとに実行される <xref:System.Activities.ActivityAction> 型の <xref:System.Object>。 各要素は、Argument プロパティを使用して Body に渡されます。

値 (省略可能) \
反復処理される要素のコレクション。 コレクションのすべての要素の型が互換性のある型であることが実行時に確認されます。

CompletionCondition (省略可能) \
<xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> プロパティは、イテレーションの完了後に評価されます。 `true` であると評価する場合、スケジュールされた保留イテレーションはキャンセルされます。 このプロパティが設定されていない場合、分岐コレクション内のすべてのアクティビティは完了するまで実行されます。

## <a name="example-of-using-parallelforeach"></a>ParallelForEach の使用例

アプリケーションでの ParallelForEach アクティビティの使用方法を次のコードに示します。

```csharp
string[] names = { "bill", "steve", "ray" };

DelegateInArgument<object> iterationVariable = new DelegateInArgument<object>() { Name = "iterationVariable" };

Activity sampleUsage =
    new ParallelForEach
    {
       Values = new InArgument<IEnumerable>(c=> names),
       Body = new ActivityAction<object>
       {
           Argument = iterationVariable,
           Handler = new WriteLine
           {
               Text = new InArgument<string>(env => string.Format("Hello {0}",                                                               iterationVariable.Get(env)))
           }
       }
   };
```

## <a name="parallelforeach-designer"></a>ParallelForEach デザイナー

サンプルのアクティビティ デザイナーは、組み込みの <xref:System.Activities.Statements.ParallelForEach%601> アクティビティ用に提供されているデザイナーに外観が似ています。 ツールボックス、デザイナーが表示されます、**サンプル**、**非ジェネリック アクティビティ**カテゴリ。 デザイナーの名前は**ParallelForEachWithBodyFactory**ツールボックスで、活動が公開するため、<xref:System.Activities.Presentation.IActivityTemplateFactory>で適切に構成されたアクティビティを作成するツールボックス<xref:System.Activities.ActivityAction>。

```csharp
public sealed class ParallelForEachWithBodyFactory : IActivityTemplateFactory
{
    public Activity Create(DependencyObject target)
    {
        return new Microsoft.Samples.Activities.Statements.ParallelForEach()
        {
            Body = new ActivityAction<object>()
            {
                Argument = new DelegateInArgument<object>()
                {
                    Name = "item"
                }
            }
        };
    }
}
```

## <a name="to-run-the-sample"></a>サンプルを実行するには

1. 選択したプロジェクトをソリューションのスタートアップ プロジェクトに設定します。

    1. **CodeTestClient**コードを使用して、アクティビティを使用する方法を示しています。

    2. **DesignerTestClient**デザイナー内でアクティビティを使用する方法を示しています。

2. プロジェクトをビルドして実行します。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> このディレクトリが存在しない場合に移動[Windows Communication Foundation (WCF) と .NET Framework 4 向けの Windows Workflow Foundation (WF) サンプル](https://go.microsoft.com/fwlink/?LinkId=150780)すべて Windows Communication Foundation (WCF) をダウンロードして[!INCLUDE[wf1](../../../../includes/wf1-md.md)]サンプル。 このサンプルは、次のディレクトリに格納されます。
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\NonGenericParallelForEach`
