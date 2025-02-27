---
title: ICorProfilerInfo4::RequestRevert メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.RequestRevert
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::RequestRevert
helpviewer_keywords:
- RequestRevert method, ICorProfilerInfo4 interface [.NET Framework profiling]
- ICorProfilerInfo4::RequestRevert method [.NET Framework profiling]
ms.assetid: 70261da5-5933-4e25-9de0-ddf51cba56cc
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 5e74cb663f968cc9b1b04a912307e3b4a12e86d4
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67748662"
---
# <a name="icorprofilerinfo4requestrevert-method"></a>ICorProfilerInfo4::RequestRevert メソッド
指定された関数のすべてのインスタンスを元のバージョンに戻します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT RequestRevert (  
   [in] ULONG    cFunctions,  
   [in, size_is(cFunctions)]  ModuleID    moduleIds[],  
   [in, size_is(cFunctions)]  mdMethodDef methodIds[],  
   [out, size_is(cFunctions)]  HRESULT status[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cFunctions`  
 [in] 元に戻す関数の数。  
  
 `moduleIds`  
 [in] 元に戻す関数を識別する (`module`、`methodDef`) ペアの `moduleId` の部分を指定します。  
  
 `methodIds`  
 [in] 元に戻す関数を識別する (`module`、`methodDef`) ペアの `methodId` の部分を指定します。  
  
 `status`  
 [out] このトピックの「状態 HRESULT」のセクションで後述する HRESULT の配列。 各 HRESULT は、並列配列 `moduleIds` と `methodIds` で指定された各関数を元に戻す操作の成功または失敗を示します。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|すべての要求を元に戻す操作が試行されました。ただし、返された状態配列を確認して、どの関数が正常に元に戻されたかを判断する必要があります。|  
|CORPROF_E_CALLBACK4_REQUIRED|プロファイラーを実装する必要があります、 [ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md)この呼び出しをサポートするためのインターフェイス。|  
|CORPROF_E_REJIT_NOT_ENABLED|JIT 再コンパイルが有効になっていませんでした。 使用して初期化中に JIT 再コンパイルを有効にする必要があります、 [icorprofilerinfo::seteventmask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md)を設定するメソッド、`COR_PRF_ENABLE_REJIT`フラグ。|  
|E_INVALIDARG|`cFunctions` が 0 であるか、`moduleIds` または `methodIds` が `NULL` です。|  
|E_OUTOFMEMORY|メモリが不足しているために、CLR は要求を完了できませんでした。|  
  
## <a name="status-hresults"></a>状態 HRESULT  
  
|状態配列 HRESULT|説明|  
|--------------------------|-----------------|  
|S_OK|対応する関数は正常に元に戻されました。|  
|E_INVALIDARG|`moduleID` パラメーターまたは `methodDef` パラメーターが `NULL` です。|  
|CORPROF_E_DATAINCOMPLETE|モジュールが完全に読み込まれていないか、またはアンロード中です。|  
|CORPROF_E_MODULE_IS_DYNAMIC|指定されたモジュールは (`Reflection.Emit` などにより) 動的に生成されました。 したがって、このメソッドではサポートされません。|  
|CORPROF_E_ACTIVE_REJIT_REQUEST_NOT_FOUND|CLR は、対応するアクティブな再コンパイル要求が見つからなかったために、指定された関数を元に戻すことができませんでした。 再コンパイルが要求されていないか、または関数は既に元に戻されています。|  
|Other|オペレーティング システムは、CLR 制御範囲外のエラーを返しました。 たとえば、メモリ ページのアクセスの保護を変更するシステム コールに失敗した場合、オペレーティング システムのエラーが表示されます。|  
  
## <a name="remarks"></a>Remarks  
 次に、元に戻された関数のいずれかのインスタンスが呼び出されると、その関数の元のバージョンが実行されます。 既に実行中の関数は、実行中のバージョンの実行を完了させます。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:** [システム要件](../../../../docs/framework/get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo4 インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-interface.md)
- [プロファイリングのインターフェイス](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [プロファイル](../../../../docs/framework/unmanaged-api/profiling/index.md)
