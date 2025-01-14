---
title: NTLM 認証および Kerberos 認証
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- authentication [.NET Framework], NTLM
- authentication [.NET Framework], Kerberos
- user authentication, Kerberos
- user authentication, NTLM
- Kerberos authentication
- receiving data, authentication
- NTLM authentication
- Internet, authentication
- client authentication, Kerberos
- sending data, authentication
- network resources, authentication
- classes [.NET Framework], authentication
- client authentication, NTLM
ms.assetid: 9ef65560-f596-4469-bcce-f4d5407b55cd
ms.openlocfilehash: b05cd88fcb492ab27e1d311045b72208167508f1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963925"
---
# <a name="ntlm-and-kerberos-authentication"></a>NTLM 認証および Kerberos 認証
既定の NTLM 認証と Kerberos 認証は、呼び出し元のアプリケーションに関連付けられている Microsoft Windows NT ユーザー資格情報を使用して、サーバーで認証を試みます。 既定以外の NTLM 認証を使用する場合、アプリケーションは認証の種類を NTLM に設定し、次の例に示すように <xref:System.Net.NetworkCredential> オブジェクトを使用して、ユーザー名、パスワード、およびドメインをホストに渡します。  
  
```vb  
Dim MyURI As String = "http://www.contoso.com/"  
Dim WReq As WebRequest = WebRequest.Create(MyURI)  
WReq.Credentials = _  
    New NetworkCredential(UserName, SecurelyStoredPassword, Domain)  
```  
  
```csharp  
String MyURI = "http://www.contoso.com/";  
WebRequest WReq = WebRequest.Create (MyURI);  
WReq.Credentials =   
    new NetworkCredential(UserName, SecurelyStoredPassword, Domain);  
```  
  
 アプリケーション ユーザーの資格情報を使用してインターネット サービスに接続する必要があるアプリケーションは、次の例に示すように、ユーザーの既定の資格情報を使用してこれを行うことができます。  
  
```vb  
Dim MyURI As String = "http://www.contoso.com/"  
Dim WReq As WebRequest = WebRequest.Create(MyURI)  
WReq.Credentials = CredentialCache.DefaultCredentials  
```  
  
```csharp  
String MyURI = "http://www.contoso.com/";  
WebRequest WReq = WebRequest.Create (MyURI);  
WReq.Credentials = CredentialCache.DefaultCredentials;  
```  
  
 ネゴシエート認証モジュールは、リモート サーバーが NTLM 認証を使用しているか Kerberos 認証を使用しているかを確認し、適切な応答を送信します。  
  
> [!NOTE]
> NTLM 認証は、プロキシ サーバー経由では機能しません。  
  
## <a name="see-also"></a>関連項目

- [基本認証とダイジェスト認証](../../../docs/framework/network-programming/basic-and-digest-authentication.md)
- [インターネット認証](../../../docs/framework/network-programming/internet-authentication.md)
