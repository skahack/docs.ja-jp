---
title: <message> の <netMsmqBinding>
ms.date: 03/30/2017
ms.assetid: 6ebf0240-d7be-4493-b0fe-f00fd5989d77
ms.openlocfilehash: b163dcb08e9656e3bde9c7fbb71fa1c92c9957ca
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69931517"
---
# <a name="message-of-netmsmqbinding"></a>\<netmsmqbinding \<> のメッセージ >

この `netMsmqBinding` バインディングでの SOAP メッセージ セキュリティ設定を定義します。

```xml
<system.ServiceModel>
  <bindings>
    <netMsmqBinding>
      <binding>
        <security>
          <message>
```

## <a name="syntax"></a>構文

```xml
<netMsmqBinding>
  <binding>
    <security>
      <message algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
               clientCredentialType="None/Windows/UserName/Certificate/CardSpace" />
    </security>
  </binding>
</netMsmqBinding>
```

## <a name="attributes-and-elements"></a>属性および要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|algorithmSuite|MSMQ トランスポートを介して送信されるメッセージにメッセージ ベースのセキュリティを実現するために使用されるメッセージの暗号化およびキー ラップ アルゴリズムを設定します。<br /><br /> 既定値は `Aes256` です。 この属性は <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 型です。|
|clientCredentialType|MSMQ トランスポートで送信されるメッセージに対してクライアント認証を実行するときに使用される資格情報の種類を指定します。 有効な値は次のとおりです。<br /><br /> 存在サービスが匿名クライアントと対話できるようになります。 サービスとクライアントはいずれも資格情報を要求しません。<br />ウィンドウこれにより、Windows 資格情報の認証済みコンテキストで SOAP 交換を行うことができます。 これは、常に Kerberos ベースの認証を実行します。<br />ユーザー名これにより、サービスは、ユーザー名資格情報を使用したクライアントの認証を要求できます。 この場合の資格情報は、 `clientCredentials`動作に注意して指定する必要があり**ます。** Windows Communication Foundation (WCF) では、パスワードダイジェストの送信や、パスワードを使用したキーの派生、およびメッセージセキュリティのためのこのようなキーの使用はサポートされていません。 そのため、ユーザー名の資格情報を使用する場合、WCF は exchange がセキュリティで保護されるように強制します。 このモードは、サービス証明書が、`clientCredential` 動作および `serviceCertificate` を使用してクライアント側で指定されることを要求します。 <br /><br /> 証明これにより、サービスは、クライアントが証明書を使用して認証されるように要求できます。 この場合のクライアント資格情報は、`clientCredentials` 動作を使用して指定する必要があります。 この場合のサービス資格情報は、`clientCredentials` を指定して `serviceCertificate` 動作を使用することで、指定する必要があります。<br />CardSpaceこれにより、サービスは、クライアントが CardSpace を使用して認証されるように要求できます。 `serviceCertificate` は、`clientCredential` 動作で提供される必要があります。<br /><br /> 既定値は `Windows` です。 この属性は <xref:System.ServiceModel.MessageCredentialType> 型です。|

### <a name="child-elements"></a>子要素

なし

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[\<security>](security-of-netmsmqbinding.md)|バインディングのセキュリティ設定を定義します。|

## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.MessageSecurityOverMsmqElement>
- <xref:System.ServiceModel.Configuration.NetMsmqSecurityElement.Message%2A>
- <xref:System.ServiceModel.NetMsmqSecurity.Message%2A>
- <xref:System.ServiceModel.MessageSecurityOverMsmq>
- [WCF のキュー](../../../wcf/feature-details/queues-in-wcf.md)
- [サービスおよびクライアントのセキュリティ保護](../../../wcf/feature-details/securing-services-and-clients.md)
- [バインディング](../../../wcf/bindings.md)
- [システムが提供するバインディングの構成](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [サービスとクライアントを構成するためのバインディングの使用](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
