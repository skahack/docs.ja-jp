---
title: <add> <scopedCertificates>要素
ms.date: 03/30/2017
ms.assetid: e21c1ef8-d6d6-4bca-ac5a-6fbf4bd77412
ms.openlocfilehash: 9756d37527fcf888cad930b24677ae8e6a2c8fba
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69920056"
---
# <a name="add-of-scopedcertificates-element"></a>\<scopedCertificates > 要素\<の > の追加
範囲指定された証明書のコレクションに X.509 証明書を追加します。  
  
 \<system.ServiceModel >  
\<<behaviors>  
endpointBehaviors セクション  
\<behavior>  
\<clientCredentials>  
\<serviceCertificate>  
\<scopedCertificates >  
\<scopedCertificates > の > \<要素の追加  
  
## <a name="syntax"></a>構文  
  
```xml  
<add findValue="String"
     storeLocation="CurrentUser/LocalMachine"
     storeName=" CurrentUser/LocalMachine"
     targetUri="string"
     x509Type="FindByThumbprint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindBySerialNumber/FindByTimeExpired/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|targetUri|文字列。 証明書に関連付けられているサービスの URI を指定します。|  
|findValue|文字列。 検索対象の値。|  
|x509FindType|列挙値。 検索する証明書フィールドのいずれかです。|  
|storeLocation|列挙値。 検索する 2 つの格納場所のいずれかです。|  
|storeName|列挙値。 検索するシステム ストアのいずれかです。|  
  
## <a name="findvalue-attribute"></a>findValue 属性  
  
|値|説明|  
|-----------|-----------------|  
|String|値は、検索されるフィールド (X509FindType 属性により指定される) によって異なります。 たとえば、サムプリント検索する場合、値は 16 進数の文字列にする必要があります。|  
  
## <a name="x509findtype-attribute"></a>x509FindType 属性  
  
|値|説明|  
|-----------|-----------------|  
|列挙|次の値が含まれます。FindByThumbprint、FindBySubjectName、Findbysubjectdistinguishedname です、FindByIssuerName、FindByIssuerDistinguishedName、FindBySerialNumber、FindByTimeValid、FindByTimeNotYetValid、FindBySerialNumber、FindByTimeExpired、FindByTemplateName, FindByApplicationPolicy, FindByCertificatePolicy, FindByExtension, FindByKeyUsage, FindBySubjectKeyIdentifier.|  
  
## <a name="storelocation-attribute"></a>storeLocation 属性  
  
|値|説明|  
|-----------|-----------------|  
|列挙型|CurrentUser または LocalMachine です。|  
  
## <a name="storename-attribute"></a>storeName 属性  
  
|値|説明|  
|-----------|-----------------|  
|列挙|次の値が含まれます。アドレス帳、AuthRoot、CertificateAuthority、許可されていない、My、Root、TrustedPeople、Trustedpeople。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<scopedCertificates>](scopedcertificates-element.md)|認証用の (範囲指定された) 特定のサービスにより提供される X.509 証明書のコレクションを表します。|  
  
## <a name="remarks"></a>Remarks  
 この要素を使用すると、クライアントは、通信するサービスの URL に基づいて、使用するサービス証明書を構成できます。 これは、クライアントが複数のサービス (エンド サービスと中間セキュリティ トークン サービス) と通信している可能性がある発行済みトークンのシナリオで特に便利です。 証明書に基づくメッセージ セキュリティを使用したバインドにおいて、この証明書を使用してサービスへのメッセージを暗号化します。サービスがクライアントへの応答に署名する際には、この証明書を使用することが要求されます。  
  
 バインディングにサービスの証明書が必要で、サービスの URL に対する特定の証明書が ScopedCertificates 内に存在しない場合は、既定の証明書が使用されます。  
  
 詳細について[は、「How to:フェデレーションクライアント](../../../wcf/feature-details/how-to-create-a-federated-client.md)を作成します。  
  
## <a name="example"></a>例  
 次の例は、コレクションに X.509 証明書を追加します。  
  
```xml  
<behaviors>
  <endpointBehaviors>
    <behavior name="MyEndpointBehavior">
      <clientCredentials>
        <serviceCertificate>
          <scopedCertificates>
            <add targetUri="http://www.contoso.com"
                 findValue="www.Contoso.com"
                 storeLocation="LocalMachine"
                 storeName="Root"
                 x509FindType="FindByIssuerName" />
          </scopedCertificates>
        </serviceCertificate>
      </clientCredentials>
    </behavior>
  </endpointBehaviors>
</behaviors>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement.ScopedCertificates%2A>
- <xref:System.ServiceModel.Configuration.X509ScopedServiceCertificateElementCollection>
- <xref:System.ServiceModel.Configuration.X509ScopedServiceCertificateElement>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.ScopedCertificates%2A>
- [方法: フェデレーションクライアントを作成する](../../../wcf/feature-details/how-to-create-a-federated-client.md)
- [証明書の使用](../../../wcf/feature-details/working-with-certificates.md)
- [クライアントのセキュリティ保護](../../../wcf/securing-clients.md)
- [サービスおよびクライアントのセキュリティ保護](../../../wcf/feature-details/securing-services-and-clients.md)
