---
title: '方法: カスタム拡張メソッドを実装して呼び出す - C# プログラミング ガイド'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- extension methods [C#], implementing and calling
ms.assetid: 7dab2a56-cf8e-4a47-a444-fe610a02772a
ms.openlocfilehash: 26ad1d2251388237e186d1ba0e885fd7def66467
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596882"
---
# <a name="how-to-implement-and-call-a-custom-extension-method-c-programming-guide"></a>方法: カスタム拡張メソッドを実装して呼び出す (C# プログラミング ガイド)
このトピックでは、あらゆる .NET 型を対象に独自の拡張メソッドを実装する方法について説明します。 クライアント コードで拡張メソッドを使用するには、拡張メソッドが格納されている DLL への参照を追加し、拡張メソッドが定義されている名前空間を指定する [using](../../language-reference/keywords/using-directive.md) ディレクティブを追加します。  
  
## <a name="to-define-and-call-the-extension-method"></a>拡張メソッドを定義して呼び出すには  
  
1. 拡張メソッドを格納するための静的[クラス](./static-classes-and-static-class-members.md)を定義します。  
  
     このクラスは、クライアント コードから参照できる必要があります。 アクセシビリティの規則の詳細については、「[アクセス修飾子](./access-modifiers.md)」を参照してください。  
  
2. 拡張メソッドを静的メソッドとして実装します。メソッドの可視性は、包含クラスと同レベル以上を指定します。  
  
3. メソッドの最初のパラメーターでは、メソッドが操作する型を指定します。型名の前には [this](../../language-reference/keywords/this.md) 修飾子を付加します。  
  
4. 呼び出し元のコードで、`using` ディレクティブを追加して、拡張メソッドのクラスを含む[名前空間](../../language-reference/keywords/namespace.md)を指定します。  
  
5. 型のインスタンス メソッドと同じようにメソッドを呼び出します。  
  
     呼び出し元のコードでは最初のパラメーターを指定しません。これは演算子を適用する型を表すものであり、コンパイラはオブジェクトの型を既に認識しているためです。 指定する必要があるのは、2 番目から `n` 番目のパラメーターの引数だけです。  
  
## <a name="example"></a>例  
 次の例では、`CustomExtensions.StringExtension` クラスの `WordCount` という名前の拡張メソッドを実装します。 このメソッドは、最初のメソッド パラメーターとして指定された <xref:System.String> クラスを操作します。 `CustomExtensions` 名前空間は、アプリケーション名前空間にインポートされ、メソッドは `Main` メソッド内で呼び出されます。  
  
 [!code-csharp[csProgGuideExtensionMethods#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExtensionMethods/cs/extensionmethods.cs#1)]  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ  
 拡張メソッドには、固有のセキュリティ上の脆弱性はありません。 名前の衝突の解決では、型自体で定義されているインスタンス メソッドまたは静的メソッドが常に優先されるため、型の既存のメソッドを偽装するために拡張メソッドが使用されることはありません。 拡張メソッドは、拡張されたクラスのプライベート データにはアクセスできません。  
  
## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [拡張メソッド](./extension-methods.md)
- [統合言語クエリ (LINQ)](../../linq/linq-in-csharp.md)
- [静的クラスと静的クラス メンバー](./static-classes-and-static-class-members.md)
- [protected](../../language-reference/keywords/protected.md)
- [internal](../../language-reference/keywords/internal.md)
- [public](../../language-reference/keywords/public.md)
- [this](../../language-reference/keywords/this.md)
- [namespace](../../language-reference/keywords/namespace.md)
