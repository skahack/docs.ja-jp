---
title: <parameter>
ms.date: 03/30/2017
ms.assetid: 0fb41e2d-64f7-44ab-993e-05892eac6d82
ms.openlocfilehash: c3f2179835ad1232e115cad0decdd3d41bbdc160
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69932847"
---
# <a name="parameter"></a>\<パラメーター >
宣言された型がジェネリック型である場合、ジェネリック パラメーターを指定します。  
  
 \<system.runtime.serialization>  
\<dataContractSerializer >  
\<declaredTypes > 要素  
\<declaredTypes > の > \<要素の追加  
\<knownType > 要素  
\<parameter > 要素  
  
## <a name="syntax"></a>構文  
  
```xml  
<parameter index="Integer"
           type="String" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|インデックス|宣言された型がジェネリック型である場合、既知の型を返すジェネリック パラメーターを指定します。|  
|型|シリアル化と逆シリアル化で使用される既知の型を説明する文字列。|  
  
## <a name="index-attribute"></a>index 属性  
  
|値|説明|  
|-----------|-----------------|  
|"0"|ジェネリック型の最初のパラメーター。 たとえば、<xref:System.Collections.Generic.List%601> にはパラメーターが 1 つだけあります。 宣言型として使用される場合、index は "0" に設定されます。|  
|"1"|ジェネリック型の 2 番目のパラメーター。 たとえば、<xref:System.Collections.Generic.Dictionary%602> には 2 つのパラメーターがあります。 2 番目のパラメーターによって既知の型が返される場合は、index 属性を "1" に設定します。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<knownType >](knowntype.md)|宣言型のフィールドまたはプロパティによって返される既知の型を指定します。|  
  
## <a name="remarks"></a>Remarks  
 既知の型の詳細については、「[データコントラクトの既知の型](../../../wcf/feature-details/data-contract-known-types.md)」と<xref:System.Runtime.Serialization.DataContractSerializer>「」を参照してください。  
  
 この要素の使用例については、 [ \<dataContractSerializer >](datacontractserializer-element.md)を参照してください。  
  
 この構成要素に、両方の属性を同時に設定することはできません。 両方の属性が設定された場合、<xref:System.Configuration.ConfigurationErrorsException> が発生します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.DataContractSerializer>
- [既知のデータ コントラクト型](../../../wcf/feature-details/data-contract-known-types.md)
- [\<dataContractSerializer >](datacontractserializer-element.md)
- [\<add>](add-of-declaredtypes-element.md)
