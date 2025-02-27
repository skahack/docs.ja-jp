---
title: '方法: シーケンシャル ワークフローの作成'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5280e816-ae17-48c4-8de0-a1e6895dd8f0
ms.openlocfilehash: 9c9746305b251e7d48ee34c2cccd5afae174ee90
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962367"
---
# <a name="how-to-create-a-sequential-workflow"></a>方法: シーケンシャル ワークフローの作成
ワークフローは、ビルトイン アクティビティおよびカスタム アクティビティから構築できます。 このトピックでは、 <xref:System.Activities.Statements.Sequence>アクティビティなどの組み込みアクティビティと、前[の手順のカスタムアクティビティの両方を使用するワークフローを作成する手順について説明します。アクティビティ](how-to-create-an-activity.md)のトピックを作成します。 このワークフローは、数値推測ゲームをモデル化しています。  
  
> [!NOTE]
> チュートリアル入門の各トピックは、前のトピックに応じて異なります。 このトピックを完了するには、まず[次の手順を完了する必要があります。アクティビティ](how-to-create-an-activity.md)を作成します。  
  
> [!NOTE]
> チュートリアルの完成版をダウンロードするには、「 [Windows Workflow Foundation (WF45) - Getting Started Tutorial (Windows Workflow Foundation (WF45) - チュートリアル入門)](https://go.microsoft.com/fwlink/?LinkID=248976)」を参照してください。  
  
## <a name="to-create-the-workflow"></a>ワークフローを作成するには  
  
1. **ソリューションエクスプローラー**で **[NumberGuessWorkflowActivities]** を右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。  
  
2. **[インストール済み]** の **[共通項目]** ノードで、 **[ワークフロー]** を選択します。 **[ワークフロー]** の一覧から **[アクティビティ]** を選択します。  
  
3. [ `SequentialNumberGuessWorkflow` **名前**] ボックスに「」と入力し、 **[追加]** をクリックします。  
  
4. **[ツールボックス]** の **[制御フロー]** セクションから**Sequence**アクティビティをドラッグし、ワークフローデザインサーフェイスの **[ここにアクティビティをドロップ]** ラベルの上にドロップします。  
  
## <a name="to-create-the-workflow-variables-and-arguments"></a>ワークフロー変数および引数を作成するには  
  
1. **ソリューションエクスプローラー**で**sequentialnumberguessworkflow.xaml**をダブルクリックして、ワークフローをデザイナーに表示します (まだ表示されていない場合)。  
  
2. ワークフローデザイナーの左下にある **[引数]** をクリックして、 **[引数]** ペインを表示します。  
  
3. **[引数の作成]** をクリックします。  
  
4. [ `MaxNumber` **名前**] ボックスに「」と入力し、 **[方向]** ドロップダウンリストから **[In]** を選択します。次に、 **[引数の型]** ドロップダウンリストから **[Int32]** を選択し、enter キーを押して引数を保存します。  
  
5. **[引数の作成]** をクリックします。  
  
6. 新しく`Turns`追加された引数の下にある [名前] ボックスに「」と入力し、[方向] ドロップダウンリストから [Out] を選択します。次に、[引数の型] ドロップダウンリストから [Int32] を選択し、enter キーを押します。 `MaxNumber`  
  
7. アクティビティデザイナーの左下にある **[引数]** をクリックして、 **[引数]** ペインを閉じます。  
  
8. ワークフローデザイナーの左下にある **[変数]** をクリックして、 **[変数]** ペインを表示します。  
  
9. **[変数の作成]** をクリックします。  
  
    > [!TIP]
    >  **[変数の作成]** ボックスが表示されない場合は、ワークフローデザイナー画面で**Sequence**アクティビティをクリックして選択します。  
  
10. [ `Guess` **名前**] ボックスに「」と入力し、 **[変数の型]** ドロップダウンリストから **[Int32]** を選択します。次に、enter キーを押して変数を保存します。  
  
11. **[変数の作成]** をクリックします。  
  
12. [ `Target` **名前**] ボックスに「」と入力し、 **[変数の型]** ドロップダウンリストから **[Int32]** を選択します。次に、enter キーを押して変数を保存します。  
  
13. アクティビティデザイナーの左下にある **[変数]** をクリックして、 **[変数]** ペインを閉じます。  
  
## <a name="to-add-the-workflow-activities"></a>ワークフロー アクティビティを追加するには  
  
1. **ツールボックス**の **[プリミティブ]** セクションから**Assign**アクティビティをドラッグし、 **Sequence**アクティビティにドロップします。 [ `Target` **To** ] ボックスに「」と入力し、[式の**入力C#**  ] または [ **VB の式を入力**してください] ボックスに次の式を入力します。  
  
    ```vb  
    New System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    ```csharp  
    new System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    > [!TIP]
    >  **[ツールボックス]** ウィンドウが表示されていない場合は、 **[表示]** メニューの **[ツールボックス]** を選択します。  
  
2. **ツールボックス**の **[制御フロー]** セクションから**dowhile**アクティビティをドラッグし、 **Assign**アクティビティの下になるようにワークフローにドロップします。  
  
3. **Dowhile**アクティビティの **[Condition]** プロパティ値ボックスに次の式を入力します。  
  
    ```vb  
    Guess <> Target  
    ```  
  
    ```csharp  
    Guess != Target  
    ```  
  
     <xref:System.Activities.Statements.DoWhile> アクティビティはその子アクティビティを実行し、その <xref:System.Activities.Statements.DoWhile.Condition%2A> を評価します。 <xref:System.Activities.Statements.DoWhile.Condition%2A> が `True` と評価される場合、<xref:System.Activities.Statements.DoWhile> 内のアクティビティが再度実行されます。 この例では、ユーザーの推定値が評価され、推定値が正しいと判断されるまで <xref:System.Activities.Statements.DoWhile> が続行されます。  
  
4. **[ツールボックス]** の **[NumberGuessWorkflowActivities]** セクションから**Prompt**アクティビティをドラッグし、前の手順の**dowhile**アクティビティにドロップします。  
  
5. [**プロパティ] ウィンドウ**で、 `"EnterGuess"` **Prompt**アクティビティの **[BookmarkName]** プロパティ値ボックスに引用符を含めて「」と入力します。 [ `Guess` **Result** ] プロパティ値ボックスに「」と入力し、 **[Text]** プロパティボックスに次の式を入力します。  
  
    ```vb  
    "Please enter a number between 1 and " & MaxNumber  
    ```  
  
    ```csharp  
    "Please enter a number between 1 and " + MaxNumber  
    ```  
  
    > [!TIP]
    >  [**プロパティ] ウィンドウ**が表示されていない場合は、 **[表示]** メニューの **[プロパティウィンドウ]** をクリックします。  
  
6. **ツールボックス**の **[プリミティブ]** セクションから**Assign**アクティビティをドラッグして、 **Prompt**アクティビティに続くように**dowhile**アクティビティにドロップします。  
  
    > [!NOTE]
    > **Assign**アクティビティを削除すると、ワークフローデザイナーが、 **Prompt**アクティビティと新しく追加された**Assign**アクティビティの両方を含む**Sequence**アクティビティを自動的に追加することに注意してください。  
  
7. [ `Turns` **To** ] ボックスに「 `Turns + 1` 」と入力し、[  **C#式を入力**するか、 **VB の式を入力**してください] ボックスに入力します。  
  
8. **[ツールボックス]** の **[制御フロー]** セクションから**If**アクティビティをドラッグし、新しく追加した**Assign**アクティビティの後になるように**Sequence**アクティビティにドロップします。  
  
9. **If**アクティビティの **[Condition]** プロパティ値ボックスに次の式を入力します。  
  
    ```vb  
    Guess <> Target  
    ```  
  
    ```csharp  
    Guess != Target  
    ```  
  
10. **ツールボックス**の **[制御フロー]** セクションから別の**if**アクティビティをドラッグし、最初の**if**アクティビティの**Then**セクションにドロップします。  
  
11. 新しく追加された**If**アクティビティの **[Condition]** プロパティ値ボックスに次の式を入力します。  
  
    ```
    Guess < Target  
    ```  
  
12. **ツールボックス**の **[プリミティブ]** セクションから2つの**WriteLine**アクティビティをドラッグしてドロップします。1つは、新しく追加した**If**アクティビティの**Then**セクションにあり、もう1つは**Else**セクションにあります。  
  
13. **[Then** ] セクションで **[WriteLine]** アクティビティをクリックして選択し、 **[Text]** プロパティ値ボックスに次の式を入力します。  
  
    ```text
    "Your guess is too low."  
    ```  
  
14. **[Else]** セクションの**WriteLine**アクティビティをクリックして選択し、 **[Text]** プロパティ値ボックスに次の式を入力します。  
  
    ```text
    "Your guess is too high."  
    ```  
  
     完成したワークフローの例を次に示します。  
  
     ![完成したシーケンシャルワークフローを示すスクリーンショット。](./media/how-to-create-a-sequential-workflow/complete-sequential-workflow.jpg)  
  
## <a name="to-build-the-workflow"></a>ワークフローをビルドするには  
  
1. Ctrl キーと Shift キーを押しながら B キーを押して、ソリューションをビルドします。  
  
     ワークフローを実行する方法については、次のトピック[「方法:ワークフロー](how-to-run-a-workflow.md)を実行します。 既に完了している[場合は、次の手順を実行します。別のスタイル](how-to-run-a-workflow.md)のワークフローを使用してワークフローステップを実行し、この手順のシーケンシャルワークフローを使用して実行するには、「方法:」の[「[アプリケーションをビルドして実行するに](how-to-run-a-workflow.md#BKMK_ToRunTheApplication)は」に進んでください。ワークフロー](how-to-run-a-workflow.md)を実行します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Activities.Statements.Flowchart>
- <xref:System.Activities.Statements.FlowDecision>
- [Windows Workflow Foundation プログラミング](programming.md)
- [ワークフローの設計](designing-workflows.md)
- [チュートリアル入門](getting-started-tutorial.md)
- [方法: アクティビティを作成する](how-to-create-an-activity.md)
- [方法: ワークフローを実行する](how-to-run-a-workflow.md)
