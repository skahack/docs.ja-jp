---
title: クライアント側 UI オートメーション プロバイダーの実装
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, client-side provider implementation
- client-side UI Automation provider, implementation
- provider implementation, UI Automation
ms.assetid: 3584c0a1-9cd0-4968-8b63-b06390890ef6
ms.openlocfilehash: 9079dfa03ab81bfa6875e43bfa8a6e5351e0a35d
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015117"
---
# <a name="client-side-ui-automation-provider-implementation"></a>クライアント側 UI オートメーション プロバイダーの実装
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 の最新情報[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]については[、「Windows Automation API:UI オートメーション](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 Microsoft オペレーティング[!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)]システム[!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]では、、、など、いくつかの異なるフレームワークが使用されています。 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)] [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] は、UI 要素に関する情報をクライアントに公開します。 ただし、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 自体は、それらのフレームワークに存在する各種のコントロールや、それらから情報を抽出するために必要な手法を認識しているわけではありません。 その代わりに、このタスクをプロバイダーと呼ばれるオブジェクトに任せます。 プロバイダーは、特定のコントロールから情報を抽出し、その情報を [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]に渡します。次に UI オートメーションが、その情報を一貫性のある方法でクライアントに提示します。  
  
 プロバイダーは、サーバー側とクライアント側のどちらにも配置できます。 サーバー側プロバイダーは、コントロール自体によって実装されます。 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 要素は、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] で作成されたすべてのサードパーティ コントロールを考慮してプロバイダーを実装しています。  
  
 ただし、 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] や [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)] に含まれているコントロールなどの比較的古いコントロールは、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]を直接サポートしていません。 これらのコントロールは、代わりにクライアント プロセス内のプロバイダーによって処理され、プロセス間通信を使用して、たとえば、コントロール間でのウィンドウ メッセージを監視することで、コントロールに関する情報を取得します。 このようなクライアント側プロバイダーは、プロキシと呼ばれることがあります。  
  
 [!INCLUDE[TLA2#tla_winvista](../../../includes/tla2sharptla-winvista-md.md)]には、標準[!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)]コントロールと Windows フォームコントロールのプロバイダーが用意されています。 また、フォールバックプロバイダーは、別の[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]サーバー側プロバイダーまたはプロキシによって処理されないが、Microsoft Active Accessibility 実装があるコントロールに対して、部分的なサポートを提供します。 これらすべてのプロバイダーは、自動的に読み込まれ、クライアント アプリケーションから使用できるようになります。  
  
 および Windows フォームコントロールの[!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)]サポートの詳細については、「 [UI オートメーションによる標準コントロールのサポート](../../../docs/framework/ui-automation/ui-automation-support-for-standard-controls.md)」を参照してください。  
  
 アプリケーションが他のクライアント側プロバイダーを登録することもできます。  
  
<a name="Distributing_Client-Side_Providers"></a>   
## <a name="distributing-client-side-providers"></a>クライアント側プロバイダーを配布する  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] では、クライアント側プロバイダーがマネージ コード アセンブリ内に見つかることを前提としています。 このアセンブリ内の名前空間は、アセンブリと同じ名前を持つ必要があります。 たとえば、ContosoProxies.dll というアセンブリには、ContosoProxies という名前空間が含まれます。 その名前空間内に、 <xref:UIAutomationClientsideProviders.UIAutomationClientSideProviders> クラスを作成します。 静的 <xref:UIAutomationClientsideProviders.UIAutomationClientSideProviders.ClientSideProviderDescriptionTable> フィールドの実装内に、プロバイダーを記述した <xref:System.Windows.Automation.ClientSideProviderDescription> 構造体の配列を作成します。  
  
<a name="Registering_and_Configuring_Client-Side_Providers"></a>   
## <a name="registering-and-configuring-client-side-providers"></a>クライアント側プロバイダーを登録および構成する  
 ダイナミックリンクライブラリ (DLL) 内のクライアント側プロバイダーは、を呼び出す<xref:System.Windows.Automation.ClientSettings.RegisterClientSideProviderAssembly%2A>ことによって読み込まれます。 クライアント アプリケーションでは、プロバイダーを利用するために、それ以上のアクションは必要ありません。  
  
 クライアント独自のコードで実装されたプロバイダーは、 <xref:System.Windows.Automation.ClientSettings.RegisterClientSideProviders%2A>を使用して登録されます。 このメソッドは引数として、 <xref:System.Windows.Automation.ClientSideProviderDescription> 構造体の配列を受け取ります。各構造体では、次のプロパティが指定されます。  
  
- プロバイダー オブジェクトを作成するコールバック関数。  
  
- プロバイダーが使用されるコントロールのクラス名。  
  
- プロバイダーが使用されるアプリケーションのイメージ名 (通常は実行可能ファイルの完全名)。  
  
- クラス名と、ターゲット アプリケーションで検出されたウィンドウ クラスを照合する方法を制御するフラグ。  
  
 最後の 2 つのパラメーターは省略できます。 クライアントでは、異なるアプリケーションに対して異なるプロバイダーを使用する必要がある場合、ターゲット アプリケーションのイメージ名を指定することができます。 たとえば、クライアントは、Multiple View パターンをサポートする既知のアプリケーションの [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] リスト ビュー コントロールに対して、あるプロバイダーを使用し、そのパターンをサポートしない別の既知のアプリケーションの同様のコントロールに対して別のプロバイダーを使用できます。  
  
## <a name="see-also"></a>関連項目

- [クライアント側 UI オートメーション プロバイダーの作成](../../../docs/framework/ui-automation/create-a-client-side-ui-automation-provider.md)
- [クライアント アプリケーションに UI オートメーション プロバイダーを実装する](../../../docs/framework/ui-automation/implement-ui-automation-providers-in-a-client-application.md)
