---
title: '方法: デザイナーを使って Windows フォーム ListView コントロールの項目をグループ化する'
ms.date: 03/30/2017
helpviewer_keywords:
- ListView control [Windows Forms], grouping items
- grouping
- groups [Windows Forms], in Windows Forms controls
ms.assetid: 8b615000-69d9-4c64-acaf-b54fa09b69e3
ms.openlocfilehash: b63bcd9e5e357db350cc2987e09af84eb58bdcff
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69039399"
---
# <a name="how-to-group-items-in-a-windows-forms-listview-control-using-the-designer"></a>方法: デザイナーを使って Windows フォーム ListView コントロールの項目をグループ化する

<xref:System.Windows.Forms.ListView>コントロールのグループ化機能を使用すると、関連する項目のセットをグループに表示できます。 これらのグループは、グループタイトルを含む横方向のグループヘッダーによって画面上で区切られます。 グループを使用<xref:System.Windows.Forms.ListView>すると、項目をアルファベット順、日付形式、またはその他の論理グループ別にグループ化することで、大きなリストを簡単に移動できます。 次の図は、グループ化された項目を示しています。

![奇数と偶数のグループに分割された数値。](./media/how-to-group-items-in-a-windows-forms-listview-control-using-the-designer/odd-even-list-view-groups.gif)

次の手順では、 <xref:System.Windows.Forms.ListView>コントロールを含むフォームを含む**Windows アプリケーション**プロジェクトが必要です。 このようなプロジェクトの設定の詳細につい[ては、「方法:Windows フォームアプリケーションプロジェクト](/visualstudio/ide/step-1-create-a-windows-forms-application-project)を作成し[、次の操作を行います。Windows フォーム](how-to-add-controls-to-windows-forms.md)にコントロールを追加します。

グループ化を有効にするには、最初に<xref:System.Windows.Forms.ListViewGroup>デザイナーまたはプログラムを使用して、1つ以上のオブジェクトを作成する必要があります。 グループを定義したら、それに項目を割り当てることができます。

> [!NOTE]
> <xref:System.Windows.Forms.ListView>グループは、アプリケーションが[!INCLUDE[WinXpFamily](../../../../includes/winxpfamily-md.md)]メソッドを<xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=nameWithType>呼び出したときにのみ使用できます。 以前のオペレーティングシステムでは、グループに関連するすべてのコードは効果がなく、グループは表示されません。 詳細については、「 <xref:System.Windows.Forms.ListView.Groups%2A?displayProperty=nameWithType> 」を参照してください。

## <a name="to-add-or-remove-groups-in-the-designer"></a>デザイナーでグループを追加または削除するには

1. **[プロパティ]** ウィンドウで、プロパティの横![にある省略記号 (省略記号ボタン ([...])](./media/visual-studio-ellipsis-button.png)をクリックして、 <xref:System.Windows.Forms.ListView.Groups%2A>プロパティの横にある [プロパティウィンドウ] ボタンをクリックします。

     **ListViewGroup Collection エディター**が表示されます。

2. グループを追加するには、 **[追加]** ボタンをクリックします。 その後、プロパティ<xref:System.Windows.Forms.ListViewGroup.Header%2A>や<xref:System.Windows.Forms.ListViewGroup.HeaderAlignment%2A>プロパティなど、新しいグループのプロパティを設定できます。 グループを削除するには、グループを選択し、 **[削除]** ボタンをクリックします。

## <a name="to-assign-items-to-groups-in-the-designer"></a>デザイナーで項目をグループに割り当てるには

1. **[プロパティ]** ウィンドウで、プロパティの横![にある省略記号 (省略記号ボタン ([...])](./media/visual-studio-ellipsis-button.png)をクリックして、 <xref:System.Windows.Forms.ListView.Items%2A>プロパティの横にある [プロパティウィンドウ] ボタンをクリックします。

     **ListViewItem Collection エディター**が表示されます。

2. 新しい項目を追加するには、 **[追加]** ボタンをクリックします。 その後、プロパティ<xref:System.Windows.Forms.ListViewItem.Text%2A>や<xref:System.Windows.Forms.ListViewItem.ImageIndex%2A>プロパティなど、新しい項目のプロパティを設定できます。

3. <xref:System.Windows.Forms.ListViewItem.Group%2A>プロパティを選択し、ドロップダウンリストからグループを選択します。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.ListView>
- <xref:System.Windows.Forms.ListView.Groups%2A>
- <xref:System.Windows.Forms.ListViewGroup>
- [ListView コントロール](listview-control-windows-forms.md)
- [ListView コントロールの概要](listview-control-overview-windows-forms.md)
- [方法: Windows フォーム ListView コントロールを使用して項目を追加および削除する](how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
