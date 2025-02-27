---
title: Windows フォーム デザイナーでのデザイン時エラー
ms.date: 03/30/2017
f1_keywords:
- DTELErrorList
- WhyDTELPage
helpviewer_keywords:
- errors [Windows Forms Designer]
- design-time errors [Windows Forms Designer]
ms.assetid: ad408380-825a-46d8-9a4a-531b130b88ce
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: cce9baf1523391e281593428b633c401103b42b5
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015970"
---
# <a name="design-time-errors-in-the-windows-forms-designer"></a>Windows フォームデザイナーのデザイン時エラー

このトピックでは、Windows フォームデザイナーの読み込みに失敗したときに Visual Studio に表示されるデザイン時エラー一覧の意味と使用方法について説明します。 このエラー リストが表示された場合、デザイナーのバグであると解釈するのではなく、コード内のエラーを修正するための参考情報であると考えてください。

エラーに関する詳細情報と考えられる解決策が提示されるので、このエラー リストの基本を理解することによって、アプリケーションのデバッグに役立てることができます。

## <a name="the-design-time-error-list-interface"></a>デザイン時エラー一覧のインターフェイス

Windows フォームデザイナーの読み込みに失敗した場合は、デザイナーにエラー一覧が表示されます。 エラーは複数のカテゴリに分類されています。 たとえば、宣言されていない変数の 4 つのインスタンスがある場合、それらは同じエラー カテゴリに分類されます。 各エラー カテゴリには、エラーの概要を示す簡単な説明が含まれます。

エラー カテゴリの見出しをクリックするか、展開/折りたたみシェブロンをクリックすることで、エラー カテゴリを展開したり、折りたたんだりできます。 エラー カテゴリを展開すると、次の追加のヘルプが表示されます。

- このエラーのインスタンス。

- このエラーのヘルプ。

- このエラーに関するフォーラムの投稿。

### <a name="instances-of-this-error"></a>このエラーのインスタンス

追加のヘルプには、現在のプロジェクトにおけるエラーのすべてのインスタンスが一覧表示されます。 多くのエラーには、次の形式の正確な場所が含まれます: *[プロジェクト名]* *[フォーム名]* 行: *[行番号]* 列: *[列番号]* 。 **[コードに移動]** リンクを使用して、エラーが発生したコード内の場所に移動できます。

呼び出し履歴がエラーに関連付けられている場合、 **[コール スタックの表示]** リンクをクリックすると、エラーがさらに展開され、呼び出し履歴が表示されます。 履歴を調べると、有用なデバッグ情報を得られる可能性があります。 たとえば、エラーが発生する前に呼び出された関数を追跡できます。 呼び出し履歴を選択して、コピーおよび保存できます。

> [!NOTE]
> Visual Basic では、デザイン時エラー リストには複数のエラーは表示されませんが、同じエラーの複数のインスタンスが表示される場合があります。 Visual C++ では、エラーに goto コード リンク/行番号リンクはありません。

### <a name="forum-posts-about-this-error"></a>このエラーに関するフォーラムの投稿

追加のヘルプには、エラーに関連するフォーラムの投稿へのリンクが含まれています。 フォーラムは、エラー メッセージの文字列に基づいて検索されます。 次のフォーラムで検索を試すこともできます。

- [Windows フォームデザイナーフォーラム](https://social.msdn.microsoft.com/Forums/windows/home?forum=winformsdesigner)

- [Windows フォームフォーラム](https://social.msdn.microsoft.com/Forums/windows/home?category=windowsforms)

### <a name="ignore-and-continue"></a>無視して続行

エラー状態を無視して、デザイナーの読み込みを続行することもできます。 この操作を選択すると、予期しない動作が発生する可能性があります。 たとえば、デザイン サーフェイスにコントロールが表示されない場合があります。

## <a name="see-also"></a>関連項目

- [デザイン時開発のトラブルシューティング](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ms171843(v=vs.120))
- [コントロールとコンポーネントの作成時のトラブルシューティング](troubleshooting-control-and-component-authoring.md)
- [デザイン時の Windows フォーム コントロールの開発](developing-windows-forms-controls-at-design-time.md)
- [Windows フォーム デザイナーのエラー メッセージ](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233640(v=vs.100))
