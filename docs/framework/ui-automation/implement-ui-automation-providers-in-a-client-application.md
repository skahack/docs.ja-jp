---
title: クライアント アプリケーションに UI オートメーション プロバイダーを実装する
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- client-side UI Automation provider, implementation within applications
- UI Automation, implementing client-side provider within application
ms.assetid: f325f0d8-1715-41ea-85ca-45b82ffea8bc
ms.openlocfilehash: ef3d03bee412b97ed88ec76e81ad2fd19a9595eb
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968947"
---
# <a name="implement-ui-automation-providers-in-a-client-application"></a>クライアント アプリケーションに UI オートメーション プロバイダーを実装する
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 の最新情報[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]については[、「Windows Automation API:UI オートメーション](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 このトピックのコード例では、アプリケーション内のクライアント側 UI オートメーション プロバイダーを実装する方法を示します。  
  
 これは、一般的ではないシナリオです。 通常は、UI オートメーション クライアント アプリケーションは、サーバー側プロバイダーを使用するか、または DLL 内に存在するクライアント側プロバイダーを使用します。  
  
## <a name="example"></a>例  
 次のコード例では、コンソール ウィンドウ用の簡単なプロバイダーを実装します。 このコードは、有用な機能は備えていませんが、クライアント コード内でプロバイダーを設定し、 <xref:System.Windows.Automation.ClientSettings.RegisterClientSideProviders%2A>を使用して登録する際の基本的な手順を示すために用意されています。  
  
 [!code-csharp[UIAClientSideProvider_snip#201](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClientSideProvider_snip/CSharp/ClientImplementationProgram.cs#201)]
 [!code-vb[UIAClientSideProvider_snip#201](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClientSideProvider_snip/visualbasic/clientimplementationprogram.vb#201)]  
  
## <a name="see-also"></a>関連項目

- [UI オートメーション プロバイダーの概要](../../../docs/framework/ui-automation/ui-automation-providers-overview.md)
- [クライアント側プロバイダー アセンブリの登録](../../../docs/framework/ui-automation/register-a-client-side-provider-assembly.md)
- [クライアント側 UI オートメーション プロバイダーの作成](../../../docs/framework/ui-automation/create-a-client-side-ui-automation-provider.md)
- [クライアント側 UI オートメーション プロバイダーの実装](../../../docs/framework/ui-automation/client-side-ui-automation-provider-implementation.md)
