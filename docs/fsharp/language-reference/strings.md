---
title: 文字列
description: "' String ' F#型が Unicode 文字のシーケンスとして不変テキストを表す方法について説明します。"
ms.date: 07/05/2019
ms.openlocfilehash: 284de939c90c4d9d4ea064fb4db1fb90a37038e2
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2019
ms.locfileid: "68627106"
---
# <a name="strings"></a>文字列

> [!NOTE]
> この記事の API リファレンスのリンクをクリックすると MSDN に移動します。  docs.microsoft.com API リファレンスは完全ではありません。

この`string`型は、変更できないテキストを Unicode 文字のシーケンスとして表します。 `string` は、.NET Framework の `System.String` のエイリアスです。

## <a name="remarks"></a>Remarks

文字列リテラルは引用符 (") で区切られます。 バックスラッシュ文字 ( \\ ) は、特定の特殊文字をエンコードするために使用されます。 円記号と次の文字は、*エスケープシーケンス*と呼ばれます。 エスケープ シーケンスが F# 文字列リテラルは、次の表に示すでサポートされています。

|文字|エスケープ シーケンス|
|---------|---------------|
|警告|`\a`|
|バックスペース|`\b`|
|フォーム フィード|`\f`|
|改行|`\n`|
|キャリッジ リターン|`\r`|
|Tab|`\t`|
|垂直タブ|`\v`|
|円記号|`\\`|
|引用符|`\"`|
|単一|`\'`|
|Unicode 文字|`\DDD`(は10進数字、000-255 の範囲、 `\231` = "ç" など) `D`|
|Unicode 文字|`\xHH`(は16進数の数字、00 ~ FF の範囲、 `\xE7` = "ç" など) `H`|
|Unicode 文字|`\uHHHH`(UTF-16)(は16進数の数字、0000 ~ FFFF の範囲を示します。`H` たとえば、 `\u00E7` = "ç")|
|Unicode 文字|`\U00HHHHHH`(UTF-32)(は16進数字、範囲 000000-10ffff を示します。`H` たとえば、 `\U0001F47D` = "👽")|

> [!IMPORTANT]
> `\DDD`エスケープシーケンスは、他のほとんどの言語のような8進数表記ではなく、10進表記です。 したがって、 `8`桁数`9`とは有効であり、の`\032`シーケンスは空白 (U + 0020) を表しますが、8進数表記では同じ`\040`コードポイントが使用されます。

> [!NOTE]
> 0-255 (0xff) の範囲に制限されている`\DDD`場合`\x` 、とエスケープシーケンスは、実際には、最初の 256 Unicode コードポイントと一致するため、 [ISO-8859-1](https://en.wikipedia.org/wiki/ISO/IEC_8859-1#Code_page_layout)文字セットになります。

前に @ 記号が付いている場合、リテラルは逐語的文字列になります。 これは、2つの引用符文字が1つの引用符文字として解釈される点を除いて、すべてのエスケープシーケンスが無視されることを意味します。

さらに、文字列を三重引用符で囲むこともできます。 この場合、二重引用符文字を含め、すべてのエスケープシーケンスが無視されます。 引用符で囲まれた埋め込み文字列を含む文字列を指定するには、逐語的文字列または三重引用符で囲んだ文字列を使用します。 逐語的文字列を使用する場合は、単一引用符文字を示す2つの引用符文字を指定する必要があります。 三重引用符で囲まれた文字列を使用する場合は、文字列の末尾として解析することなく、単一引用符文字を使用できます。 この手法は、XML や、埋め込み引用符を含むその他の構造体を操作する場合に便利です。

```fsharp
// Using a verbatim string
let xmlFragment1 = @"<book author=""Milton, John"" title=""Paradise Lost"">"

// Using a triple-quoted string
let xmlFragment2 = """<book author="Milton, John" title="Paradise Lost">"""
```

コードでは、改行文字を含む文字列は改行文字として解釈されますが、バックスラッシュ文字が改行前の最後の文字である場合は除きます。 円記号が使用されている場合、次の行の先頭の空白文字は無視されます。 次のコードでは、 `str1`値`"abc\ndef"`を持つ文字列と`str2`値`"abcdef"`を持つ文字列が生成されます。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1001.fs)]

次のように、配列に似た構文を使用して、文字列内の個々の文字にアクセスできます。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1002.fs)]

出力は `b`になります。

または、次のコードに示すように、配列スライス構文を使用して部分文字列を抽出することもできます。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1003.fs)]

出力は次のとおりです。

```
abc
def
```

符号なしバイトの配列 (型`byte[]`) によって ASCII 文字列を表すことができます。 文字列リテラルにサフィックス`B`を追加して、ASCII 文字列であることを示します。 バイト配列で使用される ASCII 文字列リテラルでは、unicode エスケープシーケンスを除き、Unicode 文字列と同じエスケープシーケンスがサポートされます。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1004.fs)]

## <a name="string-operators"></a>文字列演算子

文字列を連結するには、 `+`演算子を使用する方法と`^`演算子を使用する方法の2つの方法があります。 演算子`+`は、.NET Framework 文字列処理機能との互換性を維持します。

次の例は、文字列の連結を示しています。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1006.fs)]

## <a name="string-class"></a>String クラス

のF#文字列型は実際には .NET Framework `System.String`型であるため、すべての`System.String`メンバーを使用できます。 これには`+` 、文字列`Length`を連結するために使用される演算子、プロパティ、 `Chars`および Unicode 文字の配列として文字列を返すプロパティが含まれます。 文字列の詳細については`System.String`、「」を参照してください。

`Chars` の`System.String`プロパティを使用すると、次のコードに示すように、インデックスを指定することにより、文字列内の個々の文字にアクセスできます。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1005.fs)]

## <a name="string-module"></a>文字列モジュール

文字列処理の追加機能は、 `String` `FSharp.Core`名前空間のモジュールに含まれています。 詳細については、「 [Core. 文字列モジュール](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.string-module-%5bfsharp%5d)」を参照してください。

## <a name="see-also"></a>関連項目

- [F# 言語リファレンス](index.md)
