---
title: LoadLibraryShim 関数
ms.date: 03/30/2017
api_name:
- LoadLibraryShim
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- LoadLibraryShim
helpviewer_keywords:
- LoadLibraryShim function [.NET Framework hosting]
ms.assetid: 30931874-4d0e-4df1-b3d1-e425b50655d1
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9ab44ce8f51620d83084d1dd16e98b2b310feb76
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968938"
---
# <a name="loadlibraryshim-function"></a>LoadLibraryShim 関数
再頒布可能パッケージ .NET Framework に含まれている、指定したバージョンの DLL を読み込みます。  
  
 この関数は .NET Framework 4 で非推奨とされました。 代わりに[ICLRRuntimeInfo:: LoadLibrary](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-loadlibrary-method.md)メソッドを使用してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT LoadLibraryShim (  
    [in]  LPCWSTR  szDllName,  
    [in]  LPCWSTR  szVersion,  
          LPVOID   pvReserved,  
    [out] HMODULE *phModDll  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `szDllName`  
 から.NET Framework ライブラリから読み込む DLL の名前を表す、0で終わる文字列です。  
  
 `szVersion`  
 から読み込む DLL のバージョンを表す、0で終わる文字列。 が`szVersion` null の場合、読み込み用に選択されたバージョンは、指定された DLL のうち、バージョン4より小さい最新バージョンです。 つまり、が null の場合`szVersion` 、バージョン4以上のすべてのバージョンは無視されます。バージョン4より前のバージョンがインストールされていない場合は、DLL の読み込みに失敗します。 これは、.NET Framework 4 のインストールが、既存のアプリケーションまたはコンポーネントに影響しないようにするためです。 CLR チームブログの「[インプロセス SxS And Migration クイックスタート](https://go.microsoft.com/fwlink/?LinkId=200329)」のエントリを参照してください。  
  
 `pvReserved`  
 将来使用するために予約されています。  
  
 `phModDll`  
 入出力モジュールのハンドルへのポインター。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の値に加えて、Winerror.h で定義されている標準のコンポーネントオブジェクトモデル (COM) エラーコードを返します。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|CLR_E_SHIM_RUNTIMELOAD|読み込み`szDllName`には共通言語ランタイム (clr) を読み込む必要があり、必要なバージョンの clr を読み込むことはできません。|  
  
## <a name="remarks"></a>Remarks  
 この関数は、.NET Framework 再頒布可能パッケージに含まれている Dll を読み込むために使用されます。 ユーザーが生成した Dll は読み込まれません。  
  
> [!NOTE]
> .NET Framework バージョン2.0 以降では、Fusion .dll を読み込むと CLR が読み込まれます。 これは、Fusion の関数が、ランタイムによって実装されているラッパーであるためです。  
  
## <a name="requirements"></a>必要条件  
 **・** [システム要件](../../../../docs/framework/get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [非推奨の CLR ホスト関数](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
