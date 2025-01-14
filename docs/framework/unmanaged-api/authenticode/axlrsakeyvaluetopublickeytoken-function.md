---
title: _AxlRSAKeyValueToPublicKeyToken 関数
ms.date: 03/30/2017
api_name:
- _AxlRSAKeyValueToPublicKeyToken
api_location:
- clr.dll
api_type:
- DLLExport
ms.assetid: d60f19fe-7bec-47ba-b60e-ba9ce66abf8c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: eca6c5fc61d4f7e80046102a560d228fc01e5292
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69038410"
---
# <a name="_axlrsakeyvaluetopublickeytoken-function"></a>\_AxlRSAKeyValueToPublicKeyToken 関数

Modulus および Exponent を、厳密な名前の公開キー トークンに変換します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT _AxlRSAKeyValueToPublicKeyToken (  
    [in]  PCRYPT_DATA_BLOB pModulusBlob,  
    [in]  PCRYPT_DATA_BLOB pExponentBlob,  
    [out] LPWSTR           *ppwszPublicKeyToken  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pModulusBlob`  
 からBase64 でエンコードされた剰余 blob ( \<剰余 > 要素から)。  [CRYPTOAPI_BLOB](/windows/win32/api/dpapi/ns-dpapi-crypt_integer_blob)構造体を参照してください。  
  
 `pExponentBlob`  
 からBase64 でエンコードされた指数 ( \<指数 > 要素)。 [CRYPTOAPI_BLOB](/windows/win32/api/dpapi/ns-dpapi-crypt_integer_blob)構造体を参照してください。  
  
 `ppwszPublicKeyToken`  
 [out] 16 進エンコードされた公開キー トークンを受け取るための WCHAR * へのポインター。  
  
## <a name="return-value"></a>戻り値  
 関数が成功した場合は `S_OK`。 それ以外の場合はエラー コードを返します。  
  
## <a name="see-also"></a>関連項目

- [Authenticode](../../../../docs/framework/unmanaged-api/authenticode/index.md)
