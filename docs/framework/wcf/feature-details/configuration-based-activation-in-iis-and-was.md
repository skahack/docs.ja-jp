---
title: IIS と WAS における構成ベースのアクティブ化
ms.date: 03/30/2017
ms.assetid: 6a927e1f-b905-4ee5-ad0f-78265da38238
ms.openlocfilehash: f4de4aff2fbe6b8e82dc3d6523f492d06494c79e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69909770"
---
# <a name="configuration-based-activation-in-iis-and-was"></a>IIS と WAS における構成ベースのアクティブ化

通常、インターネットインフォメーションサービス (IIS) または Windows プロセスアクティブ化サービス (WAS) で Windows Communication Foundation (WCF) サービスをホストする場合は、.svc ファイルを指定する必要があります。 .svc ファイルには、サービスの名前と、オプションのカスタム サービス ホスト ファクトリが含まれています。 この追加ファイルによって、管理のオーバーヘッドが増加します。 構成ベースのアクティブ化機能により、.svc ファイルを用意する必要がなくなり、関連するオーバーヘッドも発生しません。

## <a name="configuration-based-activation"></a>構成ベースのアクティブ化

構成ベースのアクティブ化では、以前は .svc ファイルに配置されていたメタデータを受け取り、それを Web.config ファイルに配置します。 <`serviceHostingEnvironment`> 要素内に <`serviceActivations`> 要素があります。 <`serviceActivations`> 要素内には、ホストされる`add`サービスごとに1つの < > 要素が1つ以上含まれます。 <`add`の > 要素には、サービスの相対アドレス、サービスの種類、サービスホストファクトリを設定できる属性が含まれています。 次の構成コード例は、このセクションの使用方法を示しています。

> [!NOTE]
> 各 <`add`> 要素には、サービスまたはファクトリ属性を指定する必要があります。 サービスとファクトリ属性の両方を指定することもできます。

```xml
<serviceHostingEnvironment>
  <serviceActivations>
    <add relativeAddress="MyServiceAddress" service="Service" factory="MyServiceHostFactory"/>
  </serviceActivations>
</serviceHostingEnvironment>
```

 このコードを Web.config ファイルに含めると、サービス ソース コードをアプリケーションの App_Code ディレクトリに配置するか、コンパイル済みアセンブリをアプリケーションの Bin ディレクトリに配置することができます。

> [!NOTE]
> - 構成ベースのアクティブ化機能を使用する場合、.svc ファイルのインライン コードはサポートされません。
> - 属性には、"\<サブディレクトリ >/servicesub-directory" や "~/\</service .svc" などの相対アドレスを設定する必要があります。 `relativeAddress`
> - WCF と関連付けられている既知の拡張子を持たない相対アドレスを登録すると、構成例外がスローされます。
> - 指定された相対アドレスは、仮想アプリケーションのルートが基準になります。
> - 構成の階層的モデルにより、コンピューター レベルおよびサイト レベルの登録された相対アドレスは、仮想アプリケーションによって継承されます。
> - 構成ファイル内での登録は、.svc、.xamlx、.xoml、またはその他のファイルでの設定よりも優先されます。
> - IIS/WAS に送信された URI 内の \ (円記号) は、自動的に / (スラッシュ) に変換されます。 \ を含む相対アドレスが追加され、その相対アドレスを使用する URI を IIS に送信した場合は、円記号がスラッシュに変換されるため、IIS では、それを相対アドレスと一致させることができません。 IIS は、一致するものが見つからなかったことを示すトレース情報を送信します。

## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection.ServiceActivations%2A>
- [ホスティング サービス](../../../../docs/framework/wcf/hosting-services.md)
- [ワークフロー サービスのホストの概要](../../../../docs/framework/wcf/feature-details/hosting-workflow-services-overview.md)
- [\<serviceHostingEnvironment >](../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)
- [AppFabric のホスティング機能](https://go.microsoft.com/fwlink/?LinkId=201276)
