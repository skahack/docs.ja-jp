---
title: WS 2007 フェデレーション HTTP バインディング
ms.date: 03/30/2017
ms.assetid: 91c1b477-a96e-4bf5-9330-5e9312113371
ms.openlocfilehash: 95ec5b6b0edbab979f0bcf0238152ba6c96c5cf8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69942205"
---
# <a name="ws-2007-federation-http-binding"></a>WS 2007 フェデレーション HTTP バインディング
このサンプルでは、<xref:System.ServiceModel.WS2007FederationHttpBinding> の使用例を示します。これは、WS-Trust 仕様のバージョン 1.3 に対応したフェデレーション シナリオを構築するための標準のバインディングです。  
  
> [!NOTE]
> このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。  
  
 このサンプルは、コンソール ベースのプログラム (Client.exe)、コンソール ベースのセキュリティ トークン サービス プログラム (Securitytokenservice.exe)、およびコンソール ベースのサービス プログラム (Service.exe) で構成されています。 サービスは、要求/応答通信パターンを定義するコントラクトを実装します。 このコントラクトは `ICalculator` インターフェイスによって定義されており、算術演算 (`Add`、`Subtract`、`Multiply`、`Divide`) を公開しています。 クライアントは、セキュリティ トークンをセキュリティ トークン サービス (STS) から取得し、指定された算術演算を実行する同期要求をサービスに対して行います。 サービスが応答し、結果を返します。 クライアント アクティビティは、コンソール ウィンドウに表示されます。  
  
 このサンプルは、`ICalculator` 要素を使用して `ws2007FederationHttpBinding` コントラクトを利用できるようにします。 このバインディングのクライアント側の構成は、次のコードに示すとおりです。  
  
```xml  
<bindings>  
  <ws2007FederationHttpBinding>  
    <binding name="ServiceFed" >  
      <security mode ="Message">  
        <message issuedKeyType ="SymmetricKey"  
                 issuedTokenType ="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1" >  
          <!-- Endpoint address and binding for Security Token Service -->  
          <issuer address ="http://localhost:8000/sts/windows"   
                  binding ="ws2007HttpBinding" />                
        </message>  
      </security>  
    </binding>  
  </ws2007FederationHttpBinding>  
</bindings>  
```  
  
 セキュリティ > では、値`security`によって、使用するセキュリティモードを指定します。 [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-element-of-ws2007federationhttpbinding.md) このサンプル`message`では、セキュリティが使用されます。これは[ \<、](../../../../docs/framework/configure-apps/file-schema/wcf/message-element-of-ws2007federationhttpbinding.md) [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-element-of-ws2007federationhttpbinding.md)メッセージ > がセキュリティ > 内で指定されるためです。 [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/message-element-of-ws2007federationhttpbinding.md) `ICalculator`発行者 >、メッセージ > 内の要素は、クライアントがサービスに対して認証できるように、セキュリティトークンをクライアントに発行する STS のアドレスとバインディングを指定します。 [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/issuer.md)  
  
 このバインディングのサービス側の構成は、次のコードに示すとおりです。  
  
```xml  
<bindings>  
  <ws2007FederationHttpBinding>  
    <binding name="ServiceFed" >  
      <security mode ="Message">  
        <message issuedKeyType ="SymmetricKey"  
                 issuedTokenType ="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1" >  
          <!-- Metadata address for Security Token Service -->  
          <issuerMetadata address ="http://localhost:8000/sts/mex" >  
            <identity>  
              <certificateReference storeLocation ="CurrentUser"   
                                    storeName="TrustedPeople"   
                                    x509FindType ="FindBySubjectDistinguishedName"   
                                    findValue ="CN=STS" />  
            </identity>  
          </issuerMetadata>  
        </message>  
      </security>  
    </binding>  
  </ws2007FederationHttpBinding>  
</bindings>  
```  
  
 セキュリティ > では、値`security`によって、使用するセキュリティモードを指定します。 [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-element-of-ws2007federationhttpbinding.md) このサンプル`message`では、セキュリティが使用されます。これは[ \<、](../../../../docs/framework/configure-apps/file-schema/wcf/message-element-of-ws2007federationhttpbinding.md) [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-element-of-ws2007federationhttpbinding.md)メッセージ > がセキュリティ > 内で指定されるためです。 メッセージ > 内部の`ws2007FederationHttpBinding` [ \<issuermetadata >](../../../../docs/framework/configure-apps/file-schema/wcf/issuermetadata.md) [要素は、STS のメタデータを取得するために使用できるエンドポイントのアドレスと id を指定します。 \<](../../../../docs/framework/configure-apps/file-schema/wcf/message-element-of-ws2007federationhttpbinding.md)  
  
 このサービスの動作を次のコードに示します。  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior name ="ServiceBehaviour" >  
      <serviceDebug includeExceptionDetailInFaults ="true"/>  
      <serviceMetadata httpGetEnabled ="true"/>  
      <serviceCredentials>  
        <issuedTokenAuthentication>  
          <knownCertificates>  
            <add storeLocation ="LocalMachine"  
                 storeName="TrustedPeople"  
                 x509FindType="FindBySubjectDistinguishedName"  
                 findValue="CN=STS" />  
          </knownCertificates>  
        </issuedTokenAuthentication>  
        <serviceCertificate storeLocation ="LocalMachine"  
                            storeName ="My"  
                            x509FindType ="FindBySubjectDistinguishedName"  
                            findValue ="CN=localhost"/>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 IssuedTokenAuthentication > > を使用すると、サービスは、認証時にクライアントが提示できるトークンに対して制約を指定できます。 [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenauthentication-of-servicecredentials.md) この構成の指定では、サブジェクト名が CN=STS である証明書によって署名されたトークンがサービスによって受け入れられます。  
  
 STS は、標準の <xref:System.ServiceModel.WS2007HttpBinding> を使用して、単一のエンドポイントを利用できるようにします。 このサービスは、クライアントからのトークンの要求に応答し、 クライアントが Windows アカウントを使用して認証されている場合は、クライアントのユーザー名がクレームとして含まれているトークンを発行します。 STS は、トークン作成の一環として、CN=STS 証明書に関連付けられている秘密キーを使用して、トークンに署名します。 また、対称キーを作成し、CN=localhost 証明書に関連付けられている秘密キーを使用して暗号化します。 STS は、トークンをクライアントに返すときに、対称キーも返します。 クライアントは、発行されたトークンを `ICalculator` サービスに提示し、対称キーを使用してメッセージに署名することで対称キーを認識していることを証明します。  
  
 サンプルを実行すると、セキュリティ トークン要求が STS のコンソール ウィンドウに表示されます。 操作要求と応答は、クライアントとサービスのコンソール ウィンドウに表示されます。 いずれかのコンソール ウィンドウで Enter キーを押すと、アプリケーションがシャットダウンします。  

```
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714
Press <ENTER> to terminate client.
```

 このサンプルに用意されている Setup.bat ファイルを使用すると、適切な証明書を使用してサーバーと STS を構成し、自己ホスト型アプリケーションを実行できるようになります。 このバッチ ファイルにより、LocalMachine/TrustedPeople 証明書ストアに 2 つの証明書が作成されます。 片方の証明書は CN=STS のサブジェクト名を持ち、クライアントに発行するセキュリティ トークンを署名するために STS が使用します。 もう片方の証明書は CN=localhost のサブジェクト名を持ち、サービスが暗号化を解除できるようにシークレットを暗号化するために STS が使用します。  
  
### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1. [Windows Communication Foundation サンプルの1回限りのセットアップ手順](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)を実行したことを確認します。  
  
2. 管理者特権で Visual Studio の開発者コマンドプロンプトを開き、Setup.exe ファイルを実行して必要な証明書を作成します。  
  
 このバッチ ファイルでは、Windows SDK と共に配布される Certmgr.exe および Makecert.exe が使用されます。 ただし、スクリプトでこれらのツールを見つけるには、Visual Studio のコマンド プロンプト内から Setup.bat を実行する必要があります。  
  
1. ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)」の手順に従います。  
  
2. サンプルを単一コンピューター構成または複数コンピューター構成で実行するには、「 [Windows Communication Foundation サンプルの実行](../../../../docs/framework/wcf/samples/running-the-samples.md)」の手順に従います。 を使用して[!INCLUDE[windowsver](../../../../includes/windowsver-md.md)]いる場合は、サービスを管理者特権で実行する必要があります (ファイルを右クリックし、 **[管理者として実行]** をクリックします)。  
  
> [!IMPORTANT]
>  サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780)にアクセスして、すべての[!INCLUDE[wf1](../../../../includes/wf1-md.md)] Windows Communication Foundation (wcf) とサンプルをダウンロードしてください。 このサンプルは、次のディレクトリに格納されます。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\WS\WS2007FederationHttp`  
