---
title: '方法: WCF URL 予約を制限付きの予約に置き換える'
ms.date: 03/30/2017
ms.assetid: 2754d223-79fc-4e2b-a6ce-989889f2abfa
ms.openlocfilehash: f9cfda1d4ca14dd380dd01f944d4c900f9832096
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62039547"
---
# <a name="how-to-replace-the-wcf-url-reservation-with-a-restricted-reservation"></a>方法: WCF URL 予約を制限付きの予約に置き換える
URL 予約を使用すると、特定の URL または URL セットからメッセージを受信するユーザーを制限できます。 予約は、URL テンプレート、アクセス制御リスト (ACL)、およびフラグのセットで構成されます。 URL テンプレートは、予約の対象となる URL を定義します。 URL テンプレートが処理される方法の詳細については、次を参照してください。[受信要求のルーティング](https://go.microsoft.com/fwlink/?LinkId=136764)します。 ACL は、指定された URL からメッセージを受信できるユーザーまたはユーザー グループを制御します。 フラグは、その予約で、ユーザーまたはグループに URL を直接リッスンする権限を与えるか、リッスンを他のプロセスに委任する権限を与えるかを指定します。  
  
 既定のオペレーティング システム構成の一環として、Windows Communication Foundation (WCF) はポート 80 に、双方向の通信にデュアル HTTP バインディングを使用してアプリケーションを実行するすべてのユーザーのグローバルにアクセス可能な予約を作成します。 この予約の ACL はすべてのユーザー向けなので、管理者は URL または URL セットをリッスンする権限を明示的に許可または拒否することはできません。 このトピックでは、この予約を削除し、制限された ACL を使用する予約を再作成する方法について説明します。  
  
 [!INCLUDE[wv](../../../../includes/wv-md.md)] または [!INCLUDE[lserver](../../../../includes/lserver-md.md)] では、管理特権でのコマンド プロンプトから「`netsh http show urlacl`」と入力することで、すべての HTTP URL 予約を表示できます。  次の例では、ようになります WCF URL 予約を示します。  
  
```  
Reserved URL : http://+:80/Temporary_Listen_Addresses/  
        User: \Everyone  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;WD)  
```  
  
 予約は、WCF アプリケーションが双方向の通信にデュアル HTTP バインディングを使用する場合に使用される URL テンプレートで構成されます。 このフォームの Url は、デュアル HTTP バインディングを介して通信するときに、WCF クライアントにメッセージを返すを送信する WCF サービスに使用されます。 すべてのユーザーに対して、URL をリッスンする権限が与えられていますが、リッスンを他のプロセスに委任する権限は与えられていません。 また、ACL は SSDL (Security Descriptor Definition Language) で記述されています。 SSDL の詳細については、次を参照してください[SSDL。](https://go.microsoft.com/fwlink/?LinkId=136789)  
  
### <a name="to-delete-the-wcf-url-reservation"></a>WCF URL 予約を削除するには  
  
1. をクリックして**開始**、 をポイント**すべてのプログラム**、 をクリックして**アクセサリ**を右クリックして**コマンド プロンプト** をクリック**として実行管理者**話題になるコンテキスト メニュー。 をクリックして**続行**ユーザー アカウント制御 (UAC) ウィンドウを続行するアクセス許可を要求する可能性があります。  
  
2. 入力**netsh http 削除 urlacl url =http://+:80/Temporary_Listen_Addresses/** コマンド プロンプト ウィンドウでします。  
  
3. 予約が正常に削除されると、次のメッセージが表示されます。 **URL 予約が正常に削除されました**  
  
## <a name="creating-a-new-security-group-and-new-restricted-url-reservation"></a>新しいセキュリティ グループおよび新しい制限付き URL 予約の作成  
 WCF URL 予約を制限付きの予約に置き換えるに最初に新しいセキュリティ グループを作成する必要があります。 この操作は、コマンド プロンプトを使用する方法か、コンピューターの管理コンソールを使用する方法で行うことができます。 行う必要があるのはいずれか一方のみです。  
  
#### <a name="to-create-a-new-security-group-from-a-command-prompt"></a>コマンド プロンプトで新しいセキュリティ グループを作成するには  
  
1. をクリックして**開始**、 をポイント**すべてのプログラム**、 をクリックして**アクセサリ**を右クリックして**コマンド プロンプト** をクリック**として実行管理者**話題になるコンテキスト メニュー。 をクリックして**続行**ユーザー アカウント制御 (UAC) ウィンドウを続行するアクセス許可を要求する可能性があります。  
  
2. 入力 **net localgroup"\<セキュリティ グループ名 >"/コメント:"\<セキュリティ グループの説明 >"/add** コマンド プロンプトでします。 置き換える **\<セキュリティ グループ名 >** を作成するセキュリティ グループの名前と **\<セキュリティ グループの説明 >** の適切な説明と、セキュリティ グループ。  
  
3. セキュリティ グループが正常に作成されると、次のメッセージが表示されます。 **コマンドが正常に完了しました。**  
  
#### <a name="to-create-a-new-security-group-from-the-computer-management-console"></a>コンピューターの管理コンソールで新しいセキュリティ グループを作成するには  
  
1. をクリックして**開始**、 をクリックして**コントロール パネルの** 、 をクリックして**管理ツール**、 をクリック**コンピュータの管理**コンピューターを開く管理コンソールです。 をクリックして**続行**ユーザー アカウント制御 (UAC) ウィンドウを続行するアクセス許可を要求する可能性があります。  
  
2. をクリックして**システム ツール**、 をクリックして**ローカル ユーザーとグループ**を右クリックして**グループ**フォルダーをクリックします**新規グループ**コンテキスト メニューを起動します。 入力**グループ名**、**説明**と各種情報をこの新しいセキュリティ グループをクリックして、**作成**セキュリティ グループを作成するボタンをクリックします。  
  
#### <a name="to-create-the-restricted-url-reservation"></a>制限付き URL 予約を作成するには  
  
1. をクリックして**開始**、 をポイント**すべてのプログラム**、 をクリックして**アクセサリ**を右クリックして**コマンド プロンプト** をクリック**として実行管理者**話題になるコンテキスト メニュー。 をクリックして**続行**ユーザー アカウント制御 (UAC) ウィンドウを続行するアクセス許可を要求する可能性があります。  
  
2. 入力 **netsh http 追加 urlacl url =http://+:80/Temporary_Listen_Addresses/ ユーザー ="\< マシン名 >\\ < セキュリティ グループ名\>** コマンド プロンプトでします。 置き換える **\<マシン名 >** にコンピューター名、グループを作成する必要がありますと **\<セキュリティ グループ名 >** を作成したセキュリティ グループの名前先に。  
  
3. 予約が正常に作成されると、 **URL 予約が正常に追加された**します。
