---
title: <persistableType>
ms.date: 03/30/2017
ms.assetid: e5425fe6-523a-4076-aab4-2c2515b1d830
ms.openlocfilehash: fcfd338e289b5151688724f0e84b6878707d32be
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69933832"
---
# <a name="persistabletype"></a>\<persistableType >
すべての永続型を指定します。  
  
 \<system.ServiceModel >  
\<comContracts>  
\<comContract >  
  
## <a name="syntax"></a>構文  
  
```xml  
<comContracts>
  <comContract>
    <persistableTypes>
      <persistableType id="String"
                       name="String">
      </persistableType>
    </persistableTypes>
  </comContract>
</comContracts>
```  
  
## <a name="type"></a>型  
 `Type`  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|id|永続型の一意の ID を指定する文字列を含む必須属性。|  
|name|永続型の名前を指定する文字列を含む省略可能な属性。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<persistableTypes>](persistabletypes.md)|`persistableType` 要素のコレクション。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.ComPersistableTypeElementCollection>
- <xref:System.ServiceModel.Configuration.ComPersistableTypeElement>
- [\<comContracts>](comcontracts.md)
- [COM+ アプリケーションとの統合](../../../wcf/feature-details/integrating-with-com-plus-applications.md)
- [方法: COM + サービス設定の構成](../../../wcf/feature-details/how-to-configure-com-service-settings.md)
