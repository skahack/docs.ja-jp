---
title: '方法: 企業内のエンドポイントをロックダウンする'
ms.date: 03/30/2017
ms.assetid: 1b7eaab7-da60-4cf7-9d6a-ec02709cf75d
ms.openlocfilehash: 6a74df56d4c283569988d310b2a501e6440f58ca
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69951657"
---
# <a name="how-to-lock-down-endpoints-in-the-enterprise"></a>方法: 企業内のエンドポイントをロックダウンする
大規模な企業では、多くの場合、企業のセキュリティ ポリシーに準拠してアプリケーションを開発する必要があります。 次のトピックでは、コンピューターにインストールされているすべての Windows Communication Foundation (WCF) クライアントアプリケーションの検証に使用できるクライアントエンドポイント検証コントロールを開発してインストールする方法について説明します。  
  
 この場合、このエンドポイント動作は machine.config ファイルのクライアント[ \<commonbehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md)セクションに追加されるため、検証コントロールはクライアント検証コントロールです。 WCF は、クライアントアプリケーションに対してのみ共通のエンドポイント動作を読み込み、サービスアプリケーションに対してのみ共通のサービス動作を読み込みます。 サービス アプリケーション用のこの同じ検証コントロールをインストールするには、検証コントロールがサービス動作であることが必要です。 詳細については、 [ \<commonbehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md)に関するセクションを参照してください。  
  
> [!IMPORTANT]
> 構成ファイルの[ \<commonbehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md)セクションに<xref:System.Security.AllowPartiallyTrustedCallersAttribute>追加された属性 (APTCA) でマークされていないサービスまたはエンドポイントの動作は、アプリケーションが部分信頼環境で実行されている場合は実行されません。このエラーが発生すると、例外がスローされます。 検証コントロールなどの共通動作を強制的に実行するには、次のいずれかを行う必要があります。  
>   
>  -- 共通動作を <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 属性でマークし、部分信頼アプリケーションとして展開したときに実行できるようにします。 APTCA でマークされたアセンブリを実行できないように、コンピューターでレジストリ エントリを設定できます。  
>   
>  -- アプリケーションが完全信頼アプリケーションとして配置されている場合に、ユーザーが部分信頼環境でアプリケーションを実行するようにコード アクセス セキュリティ設定を変更できないことを確認します。 ユーザーがこのような変更を行うことができる場合、カスタム検証コントロールは実行されず、例外もスローされません。 これを確認する方法の1つと`levelfinal`して、[コードアクセスセキュリティポリシーツール (caspol.exe)](https://go.microsoft.com/fwlink/?LinkId=248222)を使用するオプションを参照してください。  
>   
>  詳細については、「[部分信頼のベストプラクティス](../../../../docs/framework/wcf/feature-details/partial-trust-best-practices.md)」および「[サポートされている展開シナリオ](../../../../docs/framework/wcf/feature-details/supported-deployment-scenarios.md)」を参照してください。  
  
### <a name="to-create-the-endpoint-validator"></a>エンドポイント検証コントロールを作成するには  
  
1. <xref:System.ServiceModel.Description.IEndpointBehavior> メソッドに、必要な検証手順を備えた <xref:System.ServiceModel.Description.IEndpointBehavior.Validate%2A> を作成します。 次にコード例を示します。 (は`InternetClientValidatorBehavior` 、[セキュリティ検証](../../../../docs/framework/wcf/samples/security-validation.md)のサンプルから取得したものです)。  
  
     [!code-csharp[LockdownValidation#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/internetclientvalidatorbehavior.cs#2)]  
  
2. 手順 1. で作成したエンドポイント検証コントロールを登録する新しい <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> を作成します。 このコード例を次に示します。 (この例の元のコードは、[セキュリティ検証](../../../../docs/framework/wcf/samples/security-validation.md)のサンプルに含まれています)。  
  
     [!code-csharp[LockdownValidation#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/internetclientvalidatorelement.cs#3)]  
  
3. コンパイル済みのアセンブリが厳密な名前で署名されていることを確認します。 詳細については、「[厳密名ツール (SN)」を参照してください。EXE)](https://go.microsoft.com/fwlink/?LinkId=248217)を使用します。  
  
### <a name="to-install-the-validator-into-the-target-computer"></a>検証コントロールをターゲット コンピューターにインストールするには  
  
1. 適切な機構を使用してエンドポイント検証をインストールします。 企業では、グループ ポリシーと Systems Management Server (SMS) を使用してインストールします。  
  
2. [Gacutil.exe (グローバルアセンブリキャッシュツール)](../../../../docs/framework/tools/gacutil-exe-gac-tool.md)を使用して、厳密な名前のアセンブリをグローバルアセンブリキャッシュにインストールします。  
  
3. <xref:System.Configuration?displayProperty=nameWithType> 名前空間の型を使用して、次の処理を行います。  
  
    1. 完全修飾型名を使用して、動作拡張機能を[ \<>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviorextensions.md)セクションに追加し、要素をロックします。  
  
         [!code-csharp[LockdownValidation#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#5)]  
  
    2. `EndpointBehaviors` [Commonbehaviors > セクションのプロパティに behavior 要素を追加し、要素をロックします。 \<](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) (サービスの検証コントロールをインストールするには、検証コントロールが <xref:System.ServiceModel.Description.IServiceBehavior> であることが必要です。また、検証コントロールを `ServiceBehaviors` プロパティに追加する必要があります)。次のコード例は、手順 a. と b. の後の適切な構成を示しています。厳密な名前が存在しない点だけが異なります。  
  
         [!code-csharp[LockdownValidation#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#6)]  
  
    3. machine.config ファイルを保存します。 次のコード例では、手順 3. にあるすべてのタスクを実行しますが、変更された machine.config ファイルのコピーはローカルに保存されます。  
  
         [!code-csharp[LockdownValidation#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#7)]  
  
## <a name="example"></a>例  
 次のコード例では、machine.config ファイルに共通の動作を追加し、そのコピーをディスクに保存する方法を示します。 は`InternetClientValidatorBehavior` 、[セキュリティ検証](../../../../docs/framework/wcf/samples/security-validation.md)のサンプルから取得されます。  
  
 [!code-csharp[LockdownValidation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#1)]  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ  
 また、構成ファイルの要素を暗号化する必要がある場合もあります。 詳細については、「参照」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [DPAPI を使用した構成ファイルの要素の暗号化](https://go.microsoft.com/fwlink/?LinkId=94954)
- [RSA を使用して構成ファイルの要素を暗号化する](https://go.microsoft.com/fwlink/?LinkId=94955)
