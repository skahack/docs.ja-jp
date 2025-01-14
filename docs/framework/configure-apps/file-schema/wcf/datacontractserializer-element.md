---
title: <dataContractSerializer>
ms.date: 03/30/2017
helpviewer_keywords:
- dataContractSerializer element
- <dataContractSerializer> element
- DataContractSerializer
- KnownTypes
ms.assetid: f41fb4d5-24e7-4059-8010-286a30bfea93
ms.openlocfilehash: 7e440810fee1dddb7025d1385b1edb4838d98a39
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69925909"
---
# <a name="datacontractserializer"></a>\<dataContractSerializer >
<xref:System.Runtime.Serialization.DataContractSerializer> 用の設定データが含まれています。 この要素は、2 つの異なる階層で使用されます。 1 つは以下の「スキーマの階層」に示したもので、もう 1 つは「解説」に記載しています。  
  
 \<system.ServiceModel >  
\<<behaviors>  
\<serviceBehaviors>  
\<behavior>  
\<dataContractSerializer >  
  
## <a name="syntax"></a>構文  
  
```xml  
<dataContractSerializer ignoreExtensionDataObject="Boolean"
                        maxItemsInObjectGraph="Integer" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|要素|説明|  
|-------------|-----------------|  
|ignoreExtensionDataObject|エンドポイントがシリアル化または逆シリアル化されているときに、そのエンドポイントにより提供されるデータを無視するかどうかを指定するブール値。 この属性は、`<dataContractSerializer>` 要素の下の `<behavior>` でのみ設定可能です。|  
|maxItemsInObjectGraph|シリアル化または逆シリアル化する項目の最大数を指定する整数。 この属性は 65536 です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-servicebehaviors.md)|サービスの動作設定のコレクション。|  
|[\<system.runtime.serialization >](system-runtime-serialization.md)|<xref:System.Runtime.Serialization> 名前空間セクションのルート要素を表し、<xref:System.Runtime.Serialization.DataContractSerializer> のオプションを設定するための要素を含みます。|  
  
## <a name="remarks"></a>Remarks  
 このトピックの冒頭で述べたように、これは\<X509Extension > 要素が発生する2番目の階層です。  
  
 [\<system.runtime.serialization >](system-runtime-serialization.md)  
  
 [\<dataContractSerializer >](datacontractserializer-element.md)  
  
 既知の型の詳細については、<xref:System.Runtime.Serialization.DataContractSerializer> を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>
- <xref:System.ServiceModel.Configuration.DataContractSerializerElement>
- [既知のデータ コントラクト型](../../../wcf/feature-details/data-contract-known-types.md)
- [データ転送とシリアル化](../../../wcf/feature-details/data-transfer-and-serialization.md)
