---
title: Windows Communication Foundation サービスのバインディングの構成
ms.date: 03/30/2017
helpviewer_keywords:
- binding configuration [WCF]
ms.assetid: 99a85fd8-f7eb-4a84-a93e-7721b37d415c
ms.openlocfilehash: bfcdcd172d96660c3351926a9c42d298ac3fa654
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69928562"
---
# <a name="configuring-bindings-for-windows-communication-foundation-services"></a>Windows Communication Foundation サービスのバインディングの構成
アプリケーションの作成では、アプリケーションの配置後は各種決定事項を管理者に任せる場合がよくあります。 たとえば、どのサービス アドレス (URI (Uniform Resource Identifier)) を使用するかなどの情報は、多くの場合、前もって知る方法がありません。 アドレスをハードコーディングする代わりに、サービスの作成後に管理者が指定する方が便利です。 構成を活用することで、この柔軟性が得られます。  
  
> [!NOTE]
> 構成ファイルをすばやく作成するには、 `/config` [ServiceModel メタデータユーティリティツール (svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)とスイッチを使用します。  
  
## <a name="major-sections"></a>主要なセクション  
 Windows Communication Foundation (WCF) 構成スキームには、次の3つの`serviceModel`主要`bindings`なセクション`services`(、、および) が含まれています。  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <bindings>  
        </bindings>  
        <services>  
        </services>  
        <behaviors>  
        </behaviors>  
    </system.serviceModel>  
</configuration>  
```  
  
### <a name="servicemodel-elements"></a>ServiceModel 要素  
 `system.ServiceModel`要素によって制限されたセクションを使用して、1つまたは複数のエンドポイントでサービスの種類を構成したり、サービスの設定を構成したりすることができます。 各エンドポイントでは、アドレス、コントラクト、およびバインディングをそれぞれ 1 つずつ構成できます。 エンドポイントの詳細については、「[エンドポイントの作成の概要](../../../docs/framework/wcf/endpoint-creation-overview.md)」を参照してください。 エンドポイントを指定しない場合、ランタイムは、既定のエンドポイントを追加します。 既定のエンドポイントについては、「[Simplified Configuration](../../../docs/framework/wcf/simplified-configuration.md)」 (簡易構成) と「[Simplified Configuration for WCF Services](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)」 (WCF サービスの簡易構成) を参照してください。  
  
 バインディングはトランスポート (HTTP、TCP、パイプ、およびメッセージ キュー) とプロトコル (セキュリティ、信頼性、およびトランザクション フロー) を指定し、バインド要素で構成されます。各バインド要素は、エンドポイントの通信方法のさまざまな側面を指定します。  
  
 たとえば、 [ \<basicHttpBinding >](../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)要素を指定すると、エンドポイントのトランスポートとして HTTP を使用することが指定されます。 このエンドポイントを使用するサービスが開かれる実行時に、エンドポイントとの接続に HTTP が使用されます。  
  
 バインディングには、定義済みバインディングとカスタム バインドの 2 種類があります。 定義済みバインディングには、一般的なシナリオで使用される要素の組み合わせが含まれています。 WCF に用意されている定義済みバインディングの種類の一覧については、「[システム指定のバインディング](../../../docs/framework/wcf/system-provided-bindings.md)」を参照してください。 定義済みバインディング コレクションに、サービス アプリケーションに必要な正しい機能の組み合わせがないときは、カスタム バインドを作成して、そのアプリケーションの要件を満たすことができます。 カスタムバインディングの詳細については、「 [ \<customBinding >](../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)」を参照してください。  
  
 次の4つの例は、WCF サービスの設定に使用される最も一般的なバインド構成を示しています。  
  
#### <a name="specifying-an-endpoint-to-use-a-binding-type"></a>バインディングの種類を使用するエンドポイントの指定  
 最初の例は、アドレス、コントラクト、およびバインディングをそれぞれ 1 つずつ使用して構成されたエンドポイントを指定する方法を示しています。  
  
```xml  
<service name="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null">  
  <!-- This section is optional with the default configuration introduced  
       in .NET Framework 4. -->  
  <endpoint   
      address="/HelloWorld2/"  
      contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
      binding="basicHttpBinding" />
</service>  
```  
  
 この例では、`name` 属性は、構成がどのサービス型に対するものであるかを示します。 `HelloWorld` コントラクトを使用してコードでサービスを作成すると、そのサービスは、この例の構成に定義されているすべてのエンドポイントと共に初期化されます。 アセンブリが1つのサービスコントラクトのみを実装`name`する場合、サービスは使用可能な型のみを使用するため、属性は省略できます。 この属性が受け取る文字列は、`Namespace.Class, AssemblyName, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null` の形式で指定される必要があります。  
  
 `address` 属性では、他のエンドポイントがこのサービスと通信するために使用する URI を指定します。 この URI は、絶対パスでも相対パスでもかまいません。 相対アドレスを指定すると、ホストは、そのバインディングで使用されるトランスポート スキームに適したベース アドレスを提供します。 アドレスが構成されていない場合、ベース アドレスはそのエンドポイントのアドレスと見なされます。  
  
 `contract` 属性では、このエンドポイントが公開するコントラクトを指定します。 サービス実装の型は、コントラクト型を実装する必要があります。 サービス実装が単一のコントラクトの型を実装する場合は、このプロパティを省略できます。  
  
 `binding` 属性では、この特定のエンドポイントに使用される定義済みバインディングまたはカスタム バインドを選択します。 バインディングが明示的に選択されていないエンドポイントでは、既定のバインディング選択 (`BasicHttpBinding`) を使用します。  
  
#### <a name="modifying-a-predefined-binding"></a>定義済みバインディングの変更  
 次の例では、定義済みバインディングを変更します。 これにより、サービスの任意のエンドポイントを構成するために使用できるようになります。 バインディングの変更では、<xref:System.ServiceModel.Configuration.IBindingConfigurationElement.ReceiveTimeout%2A> 値を 1 秒に設定します。 このプロパティは、<xref:System.TimeSpan> オブジェクトを返します。  
  
 変更されたバインディングは、バインディング セクションにあります。 この変更したバインディングは、`binding` 要素の `endpoint` 属性を設定することにより、任意のエンドポイントを作成するときに使用できます。  
  
> [!NOTE]
> バインディングに特定の名前を付ける場合、サービス エンドポイントで指定した `bindingConfiguration` と同じ名前にする必要があります。  
  
```xml  
<service name="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null">  
  <endpoint   
      address="/HelloWorld2/"  
      contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
      binding="basicHttpBinding" />
</service>  
<bindings>  
    <basicHttpBinding   
        receiveTimeout="00:00:01"  
    />  
</bindings>  
```  
  
## <a name="configuring-a-behavior-to-apply-to-a-service"></a>サービスに適用する動作の構成  
 次の例では、サービス型に対して、特定の動作を構成します。 要素は、 [ServiceModel メタデータユーティリティツール (svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)がサービスを照会し、メタデータから Web サービス記述言語 (WSDL) ドキュメントを生成するために使用されます。 `ServiceMetadataBehavior`  
  
> [!NOTE]
> 動作に特定の名前を付ける場合、サービスまたはエンドポイント セクションで指定した `behaviorConfiguration` と同じ名前にする必要があります。  
  
```xml  
<behaviors>  
    <behavior>  
        <ServiceMetadata httpGetEnabled="true" />   
    </behavior>  
</behaviors>  
<services>  
    <service   
       name="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null">
       <endpoint   
          address="http://computer:8080/Hello"  
          contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
          binding="basicHttpBinding" />
    </service>  
</services>  
```  
  
 前の構成では、クライアントが "HelloWorld" の型指定されたサービスを呼び出してメタデータを取得できます。  
  
 `svcutil /config:Client.exe.config http://computer:8080/Hello?wsdl`  
  
## <a name="specifying-a-service-with-two-endpoints-using-different-binding-values"></a>異なるバインディング値を使用する 2 つのエンドポイントを持つサービスの指定  
 この最後の例では、`HelloWorld` サービス型に 2 つのエンドポイントを構成します。 各エンドポイントは、同じ`bindingConfiguration`バインドの種類の異なるカスタマイズされた属性`basicHttpBinding`を使用します (それぞれがを変更します)。  
  
```xml  
<service name="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null">  
    <endpoint  
        address="http://computer:8080/Hello1"  
        contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
        binding="basicHttpBinding"  
        bindingConfiguration="shortTimeout" />
    <endpoint  
        address="http://computer:8080/Hello2"  
        contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
        binding="basicHttpBinding"  
        bindingConfiguration="Secure" />
</service>  
<bindings>  
    <basicHttpBinding   
        name="shortTimeout"  
        timeout="00:00:00:01"   
     />  
     <basicHttpBinding   
        name="Secure">  
        <Security mode="Transport" />  
     </basicHttpBinding>
</bindings>  
```  
  
 次の例に示すように、`protocolMapping` セクションを追加してバインディングを構成することによって、既定の構成を使用する同じ動作を取得できます。  
  
```xml  
<protocolMapping>  
    <add scheme="http" binding="basicHttpBinding" bindingConfiguration="shortTimeout" />  
    <add scheme="https" binding="basicHttpBinding" bindingConfiguration="Secure" />  
</protocolMapping>  
<bindings>  
    <basicHttpBinding   
        name="shortTimeout"  
        timeout="00:00:00:01"   
     />  
     <basicHttpBinding   
        name="Secure" />  
        <Security mode="Transport" />  
</bindings>  
```  
  
## <a name="see-also"></a>関連項目

- [簡略化された構成](../../../docs/framework/wcf/simplified-configuration.md)
- [システム標準のバインディング](../../../docs/framework/wcf/system-provided-bindings.md)
- [エンドポイントの作成の概要](../../../docs/framework/wcf/endpoint-creation-overview.md)
- [サービスとクライアントを構成するためのバインディングの使用](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
