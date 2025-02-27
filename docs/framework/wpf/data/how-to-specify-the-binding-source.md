---
title: '方法: バインディング ソースを指定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- binding data [WPF], binding sources
- data binding [WPF], binding source
- binding sources [WPF]
ms.assetid: 55d47757-2648-4a52-987f-b767953f168c
ms.openlocfilehash: 418dc77ce7638698d4850b06dafcea57787e1015
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69959698"
---
# <a name="how-to-specify-the-binding-source"></a>方法: バインディング ソースを指定する
データ バインディングでは、バインド ソース オブジェクトとは、そこからデータを取得するオブジェクトを指します。 このトピックでは、バインド ソースを指定するさまざまな方法について説明します。  
  
## <a name="example"></a>例  
 複数のプロパティを共通ソースにバインドする場合は、`DataContext` を使用できます。これは、すべてのデータ バインド プロパティが共通ソースを継承するスコープを確立するための便利な方法です。  
  
 次の例では、アプリケーションのルート要素にデータ コンテキストが確立されます。 これにより、すべての子要素がそのデータ コンテキストを継承することができます。 バインドするデータは、マッピングを通して直接参照され、リソース キー `incomeDataSource` が与えられるカスタム データ クラス `NetIncome` から取得されます。  
  
 [!code-xaml[DirectionalBinding#DataContext1](~/samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml#datacontext1)]  
[!code-xaml[DirectionalBinding#DataContext2](~/samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml#datacontext2)]  
  
 次の例は、`NetIncome` クラスの定義を示します。  
  
 [!code-csharp[DirectionalBinding#DataObject](~/samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/billsdata.cs#dataobject)]
 [!code-vb[DirectionalBinding#DataObject](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DirectionalBinding/VisualBasic/NetIncome.vb#dataobject)]  
  
> [!NOTE]
> 上記の例では、マークアップ内のオブジェクトをインスタンス化し、それをリソースとして使用しています。 コードで既にインスタンス化されているオブジェクトにバインドする場合は、`DataContext` プロパティをプログラムで設定する必要があります。 例については、「[方法: XAML でデータをバインディング可能にする](how-to-make-data-available-for-binding-in-xaml.md)」を参照してください。  
  
 個々のバインドでソースを明示的に指定する場合は、次のオプションを使用できます。 これらは、継承されたデータ コンテキストに優先します。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|<xref:System.Windows.Data.Binding.Source%2A>|オブジェクトのインスタンスにソースを設定するには、このプロパティを使用します。 複数のプロパティが同じデータコンテキストを継承するスコープを確立する機能が不要な場合は、プロパティ<xref:System.Windows.Data.Binding.Source%2A> `DataContext`の代わりにプロパティを使用できます。 詳細については、「 <xref:System.Windows.Data.Binding.Source%2A> 」を参照してください。|  
|<xref:System.Windows.Data.Binding.RelativeSource%2A>|これは、バインディング ターゲットの場所を基準としてソースを指定する場合に便利です。 このプロパティを使用できる一般的なシナリオとして、要素の 1 つのプロパティを同じ要素の別のプロパティにバインドする場合や、スタイルまたはテンプレート内のバインドを定義する場合があります。 詳細については、「 <xref:System.Windows.Data.Binding.RelativeSource%2A> 」を参照してください。|  
|<xref:System.Windows.Data.Binding.ElementName%2A>|バインド先の要素を表す文字列を指定します。 これは、アプリケーションの別の要素のプロパティにバインドする場合に便利です。 たとえば、を<xref:System.Windows.Controls.Slider>使用して、アプリケーション内の別のコントロールの高さを制御したり、 <xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A>コントロールのを<xref:System.Windows.Controls.ContentControl.Content%2A> <xref:System.Windows.Controls.ListBox>コントロールのプロパティにバインドしたりする場合などです。 詳細については、「 <xref:System.Windows.Data.Binding.ElementName%2A> 」を参照してください。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.FrameworkElement.DataContext%2A?displayProperty=nameWithType>
- <xref:System.Windows.FrameworkContentElement.DataContext%2A?displayProperty=nameWithType>
- [プロパティ値の継承](../advanced/property-value-inheritance.md)
- [データ バインディングの概要](data-binding-overview.md)
- [バインディング宣言の概要](binding-declarations-overview.md)
- [方法トピック](data-binding-how-to-topics.md)
