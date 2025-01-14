---
title: SQL Server でのアプリケーション ロールの作成
ms.date: 03/30/2017
ms.assetid: 27442435-dfb2-4062-8c59-e2960833a638
ms.openlocfilehash: e7060e1b171ee1791b9986250fe6f2050ec77acd
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69961165"
---
# <a name="creating-application-roles-in-sql-server"></a>SQL Server でのアプリケーション ロールの作成
アプリケーション ロールは、データベース ロールやユーザーに対してではなく、アプリケーションに権限を割り当てる手段です。 ユーザーはデータベースに接続し、アプリケーション ロールをアクティブ化して、そのアプリケーションに付与された権限を使用することになります。 アプリケーション ロールに付与された権限は、接続している間のみ有効です。  
  
> [!IMPORTANT]
> アプリケーション ロールは、クライアント アプリケーションが接続文字列でアプリケーション ロール名とパスワードを渡すことによってアクティブ化されます。 2 層アプリケーションでは、パスワードをクライアント コンピューターに保存する必要があるため、セキュリティ上の脆弱性を伴います。 3 層アプリケーションでは、アプリケーションのユーザーがアクセスできないような形でパスワードを保存できます。  
  
## <a name="application-role-features"></a>アプリケーション ロールの特徴  
 アプリケーション ロールには次の特徴があります。  
  
- データベース ロールとは異なり、アプリケーション ロールはメンバーを持ちません。  
  
- アプリケーション ロールは、アプリケーションが `sp_setapprole` システム ストアド プロシージャにアプリケーション ロール名とパスワードを渡すことによってアクティブ化されます。  
  
- パスワードはクライアント コンピューターに保存しておき、実行時に渡す必要があります。アプリケーション ロールを SQL Server 内からアクティブ化することはできません。  
  
- パスワードは暗号化されません。 パラメーターのパスワードが一方向のハッシュとして保存されます。  
  
- アクティブ化後、アプリケーション ロールを使用して取得した権限は、接続している間のみ有効です。  
  
- アプリケーション ロールは、`public` ロールに付与された権限を継承します。  
  
- アプリケーション ロールが `sysadmin` 固定サーバー ロールのメンバーによってアクティブ化された場合、セキュリティ コンテキストは、接続している間、アプリケーション ロールのセキュリティ コンテキストに切り替わります。  
  
- アプリケーション ロールを持ったデータベースに `guest` アカウントを作成した場合、そのアプリケーション ロールまたはそれを呼び出すログインに対するデータベース ユーザー アカウントを作成する必要はありません。 別のデータベースに `guest` アカウントが存在する場合は、アプリケーション ロールでそのデータベースに直接アクセスできます。  
  
- SYSTEM_USER など、ログイン名を返す組み込み関数を実行した場合、アプリケーション ロールを呼び出したログイン名が返されます。 データベース ユーザー名を返す組み込み関数を実行した場合、アプリケーション ロールの名前が返されます。  
  
### <a name="the-principle-of-least-privilege"></a>最小特権の原則  
 パスワードが漏洩した場合に備えて、アプリケーション ロールには必要な権限だけを付与してください。 アプリケーション ロールを使ったデータベースでは、`public` ロールに対する権限は取り消す必要があります。 アプリケーション ロールの呼び出し元が特定のデータベースにアクセスできないようにするには、そのデータベースの `guest` アカウントを無効にします。  
  
### <a name="application-role-enhancements"></a>アプリケーション ロールの機能強化  
 アプリケーション ロールをアクティブ化した後で実行コンテキストを元の呼び出し元に戻すことができるため、接続プールを無効にする必要はありません。 呼び出し元のコンテキスト情報を格納するクッキーを作成するための新しいオプションが `sp_setapprole` プロシージャに追加されています。 `sp_unsetapprole` プロシージャにそのクッキーを渡して呼び出すことによって、元のセッションに切り替えることができます。  
  
## <a name="application-role-alternatives"></a>アプリケーション ロールに代わる方法  
 アプリケーション ロールはパスワードのセキュリティに依存する関係上、セキュリティ上の脆弱性を伴います。 パスワードをアプリケーション コードに組み込んだり、ディスクに保存したりすると、パスワードが漏洩する可能性があります。  
  
 以下の代替策を検討する必要があります。  
  
- EXECUTE AS ステートメントに NO REVERT 句と WITH COOKIE 句を指定してコンテキスト切り替えを行う。 ログインにマップされていないユーザー アカウントをデータベースに作成し、 このアカウントに権限を割り当てるようにします。 EXECUTE AS はパスワード ベースではなく、権限ベースであるため、非ログイン ユーザーで使用した方が高いセキュリティを確保できます。 詳細については、「 [SQL Server で権限借用を使用してアクセス許可をカスタマイズ](../../../../../docs/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server.md)する」を参照してください。  
  
- 証明書を使ってストアド プロシージャに署名し、そのプロシージャを実行するのに必要な権限だけを付与する。 詳細については、「 [SQL Server でのストアドプロシージャ](../../../../../docs/framework/data/adonet/sql/signing-stored-procedures-in-sql-server.md)への署名」を参照してください。  
  
## <a name="external-resources"></a>外部リソース  
 詳細については、次のリソースを参照してください。  
  
|リソース|説明|  
|--------------|-----------------|  
|[アプリケーションロール](/sql/relational-databases/security/authentication-access/application-roles)|SQL Server 2008 でアプリケーション ロールを作成および使用する方法について説明します。|  
  
## <a name="see-also"></a>関連項目

- [ADO.NET アプリケーションのセキュリティ保護](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)
- [SQL Server セキュリティの概要](../../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)
- [SQL Server におけるアプリケーション セキュリティのシナリオ](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)
- [ADO.NET のマネージド プロバイダーと DataSet デベロッパー センター](https://go.microsoft.com/fwlink/?LinkId=217917)
