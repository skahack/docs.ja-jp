---
title: <serviceSecurityAudit>
ms.date: 03/30/2017
ms.assetid: ba517369-a034-4f8e-a2c4-66517716062b
ms.openlocfilehash: a1fcc59550904a34eced8e87fa9bc54a334acd03
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69937170"
---
# <a name="servicesecurityaudit"></a>\<serviceSecurityAudit>
サービス操作中にセキュリティ イベントの監査を有効にする設定を指定します。  
  
 \<system.ServiceModel >  
\<<behaviors>  
\<serviceBehaviors>  
\<behavior>  
\<serviceSecurityAudit>  
  
## <a name="syntax"></a>構文  
  
```xml  
<serviceSecurityAudit auditLogLocation="Default/Application/Security"
                      messageAuthenticationAuditLevel="None/Success/Failure/SuccessOrFailure"
                      serviceAuthorizationAuditLevel="None/Success/Failure/SuccessOrFailure"
                      suppressAuditFailure="Boolean" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|auditLogLocation|監査ログの場所を指定します。 有効な値は次のとおりです。<br /><br /> 標準セキュリティイベントは、windows XP の場合はアプリケーションログに、windows Server 2003 および Windows Vista の場合はイベントログに書き込まれます。<br />適用監査イベントは、アプリケーションイベントログに書き込まれます。<br />保護監査イベントは、セキュリティイベントログに書き込まれます。<br /><br /> 既定値は Default です。 詳細については、「 <xref:System.ServiceModel.AuditLogLocation> 」を参照してください。|  
|suppressAuditFailure|監査ログへの書き込みエラーを非表示にする動作を指定します。<br /><br /> アプリケーションには、監査ログへの書き込みエラーを通知する必要があります。 アプリケーションが監査エラーを処理するように設計されていない場合は、この属性を使用して、監査ログへの書き込みでのエラーが表示されないようにする必要があります。<br /><br /> この属性が `true` の場合、監査イベントの書き込み試行の結果発生する例外 (ただし、OutOfMemoryException、StackOverFlowException、ThreadAbortException、および ArgumentException を除く) はシステムによって処理され、アプリケーションには伝達されません。 この属性が `false` の場合、監査イベントの書き込み試行の結果発生する例外は、すべてアプリケーションまで渡されます。<br /><br /> 既定値は `true` です。|  
|serviceAuthorizationAuditLevel|監査ログに記録される承認イベントの種類を指定します。 有効な値は次のとおりです。<br /><br /> 存在サービス承認イベントの監査は実行されません。<br />ブランド成功したサービス承認イベントだけが監査されます。<br />不具合失敗したサービス承認イベントだけが監査されます。<br />- SuccessOrFailure:成功と失敗の両方のサービス承認イベントが監査されます。<br /><br /> 既定値は None です。 詳細については、「 <xref:System.ServiceModel.AuditLevel> 」を参照してください。|  
|messageAuthenticationAuditLevel|ログに記録されるメッセージ認証監査イベントの種類を指定します。 有効な値は次のとおりです。<br /><br /> 存在監査イベントは生成されません。<br />ブランド成功したセキュリティ (メッセージ署名検証、暗号、トークン検証を含む完全な検証) イベントだけがログに記録されます。<br />不具合エラーイベントのみがログに記録されます。<br />- SuccessOrFailure:成功イベントと失敗イベントの両方がログに記録されます。<br /><br /> 既定値は None です。 詳細については、「 <xref:System.ServiceModel.AuditLevel> 」を参照してください。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|動作の要素を指定します。|  
  
## <a name="remarks"></a>Remarks  
 この構成要素は、Windows Communication Foundation (WCF) 認証イベントを監査するために使用されます。 監査を有効にすると、成功した認証、失敗した認証、またはその両方を監査できます。 イベントは、3 種類のイベント ログ (アプリケーション ログ、セキュリティ ログ、およびオペレーティング システムのバージョンに対する既定のログ) のいずれかに書き込まれます。 イベント ログはすべて、Windows イベント ビューアーを使用して表示できます。  
  
 この構成要素の使用例については、「[サービス監査の動作](../../../wcf/samples/service-auditing-behavior.md)」を参照してください。  
  
 監査イベントは既定で、Windows XP の場合はアプリケーション ログに、Windows Server 2003 と Windows Vista の場合はセキュリティ ログに表示されます。 監査イベントの場所は、`auditLogLocation` 属性を "Application" または "Security" に設定することによって指定できます。 詳細については、「[方法 :セキュリティイベント](../../../wcf/feature-details/how-to-audit-wcf-security-events.md)を監査します。 イベントがセキュリティログに書き込まれた場合は、LocalSecurityPolicy-> Enable オブジェクトアクセスを "Success" と "Failure" に設定する必要があります。  
  
 イベント ログを調べる場合、監査イベントのソースは "ServiceModel Audit 3.0.0.0" です。 メッセージ認証監査レコードには "MessageAuthentication" のカテゴリ、サービス承認監査レコードには "ServiceAuthorization" のカテゴリが設定されます。  
  
 メッセージ認証監査イベントは、メッセージの改ざんや期限切れの有無、クライアントによるサービス認証の成否などに適用されます。 このイベントでは、認証の成功または失敗に関する情報とクライアント ID、およびメッセージ送信先のエンドポイントとそのメッセージに関連付けられたアクションに関する情報が提供されます。  
  
 サービス承認監査イベントは、サービス承認マネージャーによって決定される承認に適用されます。 承認が成功したか失敗したかに関する情報を、クライアントの id、メッセージが送信されたエンドポイント、メッセージに関連付けられたアクション、およびから生成された承認コンテキストの識別子に関する情報を提供します。受信メッセージと、アクセスの決定を行った承認マネージャーの種類。  
  
## <a name="example"></a>例  
  
```xml  
<system.serviceModel>
  <behaviors>
    <serviceBehaviors>
      <behavior name="NewBehavior">
        <serviceSecurityAudit auditLogLocation="Application"
                              suppressAuditFailure="true"
                              serviceAuthorizationAuditLevel="Success"
                              messageAuthenticationAuditLevel="Success" />
      </behavior>
    </serviceBehaviors>
  </behaviors>
</system.serviceModel>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.ServiceSecurityAuditElement>
- <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>
- [セキュリティ動作](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [監査](../../../wcf/feature-details/auditing-security-events.md)
- [方法: セキュリティイベントの監査](../../../wcf/feature-details/how-to-audit-wcf-security-events.md)
- [サービス監査動作](../../../wcf/samples/service-auditing-behavior.md)
