---
title: RaiseEvent ステートメント (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.RaiseEventMethod
- vb.RaiseEvent
- RaiseEvent
helpviewer_keywords:
- raising events [Visual Basic], RaiseEvent statement
- RaiseEvent statement [Visual Basic]
- event handlers, connecting events to
ms.assetid: f82e380a-1e6b-4047-bea8-c853f4d2c742
ms.openlocfilehash: ee52b4adf893ea0926c4016fcb6a89d0010ee6ad
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69957781"
---
# <a name="raiseevent-statement"></a>RaiseEvent ステートメント
クラス、フォーム、またはドキュメント内のモジュールレベルで宣言されたイベントをトリガーします。  
  
## <a name="syntax"></a>構文  
  
```  
RaiseEvent eventname[( argumentlist )]  
```  
  
## <a name="parts"></a>指定項目  
 `eventname`  
 必須。 トリガーするイベントの名前。  
  
 `argumentlist`  
 省略可能です。 変数、配列、または式のコンマ区切りの一覧。 引数`argumentlist`はかっこで囲む必要があります。 引数がない場合は、かっこを省略する必要があります。  
  
## <a name="remarks"></a>Remarks  
 必須`eventname`のは、モジュール内で宣言されたイベントの名前です。 Visual Basic 変数の名前付け規則に従います。  
  
 イベントが発生したモジュール内でイベントが宣言されていない場合は、エラーが発生します。 次のコードフラグメントは、イベントの宣言と、イベントが発生するプロシージャを示しています。  
  
 [!code-vb[VbVbalrEvents#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#37)]  
  
 を使用`RaiseEvent`して、モジュールで明示的に宣言されていないイベントを発生させることはできません。 たとえば、すべてのフォームがから<xref:System.Windows.Forms.Control.Click> <xref:System.Windows.Forms.Form?displayProperty=nameWithType>イベントを継承する場合、派生フォーム`RaiseEvent`でを使用してを生成することはできません。 フォームモジュールでイベント`Click`を宣言すると、フォーム独自<xref:System.Windows.Forms.Control.Click>のイベントがシャドウされます。 メソッドを<xref:System.Windows.Forms.Control.Click> <xref:System.Windows.Forms.Control.OnClick%2A>呼び出すことによって、フォームのイベントを呼び出すこともできます。  
  
 既定では、Visual Basic で定義されたイベントによって、接続が確立された順序でイベントハンドラーが発生します。 イベントにはパラメーター `ByRef`を含めることができるため、遅延を接続するプロセスは、以前のイベントハンドラーによって変更されたパラメーターを受け取る場合があります。 イベントハンドラーが実行されると、イベントを発生させたサブルーチンに制御が返されます。  
  
> [!NOTE]
> 共有されていないイベントは、宣言されているクラスのコンストラクター内では発生しません。 このようなイベントでは実行時エラーは発生しませんが、関連するイベントハンドラーによってキャッチされない場合があります。 コンストラクターから`Shared`イベントを発生させる必要がある場合は、修飾子を使用して共有イベントを作成します。  
  
> [!NOTE]
> イベントの既定の動作を変更するには、カスタムイベントを定義します。 カスタムイベントの場合、 `RaiseEvent`ステートメントは、イベントの`RaiseEvent`アクセサーを呼び出します。 カスタムイベントの詳細については、「 [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、イベントを使用して 10 秒から 0 秒までカウント ダウンします。 このコードは、 `RaiseEvent`ステートメントなど、イベント関連のメソッド、プロパティ、およびステートメントのいくつかを示しています。  
  
 イベントを発生させるクラスをイベント ソース、イベントを処理するメソッドをイベント ハンドラーと呼びます。 イベント ソースでは、生成されるイベントに対して複数のイベント ハンドラーを設定できます。 クラスでイベントが発生すると、そのイベントは、オブジェクトのインスタンスに対するイベントを処理するために選択されたすべてのクラスで発生します。  
  
 また、この例では、ボタン (`Button1`) とテキスト ボックス (`TextBox1`) を含んだフォーム (`Form1`) も使用しています。 ボタンをクリックすると、1 つ目のテキスト ボックスに 10 秒から 0 秒までのカウントダウンが表示されます。 カウントダウンが終わると (10 秒が経過すると)、1 つ目のテキスト ボックスに "Done" と表示されます。  
  
 `Form1` のコードでは、フォームの初期状態と終了状態を指定しています。 イベント発生時に実行されるコードも含まれています。  
  
 この例を使用するには、新しい Windows アプリケーションプロジェクトを開き、 `Button1`という名前のボタンとという名前のテキスト`TextBox1`ボックス`Form1`をメインフォームに追加します。 次に、フォームを右クリックし、 **[コードの表示]** をクリックしてコードエディターを開きます。  
  
 クラスの宣言セクションに変数を`WithEvents`追加します。 `Form1`  
  
 [!code-vb[VbVbalrEvents#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#14)]  
  
## <a name="example"></a>例  
 `Form1` のコードに次のコードを追加します。 `Form_Load` 、、など、存在する可能性のある重複するプロシージャ`Button_Click`を置き換えます。  
  
 [!code-vb[VbVbalrEvents#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#15)]  
  
 F5 キーを押して前の例を実行し、 **[Start]** というラベルのボタンをクリックします。 最初のテキスト ボックスで、秒のカウント ダウンが開始されます。 カウントダウンが終わると (10 秒が経過すると)、1 つ目のテキスト ボックスに "Done" と表示されます。  
  
> [!NOTE]
> `My.Application.DoEvents`メソッドは、フォームとまったく同じ方法でイベントを処理しません。 フォームがイベントを直接処理できるようにするには、マルチスレッドを使用します。 詳細については、「[マネージスレッド処理](../../../standard/threading/index.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [イベント](../../../visual-basic/programming-guide/language-features/events/index.md)
- [Event ステートメント](../../../visual-basic/language-reference/statements/event-statement.md)
- [AddHandler ステートメント](../../../visual-basic/language-reference/statements/addhandler-statement.md)
- [RemoveHandler ステートメント](../../../visual-basic/language-reference/statements/removehandler-statement.md)
- [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)
