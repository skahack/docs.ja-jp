---
title: ICLRDebugManager::BeginConnection メソッド
ms.date: 03/30/2017
api_name:
- ICLRDebugManager.BeginConnection
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDebugManager::BeginConnection
helpviewer_keywords:
- ICLRDebugManager::BeginConnection method [.NET Framework hosting]
- BeginConnection method [.NET Framework hosting]
ms.assetid: bdd98146-ff4d-4150-a264-a4c1a32d31f3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 37e663cbad902b5740a14b9fe60f24537d999aac
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969433"
---
# <a name="iclrdebugmanagerbeginconnection-method"></a>ICLRDebugManager::BeginConnection メソッド
ホストとデバッガーの間の新しい接続を確立して、タスクの一覧を識別子とフレンドリ名に関連付けます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT BeginConnection (  
    [in] CONNID dwConnectionId,  
    [in, string] wchar_t* szConnectionName  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwConnectionId`  
 から共通言語ランタイム (CLR) タスクのリストに関連付ける識別子。  
  
 `szConnectionName`  
 からCLR タスクの一覧に関連付けるフレンドリ名。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`BeginConnection`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドから E_FAIL が返された後は、そのプロセス内で CLR を使用できなくなります。 後続のホストメソッドの呼び出しでは、HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_INVALIDARG|`dwConnectionId`が0である`BeginConnection`か、既にこの`dwConnectionId`値を使用`szConnectionName`して呼び出されたか、またはが null でした。|  
|E_OUTOFMEMORY|この接続に関連付けられたタスクの一覧を保持するために十分なメモリを割り当てることができません。|  
  
## <a name="remarks"></a>Remarks  
 [ICLRDebugManager](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-interface.md)には`BeginConnection`、、 [setconnectiontasks](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-setconnectiontasks-method.md)、 [endconnection](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-endconnection-method.md)という3つのメソッドが用意されており、タスクリストを識別子と表示名に関連付けることができます。  
  
> [!IMPORTANT]
> これら3つのメソッドは、一連のタスクごとに特定の順序で呼び出す必要があります。 `BeginConnection`は、新しい接続を確立するために最初に呼び出されます。 `SetConnectionTasks`は、その接続に関連する一連のタスクを提供するために、次に呼び出されます。 `EndConnection`は、タスク一覧と識別子とフレンドリ名の間の関連付けを削除するために最後に呼び出されます。ただし、異なる接続の呼び出しは入れ子にすることができます。  
  
## <a name="requirements"></a>必要条件  
 **・** [システム要件](../../../../docs/framework/get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ**Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRControl インターフェイス](../../../../docs/framework/unmanaged-api/hosting/iclrcontrol-interface.md)
- [ICLRDebugManager インターフェイス](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-interface.md)
- [EndConnection メソッド](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-endconnection-method.md)
- [SetConnectionTasks メソッド](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-setconnectiontasks-method.md)
- [IHostControl インターフェイス](../../../../docs/framework/unmanaged-api/hosting/ihostcontrol-interface.md)
