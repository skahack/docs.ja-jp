---
title: -errorreport (C# コンパイラ オプション)
ms.date: 07/20/2015
f1_keywords:
- /errorreport
helpviewer_keywords:
- -errorreport compiler option [C#]
- errorreport compiler option [C#]
- /errorreport compiler option [C#]
ms.assetid: bd0e7493-b79d-4369-9c3f-ba26ebdfbedf
ms.openlocfilehash: dc876f609643b7112c0f54574bd202c7c19cb119
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924769"
---
# <a name="-errorreport-c-compiler-options"></a>-errorreport (C# コンパイラ オプション)
このオプションは、C# 内部コンパイラ エラーを Microsoft に報告する方法として便利です。  
  
> [!NOTE]
> Windows Vista と Windows Server 2008 の場合、Windows エラー報告 (WER) 経由で行った設定が Visual Studio のエラー報告設定によってオーバーライドされることはありません。 WER 設定は、常に Visual Studio のエラー報告設定よりも優先されます。  
  
## <a name="syntax"></a>構文  
  
```console  
-errorreport:{ none | prompt | queue | send }  
```  
  
## <a name="arguments"></a>引数  
 "**なし**"  
 内部コンパイラ エラーに関するレポートは、収集されず、マイクロソフトに送信されません。  
  
 **prompt**  
 内部コンパイラ エラーを受信したときにレポートを送信するかどうか確認するメッセージを表示します。 **prompt** は、開発環境でアプリケーションをコンパイルする場合の既定値です。  
  
 **queue**  
 エラー レポートを待ち行列に入れます。 管理者資格情報でログオンすると、前回のログオン以降に発生したすべてのエラーを報告できます。 エラー レポートを送信するためのダイアログ ボックスが表示されるのは、3 日に一度だけです。 **queue** は、コマンド ラインでアプリケーションをコンパイルする場合の既定値です。  
  
 **send**  
 内部コンパイラ エラーのレポートをマイクロソフトに自動的に送信します。 このオプションを有効にするには、まずマイクロソフトのデータ収集ポリシーに同意する必要があります。 コンピューターで **-errorreport:send** を初めて指定すると、マイクロソフトのデータ収集ポリシーが記載されている Web サイトが表示されます。  
    
## <a name="remarks"></a>解説  
 コンパイラがソース コード ファイルを処理できないと、内部コンパイラ エラー (ICE: Internal Compiler Error) が発生します。 ICE が発生した場合、コードの修正に利用できる出力ファイルや診断は生成されません。  
  
 以前のリリースでは、ICE が発生した場合、マイクロソフト製品サポート サービスに連絡して問題を報告することを推奨していました。 **-errorreport** を使用すると、ICE 情報を Visual C# チームに提供できます。 エラー レポートは、今後リリースされるコンパイラの機能向上に役立ちます。  
  
 コンピューターまたはユーザー ポリシーによるアクセス許可によっては、レポートを送信できない場合があります。  
  
 エラー デバッガーの詳細については、「[Windows のワトソン博士 (Drwtsn32.exe) ツールについて](https://support.microsoft.com/help/308538/description-of-the-dr--watson-for-windows-drwtsn32-exe-tool)」を参照してください。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 開発環境でこのコンパイラ オプションを設定するには  
  
1. プロジェクトの **[プロパティ]** ページを開きます。 詳細については、「[Build Page, Project Designer (C#)](/visualstudio/ide/reference/build-page-project-designer-csharp)」([ビルド] ページ (プロジェクト デザイナー) (C#)) を参照してください。  
  
2. **[ビルド]** プロパティ ページをクリックします。  
  
3. **[詳細設定]** ボタンをクリックします。  
  
4. **[内部コンパイル エラー報告]** プロパティを変更します。  
  
 このコンパイラ オプションをプログラムで設定する方法については、「<xref:VSLangProj80.CSharpProjectConfigurationProperties3.ErrorReport%2A>」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [C# コンパイラ オプション](./index.md)
