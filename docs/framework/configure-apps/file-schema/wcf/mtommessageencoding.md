---
title: <mtomMessageEncoding>
ms.date: 03/30/2017
ms.assetid: 7865d171-cd1e-430a-8421-39cc13541d1b
ms.openlocfilehash: 70a124fda5bc0e52e1271716f7e2166b7717b49a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69933198"
---
# <a name="mtommessageencoding"></a>\<mtomMessageEncoding >
SOAP Message Transmission Optimization Mechanism (MTOM) ベースのメッセージに使用されるエンコーディングおよびメッセージ バージョン管理を指定します。  
  
 \<system.serviceModel>  
\<bindings>  
\<customBinding>  
\<binding>  
\<mtomMessageEncoding >  
  
## <a name="syntax"></a>構文  
  
```xml  
<mtomMessageEncoding maxBufferSize="Integer"
                     maxReadPoolSize="Integer"
                     maxWritePoolSize="Integer"
                     messageVersion="Soap11Addressing1/Soap12Addressing10"
                     writeEncoding="UnicodeFffeTextEncoding/Utf16TextEncoding/Utf8TextEncoding" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|maxBufferSize|使用できるバッファーの最大サイズを指定する整数。|  
|maxReadPoolSize|新しいリーダーを割り当てずに同時に読み取り可能なメッセージの数を指定する整数です。 プール サイズを大きくすると、システムでは、比較的大きい作業セットで、アクティビティの急増に対する許容度が高まります。 既定値は 64 です。|  
|maxWritePoolSize|新しいライターを割り当てずに同時に送信可能なメッセージの数を指定する整数です。 プール サイズを大きくすると、システムでは、比較的大きい作業セットで、アクティビティの急増に対する許容度が高まります。 既定値は 16 です。|  
|messageVersion|バインディングを使用して送信されたメッセージの SOAP バージョンを指定します。 有効な値は、次のとおりです。<br /><br /> - Soap11Addressing1<br />- Soap12Addressing10<br /><br /> 既定値は Soap12Addressing10 です。 この属性は <xref:System.ServiceModel.Channels.MessageVersion> 型です。|  
|writeEncoding|バインドでメッセージの発行に使用される文字セット エンコーディングを指定します。 有効な値は、次のとおりです。<br /><br /> UnicodeFffeTextEncodingUnicode BigEndian エンコーディング<br />Utf16TextEncodingUnicode エンコーディング<br />Utf8TextEncoding8ビットエンコード<br /><br /> 既定値は Utf8TextEncoding です。 この属性は <xref:System.Text.Encoding> 型です。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<readerQuotas>](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|このバインドを使用して設定されるエンドポイントにより処理可能な、SOAP メッセージの複雑さに対する制約を定義します。 この要素は <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement> 型です。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<binding>](../../../misc/binding.md)|カスタム バインドのすべてのバインド機能を定義します。|  
  
## <a name="remarks"></a>Remarks  
 エンコーディングは、メッセージをバイト シーケンスに変換するプロセスです。 デコードは、その逆のプロセスです。 Windows Communication Foundation (WCF) には、SOAP メッセージの3種類のエンコードが含まれています。テキスト、バイナリ、およびメッセージ転送の最適化メカニズム (MTOM)。  
  
 `MtomMessageEncoding` 要素は、MTOM (Message Transmission Optimization Mechanism) エンコーディングを使用するメッセージの文字エンコーディング、メッセージのバージョン管理、およびその他の設定を指定します。 MTOM は、WCF メッセージでバイナリ データを転送するための効率的なテクノロジです。 MTOM エンコーダーは、効率と相互運用性のバランスをとろうとします。 MTOM エンコーディングは、ほとんどの XML をテキスト形式で転送しますが、大きいサイズのバイナリ データ ブロックは、base64 でエンコードされた形式に変換せずに、そのまま転送することによって最適化します。  
  
## <a name="example"></a>例  
  
```xml  
<mtomMessageEncoding maxReadPoolSize="211"
                     maxWritePoolSize="2132"
                     messageVersion="Soap11Addressing10"
                     textEncoding="utf-8" />
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.MtomMessageEncodingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>
- <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>
- [メッセージ エンコーディング](message-encoding.md)
- [メッセージ エンコーダーを選択する](../../../wcf/feature-details/choosing-a-message-encoder.md)
- [バインディング](../../../wcf/bindings.md)
- [バインディングの拡張](../../../wcf/extending/extending-bindings.md)
- [カスタム バインディング](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
