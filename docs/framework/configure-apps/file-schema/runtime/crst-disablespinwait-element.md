---
title: < Crst_DisableSpinWait > 要素
ms.date: 04/18/2019
f1_keywords:
- Crst_DisableSpinWait
helpviewer_keywords:
- Crst_DisableSpinWait element
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a52dd671f1fbf6fda5bdc92c0935784181eb4b03
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69663840"
---
# <a name="crst_disablespinwait-element"></a>\<Crst_DisableSpinWait > 要素

競合の多い場合、クリティカル セクションのスピン待機時間を無効にするかどうかを指定します。  
  
 \<configuration>  
\<ランタイム >  
\<Crst_DisableSpinWait >  
  
## <a name="syntax"></a>構文  
  
```xml  
<Crst_DisableSpinWait enabled="true | false"/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素

以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|**enabled**|重要なセクションが競合している場合は、スピンを待機するかどうかを指定します。|  
  
## <a name="enabled-attribute"></a>enabled 属性  
  
|値|説明|  
|-----------|-----------------|  
|1|クリティカルセクションを取得できないときに、スピン待機を無効にします。|  
|0|クリティカルセクションを取得できない場合は、スピン待機を無効にしないでください。 これが既定値です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`runtime`|さまざまなランタイム構成設定に関する情報が含まれています。|  
  
## <a name="example"></a>例  

次の例では、重要なセクションで、競合がある場合、スピン待機を無効にします。  
  
```xml  
<configuration>  
   <runtime>  
      <Crst_DisableSpinWait enabled="1"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [ランタイム設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
