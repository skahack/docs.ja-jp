---
title: 厳密な名前付きアセンブリ
ms.date: 03/30/2017
helpviewer_keywords:
- strong-named assemblies, about strong-named assemblies
- assemblies [.NET Framework], strong-named
ms.assetid: d4a80263-f3e0-4d81-9b61-f0cbeae3797b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f283aad7c6727aff111aaaf78beb1e8da4b45898
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988372"
---
# <a name="strong-named-assemblies"></a>厳密な名前付きアセンブリ
アセンブリの厳格な名前付けにより、アセンブリに対して一意の ID を作成し、アセンブリの競合を防ぐことができます。  
  
## <a name="what-makes-a-strong-named-assembly"></a>厳格な名前付きのアセンブリを作成する方法  
 厳格な名前付きのアセンブリは、アセンブリと一緒に配布された公開キーに対応する秘密キーとアセンブリ自体を使用して生成されます。 アセンブリには、アセンブリ マニフェストが含まれます。ここには、アセンブリを構成するすべてのファイルの名前とハッシュが格納されています。 同じ厳格な名前を持つ複数のアセンブリは、同一である必要があります。  
  
 Visual Studio またはコマンド ライン ツールを使用して、アセンブリに厳格な名前を付けることができます。 詳細については、「[方法 :厳密な名前でアセンブリに署名する](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md)」または「[Sn.exe (厳密な名前ツール)](../../../docs/framework/tools/sn-exe-strong-name-tool.md)」 を参照してください。  
  
 厳格に名前付けされたアセンブリには、アセンブリの単純テキスト名、バージョン番号、カルチャ情報 (省略可能)、デジタル署名、および署名に使用する秘密キーに対応した公開キーが含まれています。  
  
> [!WARNING]
> セキュリティに関しては、厳格な名前に依存しないでください。 厳格な名前は、一意の ID を提供するだけです。  
  
## <a name="why-strong-name-your-assemblies"></a>アセンブリに厳格な名前を付ける理由  
 厳密な名前付きのアセンブリを参照すると、バージョン管理や名前の一意性を保護できるなどの利点を期待できます。 厳密な名前付きのアセンブリは、一部のシナリオを有効にするために必要な、グローバル アセンブリ キャッシュにインストールできます。  
  
 厳格な名前付きのアセンブリは次のシナリオで役立ちます。  
  
- 独自のアセンブリを厳密な名前付きのアセンブリが参照できるようにする場合、または他の厳密な名前付きのアセンブリから独自のアセンブリへの `friend` アクセスを可能にする場合。  
  
- 同じアセンブリのさまざまなバージョンにアプリがアクセスする必要がある場合。 これは、競合することなく同じアプリ ドメインで side-by-side の読み込みを実行するために、アセンブリのさまざまなバージョンが必要であることを意味します。 たとえば、同じ簡易名を持つアセンブリ内に API のさまざまな拡張子が存在する場合、厳格な名前付けはアセンブリの各バージョンに一意の ID を提供します。  
  
- 独自のアセンブリを使用するアプリのパフォーマンスに悪影響を及ぼさないように、アセンブリをドメインに中立にする場合。 ドメイン中立のアセンブリはグローバル アセンブリ キャッシュにインストールされている必要があるため、この場合は厳密な名前を付ける必要があります。  
  
- 発行者ポリシーを提供することにより、アプリへのサービスを集中管理する場合。これは、グローバル アセンブリ キャッシュにアセンブリがインストールされる必要があることを意味します。  
  
 オープン ソースの開発者が厳密な名前付きのアセンブリによる ID の利点を必要とする場合、アセンブリに関連付けられた秘密キーをソース コントロール システムにチェックインすることを検討してください。  
  
## <a name="see-also"></a>関連項目

- [グローバル アセンブリ キャッシュ](../../../docs/framework/app-domains/gac.md)
- [方法: 厳密な名前でアセンブリに署名する](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md)
- [Sn.exe (厳密名ツール)](../../../docs/framework/tools/sn-exe-strong-name-tool.md)
- [厳密な名前付きアセンブリの作成と使用](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)
