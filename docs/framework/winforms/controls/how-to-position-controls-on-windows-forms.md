---
title: '方法: Windows フォーム上のコントロールを位置設定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- Location
- Location.Y
- Location.X
helpviewer_keywords:
- controls [Windows Forms]
- controls [Windows Forms], moving
- snaplines
- controls [Windows Forms], positioning
ms.assetid: 4693977e-34a4-4f19-8221-68c3120c2b2b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 1cc2cb4c749b7290a6edf914a8e6a697006ef43c
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987082"
---
# <a name="how-to-position-controls-on-windows-forms"></a>方法: Windows フォームにコントロールを配置する

コントロールを配置するには、Visual Studio で Windows フォームデザイナーを使用<xref:System.Windows.Forms.Control.Location%2A>するか、プロパティを指定します。

## <a name="position-a-control-on-the-design-surface-of-the-windows-forms-designer"></a>Windows フォームデザイナーのデザインサーフェイスにコントロールを配置する

Visual Studio で、マウスを使用して適切な位置にコントロールをドラッグします。

> [!NOTE]
> コントロールを選択し、方向キーを使用して移動し、より正確に配置します。 また、*スナップ線*を使用すると、フォームにコントロールを正確に配置できます。 詳細については、「[チュートリアル:スナップ線](walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)を使用した Windows フォーム上のコントロールの配置。

## <a name="position-a-control-using-the-properties-window"></a>プロパティウィンドウを使用してコントロールを配置する

1. Visual Studio で、配置するコントロールを選択します。

2. **[プロパティ]** ウィンドウで、 <xref:System.Windows.Forms.Control.Location%2A>プロパティの値をコンマで区切って入力し、コンテナー内にコントロールを配置します。

   最初の数値 (X) は、コンテナーの左境界線からの距離です。2番目の数値 (Y) は、コンテナー領域の上境界からの距離をピクセル単位で表したものです。

   > [!NOTE]
   > <xref:System.Windows.Forms.Control.Location%2A>プロパティを展開して、 **X**値と**Y**値を個別に入力できます。

## <a name="position-a-control-programmatically"></a>プログラムによるコントロールの配置

1. コントロールの<xref:System.Drawing.Point>プロパティをに設定します。 <xref:System.Windows.Forms.Control.Location%2A>

    ```vb
    Button1.Location = New Point(100, 100)
    ```

    ```csharp
    button1.Location = new Point(100, 100);
    ```

    ```cpp
    button1->Location = Point(100, 100);
    ```

2. サブ<xref:System.Windows.Forms.Control.Left%2A>プロパティを使用して、コントロールの位置の X 座標を変更します。

    ```vb
    Button1.Left = 300
    ```

    ```csharp
    button1.Left = 300;
    ```

    ```cpp
    button1->Left = 300;
    ```

## <a name="increment-a-controls-location-programmatically"></a>プログラムによってコントロールの位置をインクリメントする

<xref:System.Windows.Forms.Control.Left%2A>サブプロパティを設定して、コントロールの X 座標をインクリメントします。

```vb
Button1.Left += 200
```

```csharp
button1.Left += 200;
```

```cpp
button1->Left += 200;
```

> [!NOTE]
> コントロールの<xref:System.Windows.Forms.Control.Location%2A> X 位置と Y 位置を同時に設定するには、プロパティを使用します。 位置を個別に設定するには、コントロール<xref:System.Windows.Forms.Control.Left%2A>の (**X**) <xref:System.Windows.Forms.Control.Top%2A>サブプロパティまたは (**Y**) サブプロパティを使用します。 この構造体にはボタンの座標のコピーが含まれ<xref:System.Drawing.Point>ているため、ボタンの位置を表す構造体の X 座標と Y 座標は暗黙的に設定しないようにしてください。

## <a name="see-also"></a>関連項目

- [Windows フォーム コントロール](index.md)
- [チュートリアル: スナップ線を使用した Windows フォーム上のコントロールの配置](walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)
- [チュートリアル: TableLayoutPanel を使用した Windows フォームでのコントロールの配置](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)
- [チュートリアル: FlowLayoutPanel を使用した Windows フォームでのコントロールの配置](walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)
- [各 Windows フォーム コントロールのラベル設定とショートカットの作成](labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)
- [Windows フォームで使用するコントロール](controls-to-use-on-windows-forms.md)
- [Windows フォーム コントロールの機能別一覧](windows-forms-controls-by-function.md)
- [方法: 画面の場所を設定 Windows フォーム](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/52aha046(v=vs.100))
