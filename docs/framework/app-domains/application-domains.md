---
title: アプリケーション ドメイン
ms.date: 03/30/2017
helpviewer_keywords:
- process boundaries for isolation
- application isolation
- application domains, about
- common language runtime, application domains
- application domains
- runtime, application domains
- isolation between applications
- code, verification process
- verification testing code
ms.assetid: 113a8bbf-6875-4a72-a49d-ca2d92e19cc8
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 571b049300a7c7de963bd762e0266f66060479fe
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927993"
---
# <a name="application-domains"></a>アプリケーション ドメイン

オペレーティング システムやランタイム環境では、通常、複数のアプリケーションがなんらかの形で分離されています。 たとえば、Windows ではプロセスを使用してアプリケーションが分離されています。 このような分離は、あるアプリケーションで実行されているコードが、関係のない別のアプリケーションに悪影響をもたらさないようにするために必要です。  
  
 アプリケーション ドメインは、セキュリティ、信頼性、バージョン管理のための、またアセンブリをアンロードするための分離の境界を提供します。 通常、アプリケーション ドメインは、アプリケーションの実行前に共通言語ランタイムの起動を行うランタイム ホストによって作成されます。  
  
## <a name="the-benefits-of-isolating-applications"></a>アプリケーションを分離する利点

 これまで、同じコンピューター上で実行される複数のアプリケーションを分離するためには、プロセス境界が使用されていました。 この場合、各アプリケーションが独立のプロセスに読み込まれることで、アプリケーションは同じコンピューター上で実行されるほかのアプリケーションから分離されます。  
  
 アプリケーションが分離されるのは、メモリ アドレスがプロセスごとの相対アドレスになっていたためです。つまり、メモリ ポインターをあるプロセスから別のプロセスに渡しても、そのポインターが渡された側のプロセスでは機能しませんでした。 また、2 つのプロセス間で直接呼び出しを行うこともできませんでした。 代わりに間接的な呼び出しを行う場合は、プロキシを使用する必要がありました。  
  
 マネージド コードは、実行される前に必ず検査プロセスに渡されます (管理者が検査を省略する許可をコードに与えた場合は除きます)。 検査プロセスでは、そのコードが無効なメモリ アドレスにアクセスしたり、コードが実行されるプロセスの正常実行を妨げる原因となる動作を実行したりすることがないかどうかを確認します。 検査テストを通過したコードは、タイプ セーフであると言われます。 コードがタイプ セーフかどうかを検査するこのような機能があるため、共通言語ランタイムでは、プロセス境界と同等の高度な分離レベルを実現しながら、パフォーマンスへの影響は大幅に低く抑えることができます。  
  
 アプリケーション ドメインは、共通言語ランタイムがアプリケーション間を分離するために使用できる、より安全で柔軟性に富んだ処理単位となります。 個別のプロセスを使用する場合と同じ分離レベルを実現しながら、しかしプロセス間での呼び出しやプロセスの切り替えによるオーバーヘッドを生じることもなく、1 つのプロセス内で複数のアプリケーション ドメインを実行できます。 1 つのプロセス内で複数のアプリケーションを実行できるため、サーバーのスケーラビリティが飛躍的に向上します。  
  
 アプリケーションの分離は、アプリケーションのセキュリティを考えるうえでも重要です。 たとえば、複数のコントロールが互いのデータやリソースにアクセスできないようにして、1 つのブラウザー プロセスで複数の Web アプリケーションのコントロールを実行できます。  
  
 アプリケーション ドメインによる分離には、次の利点があります。  
  
- 1 つのアプリケーションで発生したエラーが、ほかのアプリケーションに影響することはありません。 タイプ セーフなコードではメモリ フォールトが発生しないため、アプリケーション ドメインを使用することで、1 つのドメインで実行されているコードが同じプロセス内のほかのアプリケーションに影響することが確実になくなります。  
  
- プロセス全体を停止せずに、個々のアプリケーションを停止できます。 アプリケーション ドメインを使用すると、1 つのアプリケーション内で実行されているコードをアンロードできます。  
  
    > [!NOTE]
    > 個々のアセンブリや型はアンロードできません。 アンロードできるのはドメイン全体だけです。  
  
- 1 つのアプリケーションで実行されているコードは、ほかのアプリケーションのコードやリソースに直接アクセスできません。 共通言語ランタイムでは、異なるアプリケーション ドメインにあるオブジェクト間での直接呼び出しを禁止することで分離を実現しています。 ドメイン間で渡されるオブジェクトは、コピーされるか、またはプロキシ経由でアクセスされます。 オブジェクトがコピーされる場合、オブジェクトの呼び出しはローカル呼び出しです。 つまり、呼び出し元と参照先オブジェクトの両方が、同じアプリケーション ドメイン内にあります。 オブジェクトがプロキシ経由でアクセスされる場合は、オブジェクトの呼び出しはリモート呼び出しです。 この場合は、呼び出し元と参照先オブジェクトが別のアプリケーション ドメイン内にあります。 ドメイン間呼び出しでは、2 つのプロセス間や 2 台のコンピューター間での呼び出しと同じリモート呼び出しインフラストラクチャが使用されます。 そのため、メソッドの呼び出しが正しく JIT コンパイルされるように、参照先オブジェクトのメタデータが両方のアプリケーション ドメインから利用できることが必要です。 呼び出し元のドメインが呼び出し先オブジェクトのメタデータにアクセスできない場合、コンパイルは <xref:System.IO.FileNotFoundException> という例外が発生して失敗する可能性があります。 詳細については、「 [Remote Objects](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))」を参照してください。 ドメイン間でオブジェクトにアクセスする方法は、アクセス対象のオブジェクトによって決まります。 詳細については、<xref:System.MarshalByRefObject?displayProperty=nameWithType> を参照してください。  
  
- コードが影響する範囲は、そのコードが実行されるアプリケーションによって決まります。 つまり、アプリケーション ドメインは、アプリケーションのバージョン ポリシー、アクセス対象となるリモート アセンブリの位置、ドメインに読み込まれるアセンブリの場所に関する情報などの構成設定を提供します。  
  
- コードに与えられるアクセス許可は、そのコードが実行されるアプリケーション ドメインによって制御されます。  
  
## <a name="application-domains-and-assemblies"></a>アプリケーション ドメインとアセンブリ

 このセクションでは、アプリケーション ドメインとアセンブリの関係について説明します。 アセンブリに含まれるコードを実行する前に、そのアセンブリをアプリケーション ドメインに読み込む必要があります。 通常のアプリケーションを実行すると、複数のアセンブリがアプリケーション ドメインに読み込まれます。  
  
 アセンブリが読み込まれる方法によって、そのアセンブリの Just-In-Time (JIT) コンパイル コードをプロセス内の複数のアプリケーション ドメインで共有できるかどうか、およびアセンブリをプロセスからアンロードできるかどうかが決まります。  
  
- アセンブリがドメインに中立として読み込まれる場合は、同じセキュリティ許可セットを共有するすべてのアプリケーション ドメインが同じ JIT コンパイル コードを共有できるため、アプリケーションに必要なメモリを削減できます。 ただし、アセンブリをプロセスからアンロードできなくなります。  
  
- アセンブリがドメインに中立として読み込まれない場合は、そのアセンブリが読み込まれる各アプリケーション ドメインで、そのアセンブリを JIT でコンパイルする必要があります。 ただし、アセンブリが読み込まれているアプリケーション ドメインをすべてアンロードすることで、プロセスからアセンブリをアンロードできます。  
  
 ランタイム ホストは、ランタイムをプロセスに読み込むときに、アセンブリをドメインに中立なアセンブリとして読み込むかどうかを決定します。 マネージド アプリケーションの場合は、<xref:System.LoaderOptimizationAttribute> 属性をプロセスのエントリ ポイント メソッドに適用し、関連付けられた <xref:System.LoaderOptimization> 列挙体から値を指定します。 共通言語ランタイムをホストするアンマネージ アプリケーションの場合は、[CorBindToRuntimeEx 関数](../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)メソッドを呼び出すときに適切なフラグを指定します。  
  
 アセンブリをドメインに中立として読み込むかどうかに関して、次の 3 つのオプションがあります。  
  
- <xref:System.LoaderOptimization.SingleDomain?displayProperty=nameWithType> では、常にドメインに中立として読み込まれる Mscorlib を除き、どのアセンブリもドメインに中立として読み込まれません。 この設定は、ホストがプロセス内で 1 つのアプリケーションだけを実行する場合に一般的に使用されるため、シングル ドメインと呼ばれます。

- <xref:System.LoaderOptimization.MultiDomain?displayProperty=nameWithType> では、すべてのアセンブリがドメインに中立として読み込まれます。 この設定は、同じコードを実行する複数のアプリケーション ドメインが 1 つのプロセス内に存在する場合に使用します。

- <xref:System.LoaderOptimization.MultiDomainHost?displayProperty=nameWithType> では、厳密な名前が付いたアセンブリとそのすべての依存関係がグローバル アセンブリ キャッシュにインストールされている場合に、それらのアセンブリがドメインに中立として読み込まれます。 その他のアセンブリは、それらが読み込まれる各アプリケーション ドメインで個別に読み込まれ、JIT でコンパイルされるため、プロセスからアンロードできます。 この設定は、同じプロセスで複数のアプリケーションが実行されている場合、または多数のアプリケーション ドメインで共有されているアセンブリと、プロセスからアンロードする必要があるアセンブリが混在している場合に使用します。
  
 <xref:System.Reflection.Assembly.LoadFrom%2A> クラスの <xref:System.Reflection.Assembly> メソッドを使用して読み込み元を指定して読み込まれたアセンブリ、またはバイト配列を指定する <xref:System.Reflection.Assembly.Load%2A> メソッドのオーバーロードを使用してイメージから読み込まれたアセンブリについては、JIT コンパイル コードを共有できません。  
  
 [Ngen.exe (ネイティブ イメージ ジェネレーター)](../../../docs/framework/tools/ngen-exe-native-image-generator.md) を使用してネイティブ コードにコンパイルされたアセンブリは、プロセスに最初に読み込まれるときにドメインに中立として読み込まれていれば、アプリケーション ドメイン間で共有できます。  
  
 アプリケーションのエントリ ポイントを含むアセンブリの JIT コンパイル コードは、そのすべての依存関係を共有できる場合にだけ共有されます。  
  
 ドメインに中立なアセンブリは、JIT で複数回コンパイルできます。 たとえば、2 つのアプリケーション ドメインのセキュリティ許可セットが異なっている場合、それらのドメインは同じ JIT コンパイル コードを共有できません。 ただし、JIT コンパイル アセンブリの各コピーは、同じ許可セットを持つ他のアプリケーション ドメインと共有できます。  
  
 アセンブリをドメインに中立として読み込むかどうかを判断する場合は、メモリ使用量の削減とその他のパフォーマンス要因とのトレードオフを考慮する必要があります。  
  
- ドメインに中立のアセンブリでは、アセンブリを分離する必要があることから、静的データおよびメソッドにアクセスする速度が遅くなります。 静的フィールド内のオブジェクトがドメイン境界を越えて参照されることがないように、アセンブリにアクセスする各アプリケーション ドメインが、静的データのコピーを個別に保持する必要があるためです。 その結果、ランタイムには、呼び出し元が静的データまたは静的メソッドの適切なコピーにアクセスできるようにするための追加のロジックが必要となります。 この追加のロジックのために、呼び出しの処理速度が低下します。  
  
- アセンブリがドメインに中立で読み込まれるときに、アセンブリのすべての依存関係を探し出して読み込む必要があります。これは、ドメインに中立として読み込むことのできない依存関係があると、アセンブリをドメインに中立として読み込むことができなくなるからです。  
  
## <a name="application-domains-and-threads"></a>アプリケーション ドメインとスレッド

 アプリケーション ドメインは、セキュリティ、バージョン管理、信頼性のための、またマネージド コードをアンロードするための分離の境界を形成します。 スレッドは、共通言語ランタイムがコードを実行するために使用する、オペレーティング システムの構成です。 実行時には、すべてのマネージド コードがアプリケーション ドメインに読み込まれ、1 つまたは複数のマネージド スレッドによって実行されます。  
  
 アプリケーション ドメインとスレッドとの関係は一対一ではありません。 1 つのアプリケーション ドメイン内で一度に複数のスレッドが実行される場合があり、また 1 つのスレッドが 1 つのアプリケーション ドメインに限定されることもありません。 つまり、スレッドはアプリケーション ドメイン境界を自由に越えることができ、アプリケーション ドメインごとに新しいスレッドが生成されるわけではありません。  
  
 特定の時点に限って見ると、どのスレッドも 1 つのアプリケーション ドメイン内で実行されています。 特定のアプリケーション ドメインでゼロ、1 つ、または複数のスレッドを実行できます。 ランタイムは、どのスレッドがどのアプリケーション ドメインで実行されているかを追跡しています。 任意の時点で、あるスレッドが実行されているドメインを特定するには、<xref:System.Threading.Thread.GetDomain%2A?displayProperty=nameWithType> メソッドを呼び出します。

### <a name="application-domains-and-cultures"></a>アプリケーション ドメインとカルチャ

 <xref:System.Globalization.CultureInfo> オブジェクトによって表されるカルチャは、スレッドに関連付けられます。 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> プロパティを使用すると、現在実行しているスレッドに関連付けられているカルチャを取得できます。<xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType> プロパティを使用すると、現在実行しているスレッドに関連付けられているカルチャを取得または設定できます。 スレッドに関連付けられているカルチャが <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType> プロパティを使用して明示的に設定されている場合、スレッドがアプリケーション ドメインの境界を越えても、そのスレッドとの関連付けが維持されます。 それ以外の場合、スレッドに関連付けられるカルチャは、任意の時点でスレッドが実行されているアプリケーション ドメインの <xref:System.Globalization.CultureInfo.DefaultThreadCurrentCulture%2A?displayProperty=nameWithType> プロパティの値によって決まります。  
  
- プロパティの値が `null` でない場合、プロパティによって返されるカルチャはスレッドに関連付けられます (したがって <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType> プロパティと <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> プロパティによって返されます)。  
  
- プロパティの値が `null` の場合は、現在のシステム カルチャがスレッドに関連付けられます。  
  
## <a name="programming-with-application-domains"></a>アプリケーション ドメインを使用したプログラミング

 通常、アプリケーション ドメインは、ランタイム ホストによってプログラムで作成および操作されます。 しかし、アプリケーション プログラムでもアプリケーション ドメインを操作する必要が生じる場合があります。 たとえば、アプリケーション プログラムはアプリケーション コンポーネントをドメインに読み込むことができるため、アプリケーション全体を停止せずにドメイン (およびコンポーネント) をアンロードできます。  
  
 <xref:System.AppDomain>は、アプリケーション ドメインに対するプログラム インターフェイスです。 このクラスには、ドメインを作成およびアンロードするメソッド、型のインスタンスをドメイン内に作成するメソッド、およびアプリケーション ドメインのアンロードなどの各種通知に登録するメソッドが含まれています。 一般的に使用される <xref:System.AppDomain> メソッドを次の表に示します。  
  
|AppDomain メソッド|説明|  
|----------------------|-----------------|  
|<xref:System.AppDomain.CreateDomain%2A>|新しいアプリケーション ドメインを作成します。 <xref:System.AppDomainSetup> オブジェクトを指定するこのメソッドのオーバーロードを使用することをお勧めします。 これは、アプリケーション ベース (アプリケーションのルート ディレクトリ)、ドメインの構成ファイルの場所、ドメインにアセンブリを読み込むときに共通言語ランタイムが使用する検索パスなど、新しいドメインのプロパティを設定する場合に望ましい方法です。|  
|<xref:System.AppDomain.ExecuteAssembly%2A> および <xref:System.AppDomain.ExecuteAssemblyByName%2A>|アプリケーション ドメインでアセンブリを実行します。 これはインスタンス メソッドであるため、参照先の別のアプリケーション ドメインでコードを実行する場合に使用できます。|  
|<xref:System.AppDomain.CreateInstanceAndUnwrap%2A>|指定した型のインスタンスをアプリケーション ドメイン内に作成し、プロキシを返します。 このメソッドを使用することで、作成された型を含むアセンブリが呼び出し元のアセンブリに読み込まれることを回避できます。|  
|<xref:System.AppDomain.Unload%2A>|ドメインを正常にシャットダウンします。 アプリケーション ドメインは、ドメイン内で実行されているすべてのスレッドが停止するか、またはドメイン内に存在しなくなるまで、アンロードされません。|  
  
> [!NOTE]
> 共通言語ランタイムはグローバル メソッドのシリアル化をサポートしないため、デリゲートを使用して他のアプリケーション ドメインでグローバル メソッドを実行できません。  
  
 共通言語ランタイムの仕様、「Hosting Interfaces」で説明されているアンマネージ インターフェイスも、アプリケーション ドメインへのアクセスを提供します。 ランタイム ホストは、アンマネージ コードのインターフェイスを使用して、プロセス内にアプリケーション ドメインを作成し、そのドメインにアクセスできます。  
  
## <a name="the-complus_loaderoptimization-environment-variable"></a>COMPLUS_LoaderOptimization 環境変数

 実行可能アプリケーションの既定のローダーの最適化ポリシーを設定する環境変数。  
  
### <a name="syntax"></a>構文  
  
```  
COMPLUS_LoaderOptimization = 1  
```  
  
### <a name="remarks"></a>解説

 一般的なアプリケーションでは、アプリケーション ドメインに複数のアセンブリが読み込まれてから、それに含まれるコードが実行されます。  
  
 アセンブリが読み込まれる方法によって、そのアセンブリの Just-In-Time (JIT) コンパイル コードをプロセス内の複数のアプリケーション ドメインで共有できるかどうかが決まります。  
  
- アセンブリがドメイン中立として読み込まれる場合は、同じセキュリティ許可セットを共有するすべてのアプリケーション ドメインが同じ JIT コンパイル コードを共有できます。 このため、アプリケーションが必要とするメモリを抑えることができます。  
  
- アセンブリがドメイン中立として読み込まれない場合、読み込まれるすべてのアプリケーション ドメインで JIT コンパイル済みである必要があり、またローダーはアプリケーション ドメイン間で内部リソースを共有できません。  
  
 COMPLUS_LoaderOptimization 環境フラグを 1 に設定すると、ランタイム ホストは強制的にすべてのアセンブリを SingleDomain と呼ばれるドメイン中立でない方法で読み込みます。 SingleDomain では、常にドメインに中立として読み込まれる Mscorlib を除き、どのアセンブリもドメインに中立として読み込まれません。 この設定は、ホストがプロセス内で 1 つのアプリケーションだけを実行する場合に一般的に使用されるため、シングル ドメインと呼ばれます。  
  
> [!CAUTION]
>  COMPLUS_LoaderOptimization 環境フラグは診断およびテストのシナリオで使用するように設計されています。 このフラグをオンにすることにより、速度の大幅な低下と使用メモリの増大が発生する場合があります。  
  
### <a name="code-example"></a>コード例

 環境の HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\IISADMIN キーの複数文字列値に `COMPLUS_LoaderOptimization=1` を追加することにより、強制的にすべてのアセンブリを IISADMIN サービスにドメイン中立として読み込まないようにできます。  
  
```  
Key = HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\IISADMIN  
Name = Environment  
Type = REG_MULTI_SZ  
Value (to append) = COMPLUS_LoaderOptimization=1  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.AppDomain?displayProperty=nameWithType>
- <xref:System.MarshalByRefObject?displayProperty=nameWithType>
- [アプリケーション ドメインとアセンブリを使用したプログラミング](index.md)
- [アプリケーション ドメインの使用](use.md)
