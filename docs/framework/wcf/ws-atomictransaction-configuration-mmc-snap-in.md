---
title: WS-AtomicTransaction 構成 MMC スナップイン
ms.date: 03/30/2017
ms.assetid: 23592973-1d51-44cc-b887-bf8b0d801e9e
ms.openlocfilehash: 1fa0548e2d63562ddcb85fc6392bf5c99d67d6c7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916818"
---
# <a name="ws-atomictransaction-configuration-mmc-snap-in"></a>WS-AtomicTransaction 構成 MMC スナップイン
WS-AtomicTransaction 構成 MMC スナップインは、WS-AtomicTransaction 設定の一部をローカル マシンとリモート マシンの両方で構成するために使用されます。  
  
## <a name="remarks"></a>Remarks  
 または[!INCLUDE[wxp](../../../includes/wxp-md.md)] [!INCLUDE[ws2003](../../../includes/ws2003-md.md)]を実行している場合、MMC スナップインを見つけるには、 **[コントロールパネル]** 、管理ツール、コンポーネントサービス の順に移動し、**マイコンピューター**を右クリックし、 **[プロパティ]** を選択します。 これは MSDTC を構成する場合と同じ場所です。 構成できるオプションは、グループ化されて、 **WS-AT**タブです。  
  
 Windows Vista また[!INCLUDE[lserver](../../../includes/lserver-md.md)]はを実行している場合は、 **[スタート]** ボタンをクリックし、**検索**ボックスに「 `dcomcnfg.exe` 」と入力すると、MMC スナップインが表示されます。 MMC が開いているときに移動、**マイ Computer\Distributed トランザクション コーディネーター DTC**ノードを右クリックし、**プロパティ**です。 構成できるオプションは、グループ化されて、 **WS-AT**タブです。  
  
 前の手順は、ローカル マシンを構成するためのスナップインを起動するために使用します。 リモートコンピューターを構成する場合は、[**コントロールパネル]、[管理ツール]、[コンポーネントサービス**]、の順に移動し、または[!INCLUDE[wxp](../../../includes/wxp-md.md)] [!INCLUDE[ws2003](../../../includes/ws2003-md.md)]を実行している場合は同様の手順を実行します。 Windows vista または[!INCLUDE[lserver](../../../includes/lserver-md.md)]を実行している場合は、 [!INCLUDE[lserver](../../../includes/lserver-md.md)]Vista の場合は前の手順に従いますが、リモートコンピューターのノードの下の **[分散トランザクション Coordinator\Local DTC]** ノードを使用します。  
  
 ツールのユーザー インターフェイスを使用するには、WsatUI.dll ファイルを登録する必要があります。このファイルのパスは次のとおりです。  
  
 **%PROGRAMFILES%\Microsoft SDKs\Windows\v6.0\Bin\WsatUI.dll**  
  
 登録するには、次のコマンドを実行します。  
  
```Output  
regasm.exe /codebase WsatUI.dll  
```  
  
 このツールを使用すると、WS-AtomicTransaction の基本設定を変更できます。 たとえば、WS-AtomicTransaction プロトコル サポートの有効/無効の切り替え、WS-AT で使用する HTTP ポートの構成、SSL 証明書の HTTP ポートへのバインド、証明書のサブジェクト名指定による証明書の構成、トレース モードの選択とタイムアウトの既定および上限の設定を行うことができます。  
  
 WS-AtomicTransaction サポートをローカル マシン上にのみ構成する必要がある場合は、このツールのコマンド ライン バージョンを使用できます。 コマンドラインツールの詳細については、「ws-atomictransaction[構成ユーティリティ (wsatConfig .exe)](../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md) 」トピックを参照してください。  
  
 MMC スナップインとコマンド ライン ツールはいずれも、すべての WS-AT 設定を構成できるわけではありません。 これらの設定は、レジストリを直接変更することによってのみ編集できます。 これらのレジストリ設定の詳細については、「 [ws-atomictransaction のサポートの構成](../../../docs/framework/wcf/feature-details/configuring-ws-atomic-transaction-support.md)」を参照してください。  
  
### <a name="user-interface-description"></a>ユーザー インターフェイスの説明  
 **Ws-atomictransaction のトランザクションネットワークサポートを有効にする**:  
  
 このチェック ボックスをオンまたはオフに切り替えると、このスナップインのすべての GUI コンポーネントが有効または無効になります。  
  
 このチェック ボックスをオンにする前に、受信か送信の通信、またはその両方で [ネットワーク DTC アクセス] が有効であることを確認する必要があります。 この値は、MSDTC スナップインの **[セキュリティ]** タブで確認できます。  
  
#### <a name="network-group-box"></a>Network グループ ボックス  
 Network グループでは、HTTPS ポートや追加のセキュリティ設定 (SSL 暗号化など) を指定できます。 DTC ネットワーク トランザクションが有効でない場合、このグループは無効 (灰色表示) です。  
  
 **HTTPS ポート**  
  
 これは WS-AT に使用される HTTPS ポートの値です。 有効なポートを表す値は、1 ～ 65535 の範囲内であることが必要です。 HTTP ポートを変更すると、HTTP サービス構成が変更されます。つまり、前に使用していた WS-AT サービス アドレスが解放され、新しいポートに基づいて新しい WS-AT サービス アドレスが登録されます。 さらに、新しく選択したポートは、現在選択している SSL 証明書で暗号化されます。  
  
> [!NOTE]
> このツールを実行する前にファイアウォールが既に有効な場合、ポートは例外の一覧に自動的に登録されます。 このツールを実行する前にファイアウォールが無効な場合、ファイアウォールに関する追加の構成はありません。  
  
 WS-AT の構成後にファイアウォールを有効にする場合は、このツールを再度実行し、このパラメーターを使用してポート番号を指定する必要があります。 WS-AT の構成後にファイアウォールを無効にする場合は、入力を追加しないで WS-AT の動作を続行します。  
  
 **エンドポイント証明書**  
  
 **[選択**] ボタンをクリックすると、ローカルコンピューターで現在利用可能な証明書が一覧表示され、ユーザーは SSL 暗号化に使用できる証明書を選択できます。 証明書には、秘密キーが必要です。 秘密キーがない場合は、エラー メッセージが表示されます。  
  
> [!NOTE]
> 選択したポートに SSL 証明書を設定すると、そのポートに関連付けられたオリジナルの SSL 証明書が上書きされます。  
  
 **承認されたアカウント**  
  
 **[選択**] ボタンをクリックすると、Windows Access Control リストエディターが呼び出されます。このエディターでは、**参加**の **[許可]** ボックスまたは **[拒否]** ボックスをオンにして、ws-atomictransaction トランザクションに参加できるユーザーまたはグループを指定できます。アクセス許可グループ。  
  
 **承認済み証明書**  
  
 **[選択**] ボタンをクリックすると、LocalMachine で現在利用可能な証明書の一覧が表示されます。 WS-AtomicTransaction への参加が許可される証明書 ID を選択できます。  
  
#### <a name="timeout-group-box"></a>Timeout グループ ボックス  
 **[タイムアウト]** グループボックスでは、ws-atomictransaction トランザクションの既定のタイムアウトと最大のタイムアウトを指定できます。 送信のタイムアウトの有効値は 1 ～ 3600 の範囲です。 受信のタイムアウトの有効値は 0 ～ 3600 の範囲です。  
  
#### <a name="tracing-and-logging-group-box"></a>グループ ボックスのトレースとログ記録  
 **[トレースとログ記録]** グループボックスを使用すると、目的のトレースとログ記録レベルを構成できます。  
  
 **[オプション]** ボタンをクリックすると、追加の設定を指定できるページが表示されます。  
  
 [**トレースレベル**の組み合わせ] ボックスを使用すると、 <xref:System.Diagnostics.TraceLevel>列挙の任意の有効な値から選択できます。 また、チェック ボックスを使用して、アクティビティ トレースやアクティビティ伝達を実行するかどうかを指定したり、個人を特定する情報を収集するかどうかを指定することもできます。  
  
 **[ログセッション]** グループボックスで、ログセッションを指定することもできます。  
  
> [!NOTE]
> 別のトレース コンシューマーが WS-AT トレース プロバイダーを使用している場合は、トレース イベントの新しいログ セッションを作成できません。 このときにログ記録を構成しようとすると、エラー メッセージ "プロバイダーを有効にできませんでした。 エラーコード:1 "。  
  
 トレースとログ記録の詳細については、「[管理と診断](../../../docs/framework/wcf/diagnostics/index.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [WS-AtomicTransaction サポートの構成](../../../docs/framework/wcf/feature-details/configuring-ws-atomic-transaction-support.md)
- [WS-AtomicTransaction 構成ユーティリティ (wsatConfig.exe)](../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md)
- [管理と診断](../../../docs/framework/wcf/diagnostics/index.md)
