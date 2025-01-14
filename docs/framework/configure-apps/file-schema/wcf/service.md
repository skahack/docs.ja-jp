---
title: <service>
ms.date: 03/30/2017
ms.assetid: 13123dd6-c4a9-4a04-a984-df184b851788
ms.openlocfilehash: 69f3c70514fc2bcab1b4ef6a45036de98d1af7b7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69936521"
---
# <a name="service"></a>\<サービス >
`service` 要素には Windows Communication Foundation (WCF) サービスの設定が含まれます。 また、サービスを公開するエンドポイントも含まれます。  
  
 \<system.ServiceModel >  
\<services>  
\<サービス >  
  
## <a name="syntax"></a>構文  
  
```xml  
<service behaviorConfiguration="String"
         name="String">
</service>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|behaviorConfiguration|サービスのインスタンス化に使用される動作の動作名を含む文字列。 動作名は、サービスが定義される時点でスコープ内にある必要があります。 既定値は空の文字列です。|  
|name|インスタンス化するサービスの型を指定する必須の文字列属性。 この設定は有効な型と同じでなければなりません。 形式は、`Namespace.Class.` です。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<endpoint>](endpoint-element.md)|このサービスを公開する `endpoint` 要素のコレクション。|  
|[\<ホスト >](host.md)|このサービス インスタンスのホストを指定します。 この要素は <xref:System.ServiceModel.Configuration.HostElement> 型です。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<services>](services.md)|すべての WCF 構成要素のルート要素です。|  
  
## <a name="remarks"></a>Remarks  
 サービスは、設定ファイルの `services` セクションで定義されます。 アセンブリには、任意の数のサービスを含めることができます。 各サービスには、独自の `service` 設定セクションがあります。 このセクションとその内容は、サービス コントラクト、動作、および特定のサービスのエンドポイントを定義します。  
  
 `behaviorConfiguration` 要素も省略可能です。 サービスが使用する動作を識別します。 この属性で指定された動作は、同じ設定ファイルの範囲にある動作にリンクしている必要があります。  
  
 各サービスでは、固有のアドレスとバインディングを持つ 1 つまたは複数のエンドポイントが公開されます。 構成ファイル内で使用されるすべてのバインディングは、そのファイルのスコープ内で定義される必要があります。 バインディングは、`name` 属性と `bindingConfiguration` 属性の組み合わせによってエンドポイントにリンクされます。 `name` 属性は、バインディングが定義されているセクションを示します。 `bindingConfiguration` 属性は、バインディング セクション内の使用される構成を定義します。 バインディング セクションでは、複数の設定を定義できます。  
  
## <a name="example"></a>例  
 これはサービスの構成の例です。  
  
```xml  
<service behaviorConfiguration="testChannelBehavior"
         name="HelloWorld">
  <endpoint address="/HelloWorld2/"
            name="test"
            bindingNamespace="http://www.cohowinery.com/"
            binding="basicHttpBinding"
            contract="IHelloWorld" />
</service>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.ServiceElement>
- [サービスの構成](../../../wcf/configuring-services.md)
