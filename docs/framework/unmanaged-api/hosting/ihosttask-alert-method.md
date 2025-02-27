---
title: IHostTask::Alert メソッド
ms.date: 03/30/2017
api_name:
- IHostTask.Alert
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTask::Alert
helpviewer_keywords:
- IHostTask::Alert method [.NET Framework hosting]
- Alert method, IHostTask interface [.NET Framework hosting]
ms.assetid: 5245d4b5-b6c3-48df-9cb9-8caf059f43fb
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 75b3fc0b1dde35e743e699d22c5766cab4cf0faf
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964717"
---
# <a name="ihosttaskalert-method"></a>IHostTask::Alert メソッド
現在の[IHostTask](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)インスタンスによって表されるタスクをホストがスリープ解除するように要求します。これにより、タスクを中止できます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Alert ();  
```  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドが正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドから E_FAIL が返された場合、そのプロセス内で CLR は使用できなくなります。 後続のホストメソッドの呼び出しでは、HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>Remarks  
 `Alert`がユーザー <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> コードから呼び出され<xref:System.Threading.Thread>た場合、または現在のに関連付けられているがシャットダウンした場合、CLRはメソッドを呼び出します。<xref:System.AppDomain> 呼び出しは非同期的に行われるため、ホストはすぐに制御を返す必要があります。 ホストがすぐにタスクを警告できない場合は、次にアラートが通知される状態になったときに起動する必要があります。  
  
> [!NOTE]
> `Alert`は、ランタイムが WAIT_ALERTABLE の[WAIT_OPTION](../../../../docs/framework/unmanaged-api/hosting/wait-option-enumeration.md)値を[Join](../../../../docs/framework/unmanaged-api/hosting/ihosttask-join-method.md)などのメソッドに渡すタスクにのみ影響します。  
  
## <a name="requirements"></a>必要条件  
 **・** [システム要件](../../../../docs/framework/get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ**Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRTask インターフェイス](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)
- [ICLRTaskManager インターフェイス](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask インターフェイス](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager インターフェイス](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
