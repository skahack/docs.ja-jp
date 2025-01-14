---
title: <localClientSettings> 要素
ms.date: 03/30/2017
ms.assetid: 4680ace5-f4e1-4fcb-b9d8-a4a4af5cd7ae
ms.openlocfilehash: e7331105582a4a48b7edd8cd4f6a691771b0b8ff
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69930795"
---
# <a name="localclientsettings-element"></a>\<localClientSettings > 要素
このバインディングのローカル クライアントのセキュリティ設定を指定します。  
  
 \<system.serviceModel>  
\<bindings>  
\<customBinding>  
\<binding>  
\<セキュリティ >  
  
## <a name="syntax"></a>構文  
  
```xml  
<security>
   <localClientSettings cacheCookies="Boolean"
                        cookieRenewalThresholdPercentage="Integer"
                        detectReplays="Boolean"
                        maxClockSkew="TimeSpan"
                        maxCookieCachingTime="TimeSpan"
                        reconnectTransportOnFailure="Boolean"
                        replayCacheSize="Integer"
                        replayWindow="TimeSpan"
                        sessionKeyRenewalInterval="TimeSpan"
                        sessionKeyRolloverInterval="TimeSpan"
                        timestampValidityDuration="TimeSpan" />
</security>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`cacheCookies`|クッキーのキャッシュが有効かどうかを示すブール値。 既定値は `false` です。|  
|`cookieRenewalThresholdPercentage`|更新できるクッキーの最大パーセンテージを指定する整数。 この値は、0 ～ 100 (0 と 100を含む) のいずれかです。 既定値は 90 です。|  
|`detectReplays`|チャネルに対するリプレイ攻撃を検出し、自動的に処理するかどうかを指定するブール値です。 既定値は `false` です。|  
|`maxClockSkew`|通信している双方の 2 つのシステム クロックのずれの最長時間を指定する <xref:System.TimeSpan>。 既定値は、"00:05:00" です。<br /><br /> この値が既定値に設定されている場合、受信側はメッセージが受信された時間より前後最大 5 分間の送信時間タイム スタンプを持つメッセージを受け入れます。 送信時間テストにパスしないメッセージは拒否されます。 この設定は、`replayWindow` 属性と組み合わせて使用します。|  
|`maxCookieCachingTime`|クッキーの最長有効期間を指定する <xref:System.TimeSpan>。 デフォルト値は "10675199.02:48:05.4775807" です。|  
|`reconnectTransportOnFailure`|WS-ReliableMessaging を使用した接続が、トランスポート エラーの後再接続を試みるかどうかを指定するブール値です。 既定値は `true` です。これは、再接続の試行が無限に行われることを意味します。 循環は非アクティブ タイムアウトにより破棄され、再接続できない場合はチャネルが例外をスローします。|  
|`replayCacheSize`|リプレイ検証で使用される、キャッシュ済みの nonce 数を指定する正の整数。 この制限を越えると、最も古い nonce が削除され、新しいメッセージ用に新しい nonce が作成されます。 既定値は 500000 です。|  
|`replayWindow`|個別のメッセージ nonce の有効期間を指定する <xref:System.TimeSpan>。<br /><br /> この期間が過ぎると、以前に送信されたメッセージと同じ nonce を持つメッセージは受け入れられません。 この属性は、リプレイ攻撃を防ぐために `maxClockSkew` 属性と組み合わせて使用します。 攻撃者は、メッセージのリプレイ ウィンドウの期限が切れた後にメッセージをリプレイする可能性があります。 ただし、このメッセージは `maxClockSkew` テストに失敗します。このテストは、メッセージが受信された時間の前後指定時間以内の送信時間タイムスタンプを持つメッセージを拒否します。|  
|`sessionKeyRenewalInterval`|イニシエーターがセキュリティ セッションのキーを更新するまでの期間を指定する <xref:System.TimeSpan>。 既定値は "10:00:00" です。|  
|`sessionKeyRolloverInterval`|キーの更新中に、前のセッション キーが受信メッセージで有効な時間間隔を指定する <xref:System.TimeSpan> です。 既定値は "00:05:00" です。<br /><br /> キーの更新中、クライアントおよびサーバーは、常に、利用可能な最新のキーを使用してメッセージを送信する必要があります。 どちらのパーティも、ロールオーバー時間に達するまで、前のセッション キーで保護された受信メッセージを受け入れます。|  
|`timestampValidityDuration`|タイムスタンプの有効期間を指定する正の <xref:System.TimeSpan>。 既定値は "00:15:00" です。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<security>](security-of-custombinding.md)|カスタム バインドのセキュリティ オプションを指定します。|  
|[\<secureConversationBootstrap>](secureconversationbootstrap.md)|セキュリティで保護されたメッセージ交換サービスの開始に使用される既定値を指定します。|  
  
## <a name="remarks"></a>Remarks  
 この設定は、サービスのセキュリティ ポリシーから派生する設定ではないという点でローカルです。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.LocalClientSecuritySettingsElement>
- <xref:System.ServiceModel.Configuration.SecurityElementBase.LocalClientSettings%2A>
- <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalClientSettings%2A>
- <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [バインディング](../../../wcf/bindings.md)
- [バインディングの拡張](../../../wcf/extending/extending-bindings.md)
- [カスタム バインディング](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
- [方法: 設定を使用してカスタムバインディングを作成する](../../../wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [カスタム バインド セキュリティ](../../../wcf/samples/custom-binding-security.md)
