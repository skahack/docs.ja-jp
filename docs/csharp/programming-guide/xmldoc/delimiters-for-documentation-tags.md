---
title: ドキュメント タグの区切り記号 - C# プログラミング ガイド
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- XML [C#], delimiters
- /** */ delimiters for C# documentation tags
- /// delimiter for C# documentation
ms.assetid: 9b2bdd18-4f5c-4c0b-988e-fb992e0d233e
ms.openlocfilehash: c8d20284b7ef2e06fb987f94f05cbe1dde1dc431
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69928074"
---
# <a name="delimiters-for-documentation-tags-c-programming-guide"></a>ドキュメント タグの区切り記号 (C# プログラミング ガイド)
XML ドキュメント コメントでは区切り記号を使用し、ドキュメント コメントの開始位置と終了位置をコンパイラに示す必要があります。 XML ドキュメント タグでは、次の種類の区切り記号を使用できます。  
  
 `///`  
 単一行の区切り記号。 ドキュメント例で使用されています。この区切り記号は、Visual C# プロジェクト テンプレートで使用されます。 区切り記号の直後に空白文字が続く場合、その文字は XML 出力に含まれません。  
  
> [!NOTE]
> Visual Studio IDE には、スマート コメント編集と呼ばれる機能があります。コード エディターで `///` 区切り記号を入力すると、\<summary> タグと \</summary> タグが自動的に挿入され、これらのタグの内側にカーソルが移動します。 [[オプション] ダイアログ ボックス](/visualstudio/ide/reference/options-text-editor-csharp-advanced)で、この機能をオンまたはオフにできます。  
  
 `/** */`  
 複数行の区切り記号。  
  
 `/** */` 区切り記号を使用する場合は、次の書式設定規則に従う必要があります。  
  
- `/**` 区切り記号がある行で、行の残りの部分が空白の場合、その行はコメントとして処理されません。 `/**` 区切り記号の後の最初の文字が空白の場合、その空白文字は無視され、行の残りの部分が処理されます。 それ以外の場合、`/**` 区切り記号の後にある行のテキスト全体が、コメントの一部として処理されます。  
  
- `*/` 区切り記号がある行で、`*/` 区切り記号までの部分がすべて空白の場合、その行は無視されます。 それ以外の場合、以下の箇条書きで説明するパターン一致規則に従って、その行の `*/` 区切り記号までのテキストがコメントの一部として処理されます。  
  
- `/**` 区切り記号で始まる行の後に来る行については、コンパイラは各行の先頭で共通のパターンを検索します。 このパターンは、空白 (省略可能) + アスタリスク (`*`) + 空白 (省略可能) で構成されます。 `/**` 区切り記号または `*/` 区切り記号で始まらない各行の先頭でコンパイラが共通のパターンを見つけた場合、各行のそのパターンは無視されます。  
  
 これらの規則について、次の例で説明します。  
  
- 次のコメントでは、`<summary>` で始まる行だけがコメントの一部として処理されます。 次の 3 つのタグ形式は、いずれも同じコメントを生成します。  
  
    ```csharp  
    /** <summary>text</summary> */   
  
    /**   
    <summary>text</summary>   
    */   
  
    /**   
     * <summary>text</summary>   
    */  
    ```  
  
- コンパイラは、2 行目と 3 行目の先頭で共通のパターン " * " を識別します。 このパターンは出力に含まれません。  
  
    ```csharp  
    /**   
     * <summary>   
     * text </summary>*/   
    ```  
  
- 次のコメントでは、3 行目の 2 番目の文字がアスタリスクではないため、コンパイラは共通のパターンを検索しません。 このため、2 行目と 3 行目のすべてのテキストがコメントの一部として処理されます。  
  
    ```csharp  
    /**   
     * <summary>   
       text </summary>  
    */   
    ```  
  
- 次のコメントでは、2 つの原因によりコンパイラはパターンを検出しません。 まず、アスタリスクの前の空白の数が一致していません。 次に、5 行目がタブで始まっています。空白とタブは一致しません。 このため、2 行目から 5 行目のすべてのテキストがコメントの一部として処理されます。  
  
    ```csharp  
    /**   
      * <summary>   
      * text   
     *  text2   
        *  </summary>   
    */   
    ```  
  
## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [XML ドキュメント コメント](./index.md)
- [/doc (C# コンパイラ オプション)](../../language-reference/compiler-options/doc-compiler-option.md)
- [XML ドキュメント コメント](./index.md)
