---
title: <bookmarkResumptionQueries>WCF の
ms.date: 03/30/2017
ms.assetid: ed086712-1dc7-4932-a592-d1116a0155f3
ms.openlocfilehash: 5ec9827e9862866096265da576c91b10573012d1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69919734"
---
# <a name="bookmarkresumptionqueries-of-wcf"></a>\<WCF の bookmarkResumptionQueries >
  
ワークフロー インスタンス内のブックマークの再開を追跡するために使用する、クエリのコレクションを表します。 追跡参加要素がブックマーク再開レコードを定期受信するには、このクエリが必要です。  
  
追跡プロファイルのクエリの詳細については、「[追跡プロファイル](../../../windows-workflow-foundation/tracking-profiles.md)」を参照してください。
  
\<system.serviceModel>  
\<追跡 >  
\<プロファイル >  
\<trackingProfile>  
\<ワークフロー >  
\<bookmarkResumptionQueries >  
\<bookmarkResumptionQuery >  
  
## <a name="syntax"></a>構文  
  
```xml  
<tracking>
  <profiles>
    <trackingProfile name="Name">
      <workflow>
        <bookmarkResumptionQueries>
          <bookmarkResumptionQuery name="String" />
        </bookmarkResumptionQueries>
      </workflow>
    </trackingProfile>
  </profiles>
</tracking>
```  
  
## <a name="attributes-and-elements"></a>属性と要素  
  
以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
なし。  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<bookmarkResumptionQuery>](bookmarkresumptionquery-of-wcf.md)|ワークフロー インスタンス内のブックマークの再開を追跡するために使用されるクエリ。 追跡参加要素がブックマーク再開レコードを定期受信するには、このクエリが必要です。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<workflow>](../windows-workflow-foundation/workflow.md)|`activityDefinitionId` プロパティによって識別される特定のワークフローのすべてのクエリを格納する構成要素。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Activities.Tracking.Configuration.BookmarkResumptionQueryElementCollection?displayProperty=nameWithType>
- <xref:System.Activities.Tracking.BookmarkResumptionQuery?displayProperty=nameWithType>
- [ワークフローの追跡とトレース](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [追跡プロファイル](../../../windows-workflow-foundation/tracking-profiles.md)
